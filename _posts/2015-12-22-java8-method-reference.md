---
layout: post
category : lessons
tags : [Method Reference, java8, java]
---
{% include JB/setup %}

###Method Reference =
<p>Method references help to point to methods by their names. A method reference is described using <strong>:: (double colon)</strong> symbol.</p>
<p>Some times, A lambda expression do nothing but just calls a method which is already defined.
To be more lazy to write, You can use method references.
Method references are just compact and more readable form of a lambda expression for already written methods.</p>
<p>A method reference can be used to point the following types of methods −</p>
- Static methods
- Instance method of a particular object
- Instance method of an arbitrary object of a particular type
- Constructors using new operator (TreeSet::new)


<p><strong>Example (as a static method reference)</strong></p>
{% highlight java %}
    import java.util.List;
    import java.util.ArrayList;

    public class StaticRef {

        public static void main(String[] args) {
            List vehicles = new ArrayList<>();
            vehicles.add("Car");
            vehicles.add("Bicycle");
            vehicles.add("Scooter");
            vehicles.add("Bus");
            vehicles.add("Train");

            vehicles.forEach(System.out::println);
        }
    }
{% endhighlight %}

<p><strong>Output</strong></p>
{% highlight java %}
    Car
    Bicycle
    Scooter
    Bus
    Train
{% endhighlight %}


<p><strong>Example (as a reference to an instance method of a particular object)</strong></p>
{% highlight java %}
    class ComparisonProvider {
        public int compareByBrand(Mobile a, Mobile b) {
            return a.getName().compareTo(b.getName());
        }
            
        public int compareByPrice(Mobile a, Mobile b) {
            return a.getBirthday().compareTo(b.getBirthday());
        }
    }

    ComparisonProvider myComparisonProvider = new ComparisonProvider();
    Arrays.sort(rosterAsArray, myComparisonProvider::compareByBrand);
{% endhighlight %}

<p>The method reference myComparisonProvider::compareByBrand invokes the method compareByBrand that is part of the object myComparisonProvider. The JRE infers the method type arguments, which in this case are (Mobile, Mobile).</p>

<p><strong>Example (as a reference to an instance method of an arbitrary object of a particular type)</p></strong>
{% highlight java %}
    String[] stringArray = { "Shweta", "Smith", "Abhi", "John", "Siya" };
    Arrays.sort(stringArray, String::compareToIgnoreCase);
{% endhighlight %}


<p>The equivalent lambda expression for the method reference String::compareToIgnoreCase would have the formal parameter list (String a, String b), where a and b are arbitrary names used to better describe this example. The method reference would invoke the method a.compareToIgnoreCase(b).</p>

<p><strong>Example (as a constructor)</p></strong>
{% highlight java %}
    public class ReferenceToConstructor {
        
        public static void main(String[] args) {
            List  numbers = Arrays.asList(4,9,16,25,36);
            List squaredNumbers = ReferenceToConstructor.findSquareRoot(numbers,Double::new); 
            
            //In lambda List squaredNumbers = ReferenceToConstructor.findSquareRoot(numbers, x -> new Double(x));
            System.out.println("Square root of numbers = "+squaredNumbers);
        }
    
        private static List findSquareRoot(List list, Function<double,double> f){
            List result = new ArrayList();
            list.forEach(x -> result.add(f.apply(Math.sqrt(x))));
            return result;
        }
    }    
{% endhighlight %}


<p><strong>Example</strong></p>
{% highlight java %}
    interface IsReferable {
        public void referenceDemo();
    }
    class ReferenceDemo {
        public static void commonMethod() {
            System.out.println("This method is already defined.");
    }
    public void implement() {
        // Anonymous class.
        IsReferable demoOne = new IsReferable() {
            @Override
            public void referenceDemo() {
                ReferenceDemo.commonMethod();
            }
        };
        demoOne.referenceDemo();
        
        // Lambda implementaion.
            IsReferable demo = () -> ReferenceDemo.commonMethod();
            demo.referenceDemo();
            
        // Method reference.
            IsReferable demoTwo = ReferenceDemo::commonMethod;
            demoTwo.referenceDemo();
    }
    }
{% endhighlight %}


###Q. When to use method reference.
<p>When a Lambda expression is invoking already defined method, you can replace it with reference to that method.</p>

###Q. When you can not use Method reference.
<p>You can not pass arguments to the method reference.</p>
<p>Example, you can not use method reference for following lambda.</p>
{% highlight java %}
    IsReferable demo = () -> ReferenceDemo.commonMethod("Argument in method."); 
{% endhighlight %}
<p>Because Java does not support <strong>currying</strong> without Wrapper methods or Lambda.</p>




