---
layout: post
category : lessons
tags : [multiple defaults, java8, java]
---
{% include JB/setup %}

###Multiple Defaults =
<p>The main reason to introduce default methods is that if at some point we need to add a method to an existing interface, we can add a method without changing the existing implementation classes. To support lambda expressions in collections API and to enhance.In this way, the interface is still compatible with older versions.</p>


- Before Java 8 in interfaces we are able to declare only abstract methods.
- If we declare a method without abstract that will be treated as abstract by default.
- These methods won't have body means implementations.
- The class which is implementing this interface need to provide body / implementation for this abstract methods.
- Now with java 8 default methods we can add methods to interface without disturbing existing functionality.
- So instead of overriding now we can inherit these default methods from interfaces.
- Can we override java 8 default method.
- Defaults methods are also  known as defender methods or virtual extension methods.


<p>With default functions in interfaces, there is a possibility that a class is implementing two interfaces with same default methods.</p>

{% highlight java %}
public interface EducationalBook {
   default void print(){
      System.out.println("I am reading an Educational Book!");
   }
}

public interface ComicBook {
   default void print(){
      System.out.println("I am reading a Comic Book!");
   }
}
{% endhighlight %}


**There are two Solutions for that -**
<p>1. First solution is to <strong>create an own method</strong> that overrides the default implementation.</p>
{% highlight java %}
public class Book implements EducationalBook, ComicBook {
   void print(){			
      System.out.println("I read books like Educational books and Comic books!");
   }
}
{% endhighlight %}

<p>2. Second solution is to call the default method of the specified interface using <strong>super.</strong></p>
{% highlight java %}
public class Book implements EducationalBook, ComicBook {
   void print(){
      EducationalBook.super.print();
      ComicBook.super.print();
   }
}
{% endhighlight %}


<p><strong>Example -</strong></p>
<p>In interface EducationalBook.java</p>
{% highlight java %}
public interface EducationalBook {
    default void read(){
        System.out.println("I am reading an Educational Book!");
    }
}
{% endhighlight %}

<p>In interface ComicBook.java</p>
{% highlight java %}
public interface ComicBook {
    default void read(){
        System.out.println("I am reading a Comic Book!");
    }
}
{% endhighlight %}

<p>In Class Book.java which implements multiple interfaces EducationalBook, ComicBook.</p>
{% highlight java %}
public class Book implements EducationalBook, ComicBook {

    @Override
    public void read() {
        System.out.println("I read books like Educational books and Comic books!");
        EducationalBook.super.read();
        ComicBook.super.read();
    }

    public static void main(String args[]){
        Book book = new Book();
        book.read();
    }
}
{% endhighlight %}

<p><strong>Output</strong></p>
{% highlight java %}
I read books like Educational books and Comic books!
I am reading an Educational Book!
I am reading a Comic Book!
{% endhighlight %}


