---
layout: post
category : lessons
tags : [Stream, parallelStream, filter, map, Collector, toList, java8, java]
---
{% include JB/setup %}

###Stream =
##Q. What is stream? Interface or class?
<p>A stream is a sequence of data.</p>
<p>A program uses an input stream to read data from a source, one item at a time.A program uses an output stream to write data to a destination, one item at time.
All Java streams are derived from Input Stream ( java.io.InputStream ) and Output Stream ( java.io.OutputStream ) classes.
The System.in is the input stream class derivative and analogically System.out is the output counterpart.</p> 

<p>They are <strong>abstract base classes</strong> meant for other stream classes.</p> 
<p>Streams support many different kinds of data, including simple bytes, primitive data types, localized characters, and objects. Some streams simply pass on data; others manipulate and transform the data in useful ways.</p> 


##Generating Streams
<p>With Java 8, Collection interface has two methods to generate a Stream</p>
- <strong>stream() −</strong> Returns a sequential stream considering collection as its source.
- <strong>parallelStream() −</strong> Returns a parallel Stream considering collection as its source.

##Using stream() =
{% highlight java %}
public class StreamBuilders {
     public static void main(String[] args){
         List<Integer> list = new ArrayList<Integer>();
         for(int i = 1; i< 10; i++){
             list.add(i);
         }
         Stream<Integer> stream = list.stream();
         List<Integer> evenNumbersList = stream.filter(i -> i%2 == 0).collect(Collectors.toList());
         System.out.print(evenNumbersList);
     }
}
{% endhighlight %}


##Using parallelStream() =
{% highlight java %}
public class StreamBuilders {
     public static void main(String[] args){
        List<Integer> list = new ArrayList<Integer>();
         for(int i = 1; i< 10; i++){
             list.add(i);
         }
         //Here creating a parallel stream
         Stream<Integer> stream = list.parallelStream(); 
         Integer[] evenNumbersArr = stream.filter(i -> i%2 == 0).toArray(Integer[]::new);
         System.out.print(evenNumbersArr);
     }
}
{% endhighlight %}


##Q. What is parallelism.
<p>To enable parallelism, all you have to do is to create a parallel stream, instead of sequential stream. Anytime you want to particular job using multiple threads in parallel cores, all you have to do is call method <strong>parallelStream()</strong> method instead of stream() method.</p>
<p>A key driver for this work is making parallelism more accessible to developers. While the Java platform provides strong support for concurrency and parallelism already, developers face unnecessary impediments in migrating their code from sequential to parallel as needed. Therefore, it is important to encourage idioms that are both sequential- and parallel-friendly. This is facilitated by shifting the focus towards describing what computation should be performed, rather than how it should be performed. It is also important to strike the balance between making parallelism easier but not going so far as to make it invisible. Making parallelism transparent would introduce non-determinism and the possibility of data races where users might not expect it.</p>


##Example -
{% highlight java %}
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class StreamExample {

    public static void main(String[] args) {
        List<String> items = new ArrayList<>();
        items.add("One");
        items.add("Two");
        items.add("Three");

        Stream<String> stream = items.stream();
        List<String> filtered = items.stream()
                .filter(item -> item.startsWith("O"))
                .collect(Collectors.toList());
        System.out.println(filtered);
        List<String> map = items.stream()
                .map(item -> item.toUpperCase())
                .collect(Collectors.toList());
        System.out.println(map);
        String shortest = items.stream()
                .min(Comparator.comparing(item -> item.length()))
                .get();
        System.out.println(shortest);
        String longest = items.stream()
                .max(Comparator.comparing(item -> item.length()))
                .get();
        System.out.println(longest);
        long count = items.stream()
                .filter(item -> item.startsWith("T"))
                .count();
        System.out.println(count);
        String reduced = items.stream()
                .reduce((acc, item) -> acc + " " + item)
                .get();
        System.out.println(reduced);
        String reduced2 = items.stream()
                .reduce("Zero", (acc, item) -> acc + " " + item);
        System.out.println(reduced2);
        String reduced3 = items.stream()
                .filter(item -> item.endsWith("e"))
                .reduce("", (acc, item) -> acc + " " + item);
        System.out.println(reduced3);
    }

}
{% endhighlight %}

<p><strong>Output</strong></p>
{% highlight java %}
[One]
[ONE, TWO, THREE]
One
Three
2
One Two Three
Zero One Two Three
 One Three
{% endhighlight %}


##Q. Are the filter and map parameters immediately processed when passed? If no why it is so.
<p>When you call the filter() / map() method on a Stream, the filter / map passed as parameter to the filter() / map() method is stored internally. No filtering /mapping takes place yet. The parameter passed to the filter() function determines what items in the stream should be processed, and which that should be excluded from the processing. If the Predicate.test() method of the parameter passed to filter() returns true for an item, that means it should be processed. If false is returned, the item is not processed.</p>

<p>Java 8 Streams are designed in such a way that most of its stream operations returns Streams only. This help us creating chain of various stream operations. This is called as <strong>pipelining.</strong></p>


##What is streaming.
<p>All of us have watch online videos on youtube or some other such website. When you start watching video, a small portion of file is first loaded into your computer and start playing. You don’t need to download complete video before start playing it. This is called <strong>streaming.</strong></p>


##What is difference between collection & stream.
<p>A Collection is an <strong>in-memory data structure</strong>, which holds all the values that the data structure currently has—every element in the Collection has to be computed before it can be added to the Collection.</p> 
<p>A Stream is a conceptually <strong>fixed data structure</strong>, in which elements are computed on demand. This gives rise to significant programming benefits. The idea is that a user will extract only the values they require from a Stream, and these elements are only produced—invisibly to the user—as and when required. This is a form of a producer-consumer relationship.</p>


##Characteristics of Stream:
- Not a data structure
- Designed for lambdas
- Do not support indexed access
- Can easily be outputted as arrays or lists
- Lazy access supported
- Parallelizable

##Collectors = 
<p>Collectors are used to combine the result of processing on the elements of a stream. Collectors can be used to return a list or a string.</p>
<p>Collectors toList() returns a Collector that accumulates the input elements into a new List.</p>

<p><strong>toList Syntax =<strong></p>
{% highlight java %}
    public static <T> Collector<T,?,List<T>> toList()
{% endhighlight %}

<p><strong>Example =</strong></p>
{% highlight java %}
    Stream<String> s = Stream.of("a","b","c");
    
    List<String> names = s
        .collect(Collectors.toList());

    System.out.println(names);
{% endhighlight %}


##Predicate
[Predicate](http://shwetasadawarte.github.io/lessons/2015/12/15/java8-predicate/)