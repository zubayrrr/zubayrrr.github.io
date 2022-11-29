---
created: 20211111172236788
desc: ''
id: caqic1zdwxl1ll1ogg1ec1f
tags:
- now
title: Scala
updated: 1652622344307
---
   
Creating a variable   
   
`var num : Int = 8;`   
   
   
- where `Int` is a class, `num` is an object and `8` is also an object, `;` semi colons are optional.   
   
Don't create a variable that is sharing and changing at the same time.   
   
Scala believes in concurrency, to achieve concurrency, immutability, like `final` in [Java](../devlog/java.md), we have `val` in Scala.   
   
You can change value of `var` but cannot change value of `val`.   
   
We use operator overloading in Scala since its (also) a functional programming language.   
   
When we do `8 + 7` we're really doing `8.+(7)`   
   
`var result = 8.+(7)` the `+` operator is not really an operator its a function/method   
   
To create a class   
   
    case class Student(var rollno: Int, var name : String, var marks : Int)   
    // dont need a separate constructor   
    // for assigning defaults, just proceed with giving values for the variables that were defined, you can also do constructor overloading   
   
    var s1 = Student(4) //> s1 : Demo.Student = Student(4, defaultValue, defaultValue)   
   
    // when the passed value doesn't match the first variable Scala was expecting, it'll throw an error to explicitly define it   
   
    var s1 = Student(name = "Somevalue")   
   
### Method calls   
   
    case class Student(var rollno: Int = 1, var name : String = "This String", var marks : Int = 100)   
    {   
        def show() = println("Hello There!") // use {} if your method is larger than 1 line   
    }   
   
    var s1 = Student(name = "New String");   
   
    // to call a method   
   
    s1.show()   
   
### Comparing two objects and function overloading   
   
    case class Student(var rollno: Int = 1, var name : String = "This String", var marks : Int = 100)   
    {   
        def show() = println("Hello There!") // use {} if your method is larger than 1 line   
   
        def >(s2 : Student) : Boolean = marks > s2.marks   
    }   
   
    var s1 = Student();   
    var s2 = Student(2, "Bro", 98)   
   
    s1.>(s2)   
   
### lists and lambda expression   
   
    var nums = List(4, 7, 3, 9)   
   
    // Looping over a list   
   
    for(n <- nums)   
    {   
        println(n)   
    }   
   
    // Lambda Expression   
   
    nums.foreach {i:Int => println(i)}   
   
### List Reverse, Drop and Take   
   
`num.reverse //> List[Int] = List(3, 2, 7, 4)` instead of mutating the existing `num` list, it creates a new list.   
   
to remove elements   
   
`nums.drop(2)` removes first 2 elements   
   
`nums.drop(2).take(2)` removes first 2 and prints next 2, even now it is creating a new list and not working on the existing list   
   
to remove syntatic sugar, `nums drop 2`   
   
### Type hierarchy   
   
List of AnyVal   
   
`var a_list = List(4, 7, true)`   
   
![](https://raw.githubusercontent.com/zubayrrr/twiki/main/bin/image.isoerzqte2n.png)   
   
List of "Any"   
   
`var b_list = List(4,6,true, "String")`   
   
### List of complex objects   
   
```
case class Stud(rollno: Int, name: String, marks: Int)

val students = List(Stud(1, "Student1", 40), Stud(2, "Student2", 80))

// you can use tail head just like in java

var first = students.head

val rest = students.tail.head // or students.tail.tail etc

val toppers = students.filter(s => s.marks>=60)

val parts = students.parition(s => s.marks<=60) // returns tuples

// tuples

val part1 = parts._1
val part2 = parts._2

val (part1, part2) = students.parition(s => s.marks<=60) // returns tuples

```
   
   
### Expressions   
   
`val anIfExpression = if(2 > 3) "bigger" else "smaller"`   
   
### Instructions VS Expressions   
   
Instructions are the building blocks of imperative programms, executed one by one, a program hence a sequence of instructions.   
   
Expressions are evaluated, reduced to a single value.   
   
Instructions like expressions in Scala are denoted by the type Unit   
   
`val theUnit = println("Hello, Scala")` _Unit, no meaningful value, = void_   
   
### Functions   
   
    def myFunc(param: Int) = 42   
   
### OOP   
   
OOP in Scala is done using Single Class Inheritance   
   
    class Animal   
    class Dog extends Animal   
    // interface   
    trait carivore {   
        // we can define abstracts here   
        def eat(animal: Animal): Unit   
    }   
   
    class Crocodile extends Animal with Carnivore {   
        override def eat(animal: Animal): Unit = println("Crunch!")   
    }   
   
    // singleton object/pattern   
   
    object MySingleton{   
        // we've defined both the Type MySingleton as well as the single Instance the Type can have   
        // additional implementation   
    }   
   
    // companions   
    if you have a class/trait and singleton with the same name in the same file, they're called companions, companions have special features   
   
    object Carinvore{   
        // implementation   
    }   
   
    // generics   
    trait MyList[A]   
    trait MyList[A] // Covariance   
   
    // method notation   
   
    val x = 1 + 2   
    val y = 1.+(2)