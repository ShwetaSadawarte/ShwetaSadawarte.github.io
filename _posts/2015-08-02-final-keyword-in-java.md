---
layout: post
category : lessons
tags : [final keyword, final class, final variable, final method, java]
---
{% include JB/setup %}

Final keyword can be used with variables, methods and class. 

##Final Keyword =

###final variables -
-final variables are nothing but constants. We cannot change the value of a final variable once it is initialized. 
-It is a good practice to name final variable in all CAPS.
-Local final variable must be initialized during declaration.
-A final variable that have no value at the time of declaration it is called `blank final variable` or `uninitialized final variable`. It can be initialized in the constructor only. 
-The blank final variable can be static also which will be initialized in the static block only.

**Example -** Modifying final variable gives Compile Time Error

{% highlight java %}
class Car {  
  final int speedLimit=90;//final variable  
  void run() {  
    speedLimit=400;  //Error: You cannot modify final variable
  }  
  public static void main(String args[]){  
    Car obj = new  Car();  
    obj.run();  
  }  
}
{% endhighlight %}

**Example -** For initializing blank final variable
{% highlight java %}
class Sample {  
    final int MAX_VALUE;	//Blank final variable	 
    Sample() {
        MAX_VALUE=100;	//It must be initialized in constructor
    }
    void myMethod(){  
        System.out.println(MAX_VALUE);
    }  
    public static void main(String args[]){  
        Sample obj = new  Sample();  
        obj.myMethod();  
    }  
}
{% endhighlight %}

###final method -
A final method cannot be overridden. Which means even though a subclass can call the final method of parent class without any issues but it cannot override it.
**Example -** You cannot override method. You will get compile time error.

{% highlight java %}
class Sample {  
    final void demo() {
      System.out.println("Sample Class Method");
    }  
}  
	     
class ABC extends Sample {  
    void demo() {
        System.out.println("ABC Class Method");
    }  
	     
    public static void main(String args[]){  
        ABC obj = new ABC();  
        obj.demo();  
    }  
}
{% endhighlight %}

**Example -** You can inherit method but cannot override.

{% highlight java %}
class Sample {  
   final void demo() {
      System.out.println("Sample Class Method");
   }  
}  
	     
class ABC extends Sample {  
   public static void main(String args[]){  
      ABC obj = new ABC();  
      obj.demo();  
   }  
}
{% endhighlight %}

###final class -
We cannot extend a final class. If you make any class as final, you cannot extend it.
**Example -** You will get Compile Time Error

{% highlight java %}
final class Sample{  
}  
	     
class ABC extends Sample{  
   void demo(){
      System.out.println(“Demo Method");
   }  
   public static void main(String args[]){  
      ABC obj= new ABC(); 
      obj.demo();
   }  
}
{% endhighlight %}

**Note -**
-A constructor cannot be declared as final. Because constructor is never inherited.
-All variables declared in an interface are by default final.
-If method parameters are declared final then the value of these parameters cannot be changed.


