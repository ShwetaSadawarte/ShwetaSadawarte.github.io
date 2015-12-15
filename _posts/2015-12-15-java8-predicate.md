---
layout: post
category : lessons
tags : [Predicate, java8, java]
---
{% include JB/setup %}

###Predicate
<p>In mathematics, a predicate is commonly understood to be a Boolean-valued function P: X? {true, false}, called the predicate on X. Informally, a predicate is a statement that may be true or false depending on the values of its variables. It can be thought of as an operator or function that returns a value that is either true or false.</p>

<p><strong>Interface Predicate&#60;T&#62;</strong></p>
{% highlight java %}
Type Parameters:
    T - the type of the input to the predicate.
{% endhighlight %}

<p><strong>Functional Interface:</strong></p>
<p>This is a functional interface and can therefore be used as the assignment target for a lambda expression or method reference.</p>

<p><strong>@FunctionalInterface</strong></p>
<p>public interface <strong>Predicate&#60;T&#62;</strong></p>
<p>Represents a predicate (boolean-valued function) of one argument.
This is a functional interface whose functional method is test(Object).</p>

<p>Predicate can be used to evaluate a condition on group/collection of similar objects such that evaluation can result either in true or false.</p>

<p><strong>Method true =</strong></p>
boolean test(T t)
    Evaluates this predicate on the given argument.
Parameters:
    t - the input argument
Returns:
    true if the input argument matches the predicate, otherwise false


<p><strong>Example =</strong></p>
{% highlight java %}
    public class Main {

        public static void main(String[] args) {
            Predicate<String> i  = (s)-> s.length() > 5;

            System.out.println(i.test("Hi!! How are you?"));
        }
    }
{% endhighlight %}

<p><strong>Output</strong></p>
true
