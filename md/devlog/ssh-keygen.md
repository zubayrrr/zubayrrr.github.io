---
created: 1653572822588
desc: ''
id: uero6kfpt6ymlishvgxvhhe
title: Ssh Keygen
updated: 1653573859935
---
   
Related::  [ssh](../devlog/ssh.md)   
   
   
---   
   
Ssh-keygen is a tool for creating new authentication key pairs for SSH. Such key pairs are used for automating logins, single sign-on, and for authenticating hosts.   
   
The [SSH](../devlog/ssh.md) protocol uses public key cryptography for authenticating hosts and users. The authentication keys, called SSH keys, are created using the keygen program.   
   
SSH supports several public key algorithms for authentication keys. These include:   
   
rsa - an old algorithm based on the difficulty of factoring large numbers. A key size of at least 2048 bits is recommended for RSA; 4096 bits is better. RSA is getting old and significant advances are being made in factoring. Choosing a different algorithm may be advisable. It is quite possible the RSA algorithm will become practically breakable in the foreseeable future. All SSH clients support this algorithm.   
   
dsa - an old US government Digital Signature Algorithm. It is based on the difficulty of computing discrete logarithms. A key size of 1024 would normally be used with it. DSA in its original form is no longer recommended.   
   
ecdsa - a new Digital Signature Algorithm standarized by the US government, using elliptic curves. This is probably a good algorithm for current applications. Only three key sizes are supported: 256, 384, and 521 (sic!) bits. We would recommend always using it with 521 bits, since the keys are still small and probably more secure than the smaller keys (even though they should be safe as well). Most SSH clients now support this algorithm.   
   
ed25519 - this is a new algorithm added in OpenSSH. Support for it in clients is not yet universal. Thus its use in general purpose applications may not yet be advisable.   
   
The algorithm is selected using the -t option and key size using the -b option. -c "Comment" to add/update the comment for a keyfile.   
   
## Generate a keyfile   
   
`ssh-keygen -t rsa -b 2048 -C "Key generated for remote machine on date"`   
   
The private and the public key can be found inside the `.ssh` dir of the user's home dir.   
   
You'll need to add the public key(`.pub`) to the remote machine.   
   
## Copy the public key   
   
Running `ssh-copy-id root@ip-addr` will append the public key to the remote machine's authorized keys(`.ssh/authorized_keys`)   
   
   
   
---   
## SSH key format   
   
 PKCS#1 key files (BEGIN RSA PRIVATE KEY) come from the PEM encrypted messaging project. The format is fairly outdated, e.g. it's weak against passphrase bruteforcing. Even OpenSSL itself later started using a newer PKCS#8 format (which uses BEGIN PRIVATE KEY or BEGIN ENCRYPTED PRIVATE KEY headers) for all new private keys.   
   
However, both PKCS#1 and PKCS#8 formats internally use ASN.1, which is a rather complex data serialization method – for TLS software that's still acceptable, because they already need ASN.1 support to parse TLS certificates anyway, but for SSH clients it just brings another unnecessary dependency on OpenSSL.   
   
In addition, their development is also primarily driven by TLS and X.509 certificates, which is a different world from SSH – for example, when OpenSSH first got support for Ed25519 keys, it couldn't use OpenSSL's existing functions to store them, because that algorithm hadn't been adopted by the TLS world yet; an algorithm ID hadn't been assigned, the data format hadn't been agreed to.   
   
So as a result, OpenSSH created its own format for storing private keys (the one with BEGIN OPENSSH PRIVATE KEY headers), which uses the same structures and algorithm identifiers as SSH itself does, meaning that any keys that SSH supports can be stored in the OpenSSH key format – and they can be loaded/stored without relying on a SSL/TLS library any longer. — via [ssh - Differences between "BEGIN RSA PRIVATE KEY" and "BEGIN OPENSSH PRIVATE KEY" - Super User](https://superuser.com/questions/1720991/differences-between-begin-rsa-private-key-and-begin-openssh-private-key)