---
created: 20211104135155144
desc: ''
id: 86tzgnwq8iyzo91f8d7dxv1
title: Java
updated: 1652818296559
---
   
Topics::  [programming](../topics/programming.md)   
   
   
---   
   
   
- Java is a platform independent language.   
  - They brought a layer on top of operating systems known as the [JVM](/not_created.md).   
  - Java was originally designed to write programs for things like refrigrator, cars etc.   
   
### To print a string out to the console   
   
`System.out.println("Hello world!");`   
   
### Declaring integers   
   
`int variableName = value;`   
   
### Adding variables and printing them to the console   
   
    int x = 5;   
    int y = 6;   
    int sum = x + y;   
    System.out.printlt(sum);   
   
### String concatenation   
   
    System.out.println("sum = " + sum)   
   
### `if` statement   
   
    if(y > x){   
        System.out.println("y is greater than x")   
    }   
   
### `else` statement   
   
    if(y > x){   
        System.out.println("y is greater than x");   
    }else if(y == x){   
        System.out.println("y is equal to x");   
    }else{   
        System.out.println("y is less than x");   
    }   
   
### Arithmetic operators   
   
   
- `+`- Addition   
- `-` - Subtraction   
- `*` - Multiplication   
- `/` - Division   
- `%` - Modulo Operation (Remainder after division   
- `++` - Increment   
- `--` - Decrement   
- `+=` - Addition Assignment   
- `-=` - Subtraction Assignment   
- `*=` - Multiplication Assignment   
- `/=` - Divison Assignment   
- `%=` - Modulus Assignment   
   
### Relational operators   
   
   
- `==` - Is Equal To   
- `=` - Assignment   
- `!=` - Not Equal To   
- `>` - Greater Than   
- `<` - Less Than   
- `>=` - Greater Than Or Equal To   
- `<=` - Less Than Or Equal To   
   
### Syntactic rules   
   
   
- Any complete statement will end in a semi colon (`;`)   
   
### `for` loop   
   
    // for(initial value; condition; increment/decrement), i++ is like writing i=i+1 or i += 1   
    for(int i = 0; i <= 10; i++){   
        System.out.println("i = " + i);   
    }   
   
### `while` loop   
   
    int x = -10;   
   
    while(x <= 0){   
        System.out.println("x = " + x);   
        x++;   
    }   
   
### `do` `while` loop   
   
    // most important difference from the while loop is that a do while loop will run at least once   
   
    int x = 10;   
   
    do{   
        System.out.println("x = " + x);   
        x--;   
    }while(x > 0);   
   
### And `&&` Or `||`   
   
    int x, y;   
    x = 10;   
    y = -10;   
   
    if (x > 0 && y > 0){   
        System.out.println("Both integers are +ve");   
    }else if (x > 0 || y > 0){   
        System.out.println("At least one integer is +ve");   
    }else{   
        System.out.println("Both integers are -ve")   
    }   
   
`&` \<– verifies both operands,   
`&&` \<– stops evaluating if the first operand evaluates to false since the result will be false, used in [bitwise operations](/not_created.md)   
   
### `switch` `case` statement   
   
    int j = 2;   
   
    switch(j){   
        case 0:   
            System.out.println("Value is 0");   
            break;   
        case 1:   
            System.out.println("Value is 1")   
            break;   
        case 2:   
            System.out.println("Value is 2")   
            break;   
        case 3:   
            System.out.println("Value is 3")   
            break;   
        default:   
            System.out.println("No Value")   
            break;   
   
    }   
   
   
- Wrapper classes such as Integer   
- Arrays, empty arrays   
- Two Dimensional Arrays, empty two dim arrays   
- Enhanced For loop   
- String   
  - Is not a primitive data type. Use String to store text.   
  - In built methods such as `toUpperCase()`   
- Primitive Datatypes:   
  - byte   
  - short   
  - int   
  - long   
  - float   
  - double   
  - char   
  - boolean   
- class and objects   
  - class has data and methods, class are templates   
  - objects are instances (copy) of classes, objects will inherit data and methods defined in the class, objects can pass in parameters to the methods(of their class),   
  - When you dont pass any parameters to the object, the constructor will define the default values   
  - constructors are run when the object is created, they've the same name as a class name, they're used to define default values .   
    - constructors do not return anything, including void   
  - you can overload a constructor also(by defining another constructor that takes in parameters)   
  - this keyword is used to refer to the data of the class(class level data) itself(as opposed to the data defined inside a method on a class, method is also called as a function)   
  - `void` keyword is put infront of a method when that method is not returning anything, if its only using the data right in that function.   
  - Create objects from a class   
    - `objName = new ClassName()`   
    - `ClassName objName = new ClassName()`   
  - When you want a method to return something, put the name of datatype that the method is returning infront of it, instead of `void`   
  - passing arguments take precedence over class level data   
- Object Oriented programming   
  - Encapsulation   
    - Data hiding   
  - Polymorphism   
    - overloading   
    - overriding   
  - Inheritance   
    - Abstract classes   
    - Interfaces   
   
Overloading:   
   
   
- having multiple methods named same but the ability of the language to decide which method to use based on the parameters being passed to the method   
   
Encapsulation: data and methods that act on the data (setters and getters)   
   
Data hiding:   
   
   
- Limiting data to class, subclass or project to protect data using **access modifiers**   
- `private` will limit it to the class   
- `public` all access(class, package, subclass, project)   
- `protected` class, package, subclass   
- default or no value, class, pacakge   
   
Once a data is `private` will have to use a setter function to work with that value or a getter function to get that value.(when working outside the class), it will not be "visible" to any other classes   
   
The setter function will usually be visible(default or public) so you can play with the private value indirectly, making it secure.   
   
As industry standard, when defining data in classes, they should be made private and their getter and setter methods should be generated(even if they don't do anything with the data), <span class="underline">methods as public and data as private</span>   
   
We can also use constructors for setting values instead of using a setter function.   
   
### [OOPS project with Java](https://github.com/zubayrrr/java_oops_project)   
   
   
---   
   
   
- Inhertitance   
- Overriding   
- Abstract classes   
- Interfaces   
- `super` keyword   
- static   
   
   
---   
   
### Inheritance   
   
When a class(subclass) acquires the properties of another class(called as base class, parent class, super class)   
   
    public class newClass extends oldClass{   
        // all the data except private from oldClass will be made available for newClass when compling(?)   
    }   
   
### Overriding   
   
When a method in the subclass has the same signature(signature really means the method name and the passing arguments) as a method in the super class, then the subclass method takes precendece.   
   
### Abstract classes   
   
Class which has empty methods and fully defined methods   
   
    public abstract class Container{   
        public void calculateVolume(int length, int height){   
            double volume = calculateAreaOfBase(length) * height;   
            System.out.println("Volume = " + volume);   
        }   
   
        public abstract double calculateAreaOfBase(int length);   
    }   
   
   
    // //   
   
    public class SquareContainer extends Container{   
        // you'll be prompted to add unimplemented methods   
   
        public double calculateAreaOfBase(int length){   
            // actual code that you will be using to calcuate area of base of a square   
            double area = length * length;   
            System.out.println("square Area = " + area );   
            return area;   
        }   
    }   
   
    // //   
   
    public class circleContainer extends Container{   
   
        public double calculateAreaOfBase(int length){   
            double area = Math.PI * (length/2)*(length/2);   
            System.out.println("Circle Area = " + area );   
            return area;   
        }   
    }   
   
    // finally, these abstract methods can be used such as   
   
    public class TestContainer{   
        public static void main(String[] args) {   
            CircleContainer c1 = new CircleContainer();   
            c1.calculateVolume(10, 5);   
   
            // you can also use super class when initializing objects   
            // superClass obj = new subClass();   
   
            // Container c1 = new CircleContainer();   
            // which can be further used   
            // c1 = new SquareContainer();   
   
            SquareContainer s1 = new SquareContainer();   
            s1.calculateVolume(10, 5);   
        }   
    }   
   
Reusing Objects   
   
    class A {   
   
    }   
   
    class B extends A {   
   
    }   
   
    A obj = new A();   
    B obj = new B();   
    A obj = new B();   
    B obj = new A(); <--- this cannot be done   
   
### Interface   
   
A class with only empty methods. A class `implements` an interface. An interface will hold names for methods. which can be implemented further in a class. If a method is unimplemented it can be written (override) inside the class itself. A class can only extend one class but multiple interfaces can be implemented by a class.   
\!\!\! `super` keyword   
   
Is used to access a super class's data and methods.   
When using a super class's method inside a sub class, append the `super` keyword before the method call to access it.   
   
### `static` keyword   
   
Data that is one per class not one per object, you can also have static blocks of code. static block of code is run even before the constructor runs.   
For every object created, constructor is run but static block of code is only fired once. static methods/data can be called by their class names directly. Non static methods/data cannot be called directly from the class.   
   
static variables can be called from objects but they are "static", different objects don't have different static variables, only one static variable exists.   
   
### main method   
   
Is entry point for execution, it is defined as static and public, it also returns void, because everything will be utilized inside the method itself. main is declared as static to avoid creation of instances of main methods. There can only ever be one `main`.   
   
   
---   
   
## Collections   
   
   
- List   
- ArrayList   
- HashMap   
- generics   
   
### ArrayList   
   
Arrays are of fixed length. Array list is one of the collections, brought about to overcome the disadvantage of using Arrays.   
   
    `import java.util.ArrayList;`   
   
    `ArrayList list = new ArrayList();`   
    // List list = new ArrayList();   
    // List is the super class of ArrayList   
   
   
    // non generic list, anything can be added   
    list.add("zero");   
    list.add("one");   
    list.add(2);   
    list.add(true);   
   
    for(Object temp: list){   
        System.out.println(temp);   
    }   
   
    // generic list, add specific elements   
   
    List<String> stringList = new ArrayList<String>();   
    // with java 7, you can new ArrayList<>(); using the diamon operator   
    // this ArrayList is limited to strings only   
   
    stringList.add('wow');   
   
    for(String temp: stringList){   
        System.out.println(temp);   
    }   
   
<span class="underline">All classes extend the Object class</span>   
   
Object obj = new A();   
Object obj2 = new Integer();   
Object obj3 = new String();   
   
    public class ClassName extends Object{   
        // data and methods   
    }   
   
### Hashmap   
   
Is used to store `("key", value)` pairs. Since you have a key   
   
    import java.util.HashMap;   
   
    HashMap hm = new HashMap();   
   
    hm.put("wow", 69);   
   
    System.out.println(hm.get("wow"))   
   
    // to make it generic   
   
    HashMap<String, Double> hm2 = new HashMap<>();   
   
   
- Linked List   
- Sets   
   
   
---   
   
### UML class diagram   
   
Unified Modeling Language   
   
Representing classes that we create using UML   
   
It must contain three boxes:   
   
   
- First box will represent class name   
- Second box will represent the data of the classes   
   
Example UML diagram   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.atut4xg4mxv.png)   
   
   
- `-` for private   
- `+` for public   
- `#` for protected   
- `~` default   
   
   
---   
   
### Error/Exception Handling   
   
   
- try   
- catch   
- finally   
   
Whenever you feel like a block of code might break because of input data, use a `try` `catch` block and use the exception object to read the error/exception message.   
   
You can use methods on the exception object to get more info such as `e.printStack()`   
   
    int d[] = new int[3];   
    int a = 10;   
    int b = 1;   
    int c = 0;   
   
    try{   
        d[1] = 10;   
        c = a/b;   
    }catch(Exception e){   
        System.out.println("Exception occured " + e);   
        e.printStackTrace();   
    }   
   
You can also use multiple `catch` statements for different kind of exceptions.   
   
````java
try {
    d[1] = 10;
    c = a / b;
} catch (ArrayIndexOutOfBoundsException | ArithmeticException e) {
    System.out.println("Defined exceptions occured " + e);
} catch (Exception e) {
    System.out.println("Generic exceptions " + e);
} finally {
    System.out.println("Will always run");
} // if there is an exception, the exception will run, if there arent any, finally will run anyway EVEN if there is a return right after the try block. ```!!! throw and throws !!! variable arguments !!!`final`keyword`final`keyword can be applied to data, methods and classes,`final`data s a constant, cannot be changed.`final`methods cannot be overriden,`final`classes cannot be sub classed. !!!`.jar`files is like zipping them, in java world`.jar`files contains bunch of java programs that can be created from IDE. More options can be found on the IDE when exporting. They can also be used for importing them on your IDE.
````
