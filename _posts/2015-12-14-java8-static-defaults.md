---
layout: post
category : lessons
tags : [Static defaults, java8, java]
---
{% include JB/setup %}

###Static Default Methods =
- An interface can also have static helper methods from Java 8 onwards.
- A class is implementing two interfaces with same static methods. i.e. You may add a method with the same signature in an implementing class, you’re not truly overriding the static interface method. 
- Being a static method you do not need object reference to call that method.
- The static method can only be called through the interface or class type reference, not on instance.
EducationalBook.readingStories();
ComicBook.readingStories();


<p><strong>Example -</strong></p>
<p>In interface EducationalBook.java</p>
{% highlight java %}
public interface EducationalBook {
   static void readingStories(){
        System.out.println("Reading Stories in Educational books!!!");
    }
}
{% endhighlight %}

<p>In interface ComicBook.java</p>
{% highlight java %}
public interface ComicBook {
   static void readingStories(){
        System.out.println("Reading Stories in comic book!!!");
    }
}
{% endhighlight %}

<p>In Class Book.java which implements multiple interfaces EducationalBook, ComicBook.</p>
{% highlight java %}
public class Book implements EducationalBook, ComicBook {

    public static void main(String args[]){
        EducationalBook.readingStories();
        ComicBook.readingStories();
    }
}
{% endhighlight %}

<p><strong>Output</strong></p>
{% highlight java %}
Reading Stories in Educational books!!!
Reading Stories in comic book!!!
{% endhighlight %}


<p><strong>Example -</strong>Combining Multiple inheritance having Multiple Default method & Static Default method</p>
<p>In interface EducationalBook.java</p>
{% highlight java %}
public interface EducationalBook {
    default void read(){
        System.out.println("I am reading an Educational Book!");
    }

    static void readingStories(){
        System.out.println("Reading Stories in Educational books!!!");
    }
}
{% endhighlight %}

<p>In interface ComicBook.java</p>
{% highlight java %}
public interface ComicBook {
    default void read(){
        System.out.println("I am reading a Comic Book!");
    }

    static void readingStories(){
        System.out.println("Reading Stories in comic book!!!");
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
        EducationalBook.readingStories();
        ComicBook.readingStories();
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
Reading Stories in Educational books!!!
Reading Stories in comic book!!!
{% endhighlight %}
