---
layout: post
category : lessons
tags : [Optional, java8, java]
---
{% include JB/setup %}

###Optional class =
<p>Optional is a <strong>container object</strong> which is used to contain not-null objects. Optional object is used to represent null with absent value. This class has various utility methods to facilitate code to handle values as ‘available’ or ‘not available’ instead of checking null values.</p>
<p>As a java programmer you have seen null pointer exception many times.</p>
<p>Java SE 8 introduces a new class called <strong>java.util.Optional</strong> that solves some of the problems caused by the null reference.</p>

{% highlight java %}
Class Optional<T>
    java.lang.Object
{% endhighlight %}

<p>Declaration for <strong>java.util.Optional&#60;T&#62;</strong> class</p>

{% highlight java %}
public final class Optional<T>
    extends Object
{% endhighlight %}

<p>This class inherits methods from the java.lang.Object class.</p>

<p>A container object which may or may not contain a non-null value. If a value is present, <strong>isPresent()</strong> will return true and get() will return the value.
Additional methods that depend on the presence or absence of a contained value are provided, such as <strong>orElse()</strong> (return a default value if value not present) and <strong>ifPresent()</strong> (execute a block of code if the value is present).</p>

<p>This is a <strong>value-based class</strong>; use of identity-sensitive operations (including reference equality (==), identity hash code, or synchronization) on instances of Optional may have unpredictable results and should be avoided.</p>

**Example -**
{% highlight java %}
import java.util.Optional;

public class OptionalExample {
   public static void main(String args[]){

    OptionalExample optionalExample = new OptionalExample();
    Integer value1 = null;
    Integer value2 = new Integer(15);
            
    //Optional.ofNullable - allows passed parameter to be null.
    Optional<Integer> a = Optional.ofNullable(value1);
            
    //Optional.of - throws NullPointerException if passed parameter is null
    Optional<Integer> b = Optional.of(value2);
    System.out.println(optionalExample.sum(a,b));
   }
	
   public Integer sum(Optional<Integer> a, Optional<Integer> b){
	
      //Optional.isPresent - checks the value is present or not
		
      System.out.println("First parameter is present: " + a.isPresent());
      System.out.println("Second parameter is present: " + b.isPresent());
		
      //Optional.orElse - returns the value if present otherwise returns the default value passed.
      Integer value1 = a.orElse(new Integer(0));
		
      //Optional.get - gets the value, value should be present
      Integer value2 = b.get();
      return value1 + value2;
   }
}
{% endhighlight %}

<p><strong>Output</strong></p>
<p>First parameter is present: false</p>
<p>Second parameter is present: true</p>
<p>15</p>



