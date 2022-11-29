---
created: 1662341857497
desc: ''
id: 2iyixxnnc2hsl2lb1jqwdz9
title: Helm Chart for Microservices
updated: 1662349263978
---
   
Related::  [kubernetes.helm](../devlog/kubernetes.helm.md), [microservices](../devlog/microservices.md), [kubernetes.microservices](../devlog/kubernetes.microservices.md)   
   
   
---   
   
Create Helm Chart for Microservice.   
   
In [kubernetes.Deploy Microservices Application](../devlog/kubernetes.Deploy%20Microservices%20Application.md) we saw that we've same attributes but different values across all of our 10 Deployments & Services.   
   
Let's create a single blueprint for Deployment and Service for all Microservice where we can set values for individual Microservices keeping our code DRY using Helm Charts.   
   
We can do it in 2 ways:   
   
1. Create 1 Helm Chart for each Microservice.   
   
   - Which is preferable if the configurations are different across the different MSes.   
2. Create 1 Shared Helm Chart for all Microservices.   
   
We can even use both of these methods in combination by create a shared chart for applications that are similar, pass values for them and create separate charts for the applications that use completely different configuration.   
   
In our case, we'll go with the 2nd option.   
   
## Basic Structure   
   
`helm chart microservice` will bootstrap a folder "microservice" with some auto-generated files inside.   
   
   
- `Chart.yaml` describes the metadata.   
- `charts` dir stores chart dependencies.   
- `.helmignore` defines stuff that you don't want to include in your helm chart when building chart archived. Helm charts can be built and distributed just like any other artifacts.   
- `templates` dir is where the actual K8s YAML files(template files) are created.   
   
