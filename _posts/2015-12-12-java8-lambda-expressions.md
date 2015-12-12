---
layout: post
category : lessons
tags : [lambda, java8, java]
---
{% include JB/setup %}

###Lambda Expressions =
<p>The lambda expressions allows us to pass logic in a compact way.</p>
<p>Lambda expressions are used primarily to define inline implementation of a functional interface, i.e., an interface with a single method only.</p>

**Syntax**
<p>A lambda expression describes an anonymous function. Like a function it has a parameter list and a body. A lambda expression consists of a parameter list, the arrow symbol "->", and a body.</p>

{% highlight java %}
parameter -> expression body

    LambdaExpression: 
        LambdaParameters '->' LambdaBody 

    LambdaParameters: 
        Identifier 
        '(' ParameterList ')' 
    LambdaBody: 
        Expression 
        Block 
{% endhighlight %}

###Important characteristics of a lambda expression =
- <strong>Optional type declaration −</strong> No need to declare the type of a parameter. The compiler can inference the same from the value of the parameter.
- <strong>Optional parenthesis around parameter −</strong> No need to declare a single parameter in parenthesis. For multiple parameters, parentheses are required.
- <strong>Optional curly braces −</strong> No need to use curly braces in expression body if the body contains a single statement.
- <strong>Optional return keyword −</strong> The compiler automatically returns the value if the body has a single expression to return the value. Curly braces are required to indicate that expression returns a value.

<p>Lambdas look similar to methods. The difference is that they do not have a name and neither the return type nor the throws clause is declared. Both are automatically inferred by the compiler.</p>

###Difference between Anonymous class and Lambda expression =
<p>One key difference between using Anonymous class and Lambda expression is the use of ‘this’ keyword. For anonymous class <strong>‘this’</strong> keyword resolves to anonymous class, whereas for lambda expression ‘this’ keyword resolves to enclosing class where lambda is written.</p>

<p>Another difference between lambda expression and anonymous class is in the way these two are compiled. Java compiler compiles lambda expressions and convert them into private method of the class. It uses <strong>invokedynamic</strong> instruction that was added in Java 7 to bind this method dynamically.</p>

{% highlight java %}
    ExInterface exInterface1 = new ExInterface() {
        @Override
        public void sayHello() {
            System.out.println("In main hello");
        }
    };
{% endhighlight %}

<p>Using lambda we can write in single line.</p>

{% highlight java %}
    ExInterface exInterface1 = () -> System.out.println("In main hello");
{% endhighlight %}

<p>Instead of passing in an inner class that implements an interface, we're passing in a block of code.</p>
<p>Nothing passed in a parameter,</p>
<p>-> separates the parameter from the body of the lambda expression.</p>
<p>In the lambda expression the parameter is empty. javac is inferring the type from its context, the signature of exInterface1.</p>
<p>We don't need to explicitly write out the type when it's obvious. The lambda method parameters are still <strong>statically typed.</strong></p>


###Body =
<p>The lambda body can be a block of one or more statements. It can also be as simple as a plain expression.</p>

{% highlight java %}
    lambda expression: () -> System.gc() 	
        equivalent method: void nn() { System.gc(); } 

        (int x) -> x+1 	
        equivalent method: int nn(int x) { return x+1; } 

        (int x, int y) -> x+y 
        equivalent method: int nn(int x, int y) { return x+y; } 

        (String... args) -> args.length 
        equivalent method: int nn(String... args) { return args.length; } 

        (String[] args) -> (args!=null)? args.length : 0 
        equivalent method: int nn(String[] args) { return (args != null) ? args.length: 0; } 

        (Future f) -> f.get() 
        equivalent method: Long nn(Future f) throws ExecutionException, InterruptedException { return f.get(); }

        (int x) -> { return x+1; } 	//fine
        (int x) -> return x+1 	//error: not a statement The return keyword can only appear in a statement and statements must be terminated by a semicolon. 
        (int x) -> return x+1; 	//error: illegal start of expression A statement can only appear in a block, i.e. the statement must be enclosed in curly braces.
{% endhighlight %}

###Parameter List =
<p>There are a couple of variations of the parameter list. The parameter types of a lambda expression may either all be declared or all inferred. The inferred types are derived from the context in which the lambda expression appears.</p>

###Single Parameter with Inferred Type =
<p>If the parameter list consists of exactly one parameter then it can be reduced to an identifier, i.e. the name of the parameter.</p>
{% highlight java %}
    args -> args.length 	//fine 
        f -> { return f.get(); } 	//fine 
        f -> f.get() 	//fine 
{% endhighlight %}

###Multiple Parameters with Inferred Types =
<p>The enclosing parentheses are mandatory. The declared type can only be omitted when the compiler can infer the parameter type from the context in which the lambda expression appears.</p>
{% highlight java %}
    x -> x+1 	//fine (because there is only one parameter) 
        (x) -> x+1 	//fine 
        (int x) -> x+1 	//fine 
        int x -> x+1 	//error: illegal If the parameter type is specified then the enclosing parenthesis are mandatory 
        (int x,int y) -> x+y 	//fine 
        int x,int y -> x+y 	//error: illegal If the parameter type is specified then the enclosing parenthesis are mandatory.
        (x,y) -> x+y 	//fine 
        x,y -> x+y 	//error: illegal If there is more than one parameter then the enclosing parenthesis are mandatory.
{% endhighlight %}

###Regular Parameters with Declared Types =
<p>The enclosing parentheses are mandatory. The parameter list can be empty, in which case it consist of empty brackets. It can contain one or more parameters with a declared type. If one parameter has a declared type, then all parameters must have a declared type. Mixing inferred and declared types is illegal. The declared type can have modifiers like final for instance. The last parameter may be a variable parameter, also know as "varargs" parameter like String... for instance.</p>
{% highlight java %}
    () -> 42 fine 
        (String fmt, Object... args) -> String.format(fmt,args) 	//fine 
        (int x, y) -> x+y 	//error: illegal Mixing inferred and explicit parameter types is illegal. 
        (final int x) -> x+1 	//fine 
        (final x) -> x+1 	//error: illegal Only explicit parameter types can have modifiers.
{% endhighlight %}

###Return Type and Throws Clause =
<p>Different from a method a lambda expression does neither declare a return type nor a throws clause. Both the lambda's return type and its throws clause are always automatically inferred by the compiler from the context in which the lambda expression appears.</p>



