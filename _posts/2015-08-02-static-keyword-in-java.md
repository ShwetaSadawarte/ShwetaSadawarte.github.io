---
layout: post
category : lessons
tags : [static keyword, static block, static variable, static method, java]
---
{% include JB/setup %}

Static keyword can be used with variables, methods and blocks. 

###Static variables -
Static variables are created only once and they exist even if we do not have any object. But Object variables get created for each object separately.
Variables defined by using static keyword are named as **“class variables”**. This variables hold values related to a class, and they occupy space in memory even if there is no existing object created from that class. 
There is only one instance of a class variable no matter how many objects are created.

###Static block -
Static block is executed before main method executes i.e. before an object created for that class.
Static block is useful to check conditions before execution of main begin.
Static blocks also called as **“static initializers”** are used for assigning initial values to static variables. 
Static blocks are executed right after static variables are loaded into the memory.
We cannot access non-static elements inside static code blocks.

{% highlight java %}
class StaticBlock {
  public static void main(String[] args) {
    System.out.println("In Main method.”);
  }
 
  static {
    System.out.println("In Static block.It is executed before main method.");
  }
}

{% endhighlight %}

###Static methods -
Static methods in Java can be called without creating an object of class. main method is static  because program execution begins from main and no object has been created yet. 

{% highlight java %}
class Languages {
  public static void main(String[] args) {
    display();
  }
 
  static void display() {
    System.out.println("In static method.");
  }
}
{% endhighlight %}

Instance method requires an object of its class to be created before it can be called while static method doesn't require object creation.
We cannot reference to a non-static element within a static method.
We cannot invoke non-static methods within static methods.

###Static Import
In Java, Math class in java.lang package is full of static methods and we need to invoke these methods using Math.nameOfMethod(). Using static import we can invoke them by using method name only. 

{% highlight java %}
import static java.lang.Math.*;

public class Program {
    public static void main(String args[]) {
        System.out.println("Square root 25: " + sqrt(25));
        System.out.println("Value of Pi: " + PI);
    }
}
{% endhighlight %}

We can reference static methods and variables without using the class name. Normally we would use Math.sqrt() and Math.PI if we did not have static import.

###public static void main(String args[])
Main method has to be public and static. It has to be public because JVM needs to be able invoke it from outside. It also has to be static because JVM does not instantiate the class where main method resides. To invoke a method without creating an object, method has to be defined static.