The structure of the template files is the same as actual K8s YAML files. As for values, there are placeholders with `{{}}` ([Chart Template Guide | Helm Docs](https://helm.sh/docs/chart_template_guide/control_structures/))   
   
The Helm template syntax is based on the Go programming language's [text/template package](https://pkg.go.dev/text/template).   
   
The braces `{{` and `}}` are the opening and closing brackets to enter and exit template logic.   
   
`values.yaml` is where the actual values are set.   
   
Values are passed into template from 3 sources,   
   
   
- the `values.yaml` file in the chart.   
- user-supplied, custom `values.yaml` file passed with `-f` flag.   
- parameter passed with `--set` flag.   
   
**Built-in Objects**   
   
Helm uses many built-in objects, that are passed into template by the template engine.   
Examples: "Release", "Files", "Values" etc. See [Helm | Built-in Objects](https://helm.sh/docs/chart_template_guide/builtin_objects/)   
   
User-defined variable names can be in any case however, the naming convention is camelCase.   
   
**Flat or Nested Values**   
   
Values may be flat or deeply nested, although Helm recommends flat structure.   
   
```yaml
appName: myapp
appReplicas: 1
```
   
   
```yaml
app:
  name: myapp
  replicas: 1
```
   
   
**Dynamic Environment Variables**   
   
Environment variables values as interpreted as strings. So, you've to keep them quoted using the **quote** function with **Pipelines** (`|`) which is similar to [piping](../devlog/piping.md) in Unix or Unix-like systems.   
   
**-range**   
   
Provides a "for each" style loop to iterate through or "range over" a list.   
   
   
---   
   
```yaml
# deployment.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: { { .Values.appName } } # Values is an built-in object which is empty by default
spec:
  replicas: { { .Values.appReplicas } }
  selector:
    matchLabels:
      app: { { .Values.appName } }
  template:
    metadata:
      labels:
        app: { { .Values.appName } }
    spec:
      containers:
        - name: { { .Values.appName } }
          image: "{{ .Values.appImage }}:{{ .Values.appVersion }}"
          ports:
            - containerPort: { { .Values.containerPort } }
          env:
          {{- range .Values.containerEnvVars}} # The dash syntax causes white space to be removed.
          - name: { { .name } }
            value: { { .value | quote } }
          {{- end}}
```
   
   
```yaml
# service.yaml
---
apiVersion: v1
kind: Service
metadata:
  name: { { .Values.appName } }
spec:
  type: { { .Values.serviceType } }
  selector:
    app: { { .Values.appName } }
  ports:
    - protocol: TCP
      port: { { .Values.servicePort } }
      targetPort: { { .Values.containerPort } }
```
   
   
Declaring default values that will ultimately be substituted for real values.   
   
```yaml
# for deployment.yaml
appName: appServiceName
appImage: gcr.io/google-samples/microservices-demo/appServiceName
appVersion: v.0.0.0
appReplicas: 1
containerPort: 8080
containerEnvVars:
  - name: ENV_VAR_ONE
    value: "valueone"
  - name: ENV_VAR_TWO
    value: "valuetwo"
###
# for services.yaml
###
servicePort: 8080
serviceType: ClusterIP
```
   
   
   
---   
   
For each Microservice create a file `<microservice>-values.yaml` and fill in all the values.   
   
`helm template` to render chart templates locally and display output.   
   
To check if you're producing valid helm files - `helm template -f <microservice>-values.yaml microservice`   
   
`helm lint` examines chart for possible issues, where ERRORS are issues that will render a chart uninstallable and WARNINGS are issues that break conventions and recommendations.   
   
**--dry-run**   
   
Another way of checking if our helm files are valid is using the `--dry-run` flag, it does this by sending the files to the cluster, while `helm template` only validates locally.   
   
`helm install --dry-run -f values/<microservice>-values.yaml <release-name> charts/<microservice>`   
   
It also gives a preview of what will be install on the cluster, similar to `terraform plan`.   
   
**helm install**   
   
"Creating a new release"   
   
release name = app name   
   
`helm install -f myvalues.yaml <release-name> <chart-name>`   
   
`helm ls` to list Microservices running, similar to `kubectl get pod`.   
   
You can define values for the rest of the Microservices inside `charts/values/` dir.   
   
## Create Redis Helm Chart   
   
Move the `microservice` dir into a `charts` dir as we create a new chart for Redis.   
   
`helm create redis`   
   
```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: { { .Values.appName } }
spec:
  replicas: { { .Values.appReplicas } }
  selector:
    matchLabels:
      app: { { .Values.appName } }
  template:
    metadata:
      labels:
        app: { { .Values.appName } }
    spec:
      containers:
        - name: { { .Values.appName } }
          image: "{{ .Values.appImage }}:{{ .Values.appVersion }}"
          ports:
            - containerPort: { { .Values.containerPort } }
          volumeMounts:
            - name: { { .Values.volumeName } }
              mountPath: { { .Values.containerMountPath } }
      volumes:
        - name: { { .Values.volumeName } }
          emptyDir: {}
```
   
   
```yaml
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: { { .Values.appName } }
spec:
  type: ClusterIP
  selector:
    app: { { .Values.appName } }
  ports:
    - protocol: TCP
      port: { { .Values.servicePort } }
      targetPort: { { .Values.containerPort } }
```
   
   
```yaml
# values.yaml
appName: redis
appImage: redis
appVersion: alpine
appReplicas: 1
containerPort: 6379
volumeName: redis-data
containerMountPath: /data

servicePort: 6379
```
   
   
## Deploying Microservices with `helm install`   
   
1. `helm install` for each MS one by one manually.   
2. Write a bash script `install.sh` and list all the `helm install` commands.   
   
   - Not really the most elegant solution, if you want to uninstall it, you'd need to `helm uninstall <microservice>` each MS one by one.   
3. Using a `Helmfile`   
   
## Helmfile   
   
It is a declarative way of telling helm what charts to deploy. Similar to how [terraform](../devlog/terraform.md) works, you can define a desired state. You can declare a definition of an entire K8s cluster in a single `helmfile.yaml`. You can define multiple helm "releases" in it and change specifications of each release depending on application or type of environment.   
   
```yaml
# helmfile.yaml
repositories:
  - name: stable
    url: https://kubernetes-charts.storage.googleapis.com

releases:
  - name: postgres
    chart: ./charts/postgres
    values:
      - ./values/kanban-postgres.yaml

  - name: ingress-backend
    chart: stable/nginx-ingress
    version: 1.36.0

  - name: ingress-controller
    chart: ./charts/ingress
    values:
      - ./values/ingress.yaml
```
   
   
**Create a Helmfile**   
   
```yaml
releases:
  - name: rediscart
    chart: charts/redis
    values:
      - values/redis-values.yaml
      - appReplicas: "1" # overwriting values from values.yaml
      - volumeName: "redis-cart-data"

  - name: emailservice
    chart: charts/microservice
    values:
      - values/email-service-values.yaml

  - name: cartservice
    chart: charts/microservice
    values:
      - values/cart-service-values.yaml

  - name: currencyservice
    chart: charts/microservice
    values:
      - values/currency-service-values.yaml

  - name: paymentservice
    chart: charts/microservice
    values:
      - values/payment-service-values.yaml

  - name: recommendationservice
    chart: charts/microservice
    values:
      - values/recommendation-service-values.yaml

  - name: productcatalogservice
    chart: charts/microservice
    values:
      - values/productcatalog-service-values.yaml

  - name: shippingservice
    chart: charts/microservice
    values:
      - values/shipping-service-values.yaml

  - name: adservice
    chart: charts/microservice
    values:
      - values/ad-service-values.yaml

  - name: checkoutservice
    chart: charts/microservice
    values:
      - values/checkout-service-values.yaml

  - name: frontendservice
    chart: charts/microservice
    values:
      - values/frontend-values.yaml
```
   
   
**Install Helmfile**   
   
   
- [Install Helmfile package](https://helmfile.readthedocs.io/en/latest/#installation) .   
- `helmfile sync`   
  - It'll compare the current state with desired state and plan what needs to be done.   
- `helmfile list` shows the currently installed releases helm manages.   
   
**Uninstall Releases**   
   
`helmfile destroy`   
   
**Where to host Helm Charts**   
   
   
- Helm Charts are [IaC](../devlog/IaC.md) and we'll store them in a [version control.git](../devlog/version%20control.git.md) repo.   
  - Package it along with your microservices code.   
  - OR have a separate Git repo for just Helm Charts.   
   
**How does this fit in the [CICD pipeline](../devlog/CICD%20pipeline.md) or DevOps workflow?**   
   
You as a DevOps engineer would create these charts for the developers and hand it over to the developers and they will "use" these Helm Charts.   
   
   
---   
   
You can find the finished code at [zubayrrr / online-shop-microservices-deployment](https://gitlab.com/zubayrrr/online-shop-microservices-deployment)