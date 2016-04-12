---
layout: page
description: Let's talk about Syntax 
title:  "Basic Java Syntax"
date:   2016-04-11 16:10:04 -0400
categories: java syntax basics
---

## Java Syntax

Here is a running digest of the [syntax](https://en.wikipedia.org/wiki/Syntax) of the Java language.

### Basic Types
Here are the differnt 

*   int  - whole numbers (`int i = 42;`)
*   String - free-form text (`String s = "Hello!";`)
*   char - one character of free-form text (`char c = 'H';`)
*   bool - either a true or false value (`bool isAwesome = true;`)
*   double - a double-precision decimal value (`double accountBalance = 1.00;`)
*   float - a single-precision decimal value (`float pi = 3.14;`);
*   long - a large whole number (`long l = 4200000000;`);

### Classes
With only a couple of exceptions, the vast majority of Java code exists inside either a class or Interface. Classes are abstractions of real-world objects in code. They are the blueprints of any object in Java.

{% highlight java linenos %}
class SampleClass {
    
}
{% endhighlight %}

#### Fields
Classes can contain fields. Fields are properties that each instance of the class can have. A field can be of any class, including the base classes that are a part of the Java language. Here is how you declare a field: 

{% highlight java linenos %}
class SampleClass {
    String sampleField;
    AnotherClass anotherField;
}
{% endhighlight %}

Sometimes in order to properly define a model, you may want a field to apply to ALL instances of a class. In this case, it's possible to define what's called a static field. Note the only difference between this and a regular field is the presence of the `static` keyword.

{% highlight java linenos %}
class SampleClass {
    static String sampleField;
    static AnotherClass anotherField;
}
{% endhighlight %}

You can declare and set fields (like all variables) on the same line:

{% highlight java linenos %}
class SampleClass {
    static String sampleField = "Hello, World!";
}
{% endhighlight %}


#### Methods
Along with fields, classes can contain methods. You can think of methods like mathematical functions -- you take in whatever inputs you need to perform an action, then return data if need be.

The different inputs to a function are its parameters. Whatever is returned by the function is its "return type".

{% highlight java linenos %}
class SampleClass {
    // `addOne` takes one parameter of type int,
    // returns another int.
    int addOne(int number) {
        int results = number + 1;
        return results;
    }
    
    // `greetUser` prints a welcome message,
    // but does not return anything
    void greetUser(String userName) {
        System.out.println("Hello, " + userName);
    }
}
{% endhighlight %}

Just like fields, methods can be static. The two methods above can be made static since they don't have any references to fields:

{% highlight java linenos %}
class SampleClass {
    // `addOne` takes one parameter of type int,
    // returns another int.
    static int addOne(int number) {
        int results = number + 1;
        return results;
    }
    
    // `greetUser` prints a welcome message,
    // but does not return anything
    static void greetUser(String userName) {
        System.out.println("Hello, " + userName);
    }
}
{% endhighlight %}

*NOTE:* Static fields and methods can _not_ contain references to non-static methods or fields.

In a non-static context, you can access the current object by using the `this` keyword. e.g., `this.name`.

#### Constructors
Constructors are special methods designed to create objects. The name of these methods are the same of the enclosing type. By default, all classes receive a parameterless constructor by the Java compiler. A constructor looks like so:

{% highlight java linenos %}
class SampleClass {
    String name;
    int meaningOfLife;
    
    // this is a parameterless constructor.
    SampleClass() {
    }
    
    SampleClass(String name, int randomNumber) {
        
        // we only have to use `this` here because the field name
        // is the same as the parameter name.
        this.name = name;
        
        // note that we don't have to do the same here.
        meaningOfLife = randomNumber;
    }
}
{% endhighlight %}

Usually you would make a constructor if you wanted to ensure the existence of field values before creating an object.

#### Access Modifiers

#### Inheritance


### Arrays

### Interfaces

### Data Structures

### Packages

### Methods