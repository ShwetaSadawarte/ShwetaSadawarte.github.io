---
layout: post
category : lessons
tags : [default methods, java8, java]
---
{% include JB/setup %}

###Default Methods =
<p>The main reason to introduce default methods is that if at some point we need to add a method to an existing interface, we can add a method without changing the existing implementation classes. To support lambda expressions in collections API and to enhance.In this way, the interface is still compatible with older versions.</p>

- Before Java 8 in interfaces we are able to declare only abstract methods.
- If we declare a method without abstract that will be treated as abstract by default.
- These methods won't have body means implementations.
- The class which is implementing this interface need to provide body / implementation for this abstract methods.
- Now with java 8 default methods we can add methods to interface without disturbing existing functionality.
- So instead of overriding now we can inherit these default methods from interfaces.
- We can override java 8 default method.
- Defaults methods are also  known as defender methods or virtual extension methods.


<p><strong>Example -</strong></p>
<p>In interface MyInterface.java</p>
{% highlight java %}
public interface MyInterface {
    String text = "Hello";

    void sayHello();
    default void saySomething() {
        System.out.println("In MyInterface");
    }
}
{% endhighlight %}


<p>In class MyInterfaceImpl.java</p>
{% highlight java %}
public class MyInterfaceImpl implements MyInterface{

    @Override
    public void sayHello() {
        System.out.println(MyInterface.text);
    }

    public static void main(String[] args) {
        MyInterfaceImpl myInterfaceImpl = new MyInterfaceImpl();
        myInterfaceImpl.sayHello();         // calling implemented method
        myInterfaceImpl.saySomething();     // calling inherited method

        MyInterface myInterface = new MyInterfaceImpl();
        myInterface.saySomething();         // calling using interface name
    }
}
{% endhighlight %}

<p><strong>Output</strong></p>
{% highlight java %}
Hello
In MyInterface
In MyInterface
{% endhighlight %}

###Multiple Defaults
[Multiple Defaults](http://shwetasadawarte.github.io/lessons/2015/12/14/java8-multiple-defaults/) 

###Static Defaults
[Static Defaults](http://shwetasadawarte.github.io/lessons/2015/12/14/java8-static-defaults/)