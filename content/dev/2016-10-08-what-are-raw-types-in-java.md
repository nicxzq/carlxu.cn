---
title: What are raw types in Java
author: Carlxu
type: post
date: 2016-10-08T09:09:49+00:00
url: /201610/64/
categories:
  - JAVA

---
### Questions:

  * What are raw types in Java, and why do I often hear that they shouldn&#8217;t be used in new code?
  * What is the alternative if we can&#8217;t use raw types, and how is it better?

<!--more-->

## Answers:

## What is a raw type?

The Java Language Specification defines a _raw type_ as follows:

### [JLS 4.8 Raw Types][1]

> A raw type is defined to be one of:
> 
>   * The reference type that is formed by taking the name of a generic type declaration without an accompanying type argument list.
>   * An array type whose element type is a raw type.
>   * A non-`static` member type of a raw type `R` that is not inherited from a superclass or superinterface of `R`.

Here&#8217;s an example to illustrate:

<pre class="lang-java prettyprint prettyprinted"><code>&lt;span class="kwd">public&lt;/span> &lt;span class="kwd">class&lt;/span> &lt;span class="typ">MyType&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="pln">E&lt;/span>&lt;span class="pun">&gt;&lt;/span> &lt;span class="pun">{&lt;/span>
    &lt;span class="kwd">class&lt;/span> &lt;span class="typ">Inner&lt;/span> &lt;span class="pun">{&lt;/span> &lt;span class="pun">}&lt;/span>
    &lt;span class="kwd">static&lt;/span> &lt;span class="kwd">class&lt;/span> &lt;span class="typ">Nested&lt;/span> &lt;span class="pun">{&lt;/span> &lt;span class="pun">}&lt;/span>

    &lt;span class="kwd">public&lt;/span> &lt;span class="kwd">static&lt;/span> &lt;span class="kwd">void&lt;/span>&lt;span class="pln"> main&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">[]&lt;/span>&lt;span class="pln"> args&lt;/span>&lt;span class="pun">)&lt;/span> &lt;span class="pun">{&lt;/span>
        &lt;span class="typ">MyType&lt;/span>&lt;span class="pln"> mt&lt;/span>&lt;span class="pun">;&lt;/span>          &lt;span class="com">// warning: MyType is a raw type&lt;/span>
        &lt;span class="typ">MyType&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="typ">Inner&lt;/span>&lt;span class="pln"> inn&lt;/span>&lt;span class="pun">;&lt;/span>   &lt;span class="com">// warning: MyType.Inner is a raw type&lt;/span>

        &lt;span class="typ">MyType&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="typ">Nested&lt;/span>&lt;span class="pln"> nest&lt;/span>&lt;span class="pun">;&lt;/span> &lt;span class="com">// no warning: not parameterized type&lt;/span>
        &lt;span class="typ">MyType&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">Object&lt;/span>&lt;span class="pun">&gt;&lt;/span>&lt;span class="pln"> mt1&lt;/span>&lt;span class="pun">;&lt;/span> &lt;span class="com">// no warning: type parameter given&lt;/span>
        &lt;span class="typ">MyType&lt;/span>&lt;span class="pun">&lt;?&gt;&lt;/span>&lt;span class="pln"> mt2&lt;/span>&lt;span class="pun">;&lt;/span>      &lt;span class="com">// no warning: type parameter given (wildcard OK!)&lt;/span>
    &lt;span class="pun">}&lt;/span>
&lt;span class="pun">}&lt;/span></code></pre>

Here, `MyType<E>` is a _parameterized type_ ([JLS 4.5][2]). It is common to colloquially refer to this type as simply `MyType` for short, but technically the name is `MyType<E>`.

`mt` has a raw type (and generates a compilation warning) by the first bullet point in the above definition; `inn` also has a raw type by the second bullet point.

`MyType.Nested` is not a parameterized type, even though it&#8217;s a member type of a parameterized type `MyType<E>`, because it&#8217;s `static`.

`mt1`, and `mt2` are both declared with actual type parameters, so they&#8217;re not raw types.

* * *

## What&#8217;s so special about raw types?

Essentially, raw types behaves just like they were before generics were introduced. That is, the following is entirely legal at compile-time.

<pre class="lang-java prettyprint prettyprinted"><code>&lt;span class="typ">List&lt;/span>&lt;span class="pln"> names &lt;/span>&lt;span class="pun">=&lt;/span> &lt;span class="kwd">new&lt;/span> &lt;span class="typ">ArrayList&lt;/span>&lt;span class="pun">();&lt;/span> &lt;span class="com">// warning: raw type!&lt;/span>&lt;span class="pln">
names&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">add&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="str">"John"&lt;/span>&lt;span class="pun">);&lt;/span>&lt;span class="pln">
names&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">add&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="str">"Mary"&lt;/span>&lt;span class="pun">);&lt;/span>&lt;span class="pln">
names&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">add&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="typ">Boolean&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">FALSE&lt;/span>&lt;span class="pun">);&lt;/span> &lt;span class="com">// not a compilation error!&lt;/span></code></pre>

The above code runs just fine, but suppose you also have the following:

<pre class="lang-java prettyprint prettyprinted"><code>&lt;span class="kwd">for&lt;/span> &lt;span class="pun">(&lt;/span>&lt;span class="typ">Object&lt;/span>&lt;span class="pln"> o &lt;/span>&lt;span class="pun">:&lt;/span>&lt;span class="pln"> names&lt;/span>&lt;span class="pun">)&lt;/span> &lt;span class="pun">{&lt;/span>
    &lt;span class="typ">String&lt;/span>&lt;span class="pln"> name &lt;/span>&lt;span class="pun">=&lt;/span> &lt;span class="pun">(&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">)&lt;/span>&lt;span class="pln"> o&lt;/span>&lt;span class="pun">;&lt;/span>
    &lt;span class="typ">System&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">out&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">println&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="pln">name&lt;/span>&lt;span class="pun">);&lt;/span>
&lt;span class="pun">}&lt;/span> &lt;span class="com">// throws ClassCastException!&lt;/span>
  &lt;span class="com">//    java.lang.Boolean cannot be cast to java.lang.String&lt;/span></code></pre>

Now we run into trouble at run-time, because `names` contains something that isn&#8217;t an `instanceof String`.

Presumably, if you want `names` to contain only `String`, you _could_ perhaps still use a raw type and_manually check every_ `add` yourself, and then _manually cast_ to `String` every item from `names`.**Even better**, though is NOT to use a raw type and _let the compiler do all the work for you_, harnessing the power of Java generics.

<pre class="lang-java prettyprint prettyprinted"><code>&lt;span class="typ">List&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">&gt;&lt;/span>&lt;span class="pln"> names &lt;/span>&lt;span class="pun">=&lt;/span> &lt;span class="kwd">new&lt;/span> &lt;span class="typ">ArrayList&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">&gt;();&lt;/span>&lt;span class="pln">
names&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">add&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="str">"John"&lt;/span>&lt;span class="pun">);&lt;/span>&lt;span class="pln">
names&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">add&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="str">"Mary"&lt;/span>&lt;span class="pun">);&lt;/span>&lt;span class="pln">
names&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">add&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="typ">Boolean&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">FALSE&lt;/span>&lt;span class="pun">);&lt;/span> &lt;span class="com">// compilation error!&lt;/span></code></pre>

Of course, if you _DO_ want `names` to allow a `Boolean`, then you can declare it as `List<Object> names`, and the above code would compile.

### See also

  * [Java Tutorials/Generics][3]

* * *

## How&#8217;s a raw type different from using `<Object>` as type parameters?

The following is a quote from _Effective Java 2nd Edition, Item 23: Don&#8217;t use raw types in new code_:

> Just what is the difference between the raw type `List` and the parameterized type `List<Object>`? Loosely speaking, the former has opted out generic type checking, while the latter explicitly told the compiler that it is capable of holding objects of any type. While you can pass a `List<String>` to a parameter of type `List`, you can&#8217;t pass it to a parameter of type `List<Object>`. There are subtyping rules for generics, and `List<String>` is a subtype of the raw type `List`, but not of the parameterized type `List<Object>`. As a consequence, **you lose type safety if you use raw type like `List`, but not if you use a parameterized type like `List<Object>`**.

To illustrate the point, consider the following method which takes a `List<Object>` and appends a `new Object()`.

<pre class="lang-java prettyprint prettyprinted"><code>&lt;span class="kwd">void&lt;/span>&lt;span class="pln"> appendNewObject&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="typ">List&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">Object&lt;/span>&lt;span class="pun">&gt;&lt;/span>&lt;span class="pln"> list&lt;/span>&lt;span class="pun">)&lt;/span> &lt;span class="pun">{&lt;/span>&lt;span class="pln">
   list&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">add&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="kwd">new&lt;/span> &lt;span class="typ">Object&lt;/span>&lt;span class="pun">());&lt;/span>
&lt;span class="pun">}&lt;/span></code></pre>

Generics in Java are invariant. A `List<String>` is not a `List<Object>`, so the following would generate a compiler warning:

<pre class="lang-java prettyprint prettyprinted"><code>&lt;span class="typ">List&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">&gt;&lt;/span>&lt;span class="pln"> names &lt;/span>&lt;span class="pun">=&lt;/span> &lt;span class="kwd">new&lt;/span> &lt;span class="typ">ArrayList&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">&gt;();&lt;/span>&lt;span class="pln">
appendNewObject&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="pln">names&lt;/span>&lt;span class="pun">);&lt;/span> &lt;span class="com">// compilation error!&lt;/span></code></pre>

If you had declared `appendNewObject` to take a raw type `List` as parameter, then this would compile, and you&#8217;d therefore lose the type safety that you get from generics.

### See also

  * [What is the difference between `<E extends Number>` and `<Number>`?][4]
  * [java generics (not) covariance][5]

* * *

## How&#8217;s a raw type different from using `<?>` as a type parameter?

`List<Object>`, `List<String>`, etc are all `List<?>`, so it may be tempting to just say that they&#8217;re just `List` instead. However, there is a major difference: since a `List<E>` defines only `add(E)`, you can&#8217;t add just any arbitrary object to a `List<?>`. On the other hand, since the raw type `List`does not have type safety, you can `add` just about anything to a `List`.

Consider the following variation of the previous snippet:

<pre class="lang-java prettyprint prettyprinted"><code>&lt;span class="kwd">static&lt;/span> &lt;span class="kwd">void&lt;/span>&lt;span class="pln"> appendNewObject&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="typ">List&lt;/span>&lt;span class="pun">&lt;?&gt;&lt;/span>&lt;span class="pln"> list&lt;/span>&lt;span class="pun">)&lt;/span> &lt;span class="pun">{&lt;/span>&lt;span class="pln">
    list&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">add&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="kwd">new&lt;/span> &lt;span class="typ">Object&lt;/span>&lt;span class="pun">());&lt;/span> &lt;span class="com">// compilation error!&lt;/span>
&lt;span class="pun">}&lt;/span>
&lt;span class="com">//...&lt;/span>

&lt;span class="typ">List&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">&gt;&lt;/span>&lt;span class="pln"> names &lt;/span>&lt;span class="pun">=&lt;/span> &lt;span class="kwd">new&lt;/span> &lt;span class="typ">ArrayList&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">&gt;();&lt;/span>&lt;span class="pln">
appendNewObject&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="pln">names&lt;/span>&lt;span class="pun">);&lt;/span> &lt;span class="com">// this part is fine!&lt;/span></code></pre>

The compiler did a wonderful job of protecting you from potentially violating the type invariance of the `List<?>`! If you had declared the parameter as the raw type `List list`, then the code would compile, and you&#8217;d violate the type invariant of `List<String> names`.

* * *

## A raw type is the erasure of that type

Back to JLS 4.8:

> It is possible to use as a type **the erasure** of a parameterized type or the erasure of an array type whose element type is a parameterized type. **Such a type is called a _raw type_.**
> 
> _[&#8230;]_
> 
> The superclasses (respectively, superinterfaces) of a raw type are the erasures of the superclasses (superinterfaces) of any of the parameterizations of the generic type.
> 
> The type of a constructor, instance method, or non-`static` field of a raw type `C` that is not inherited from its superclasses or superinterfaces is the raw type that corresponds to the erasure of its type in the generic declaration corresponding to `C`.

In simpler terms, when a raw type is used, the constructors, instance methods and non-`static`fields are _also erased_.

Take the following example:

<pre class="lang-java prettyprint prettyprinted"><code>&lt;span class="kwd">class&lt;/span> &lt;span class="typ">MyType&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="pln">E&lt;/span>&lt;span class="pun">&gt;&lt;/span> &lt;span class="pun">{&lt;/span>
    &lt;span class="typ">List&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">&gt;&lt;/span>&lt;span class="pln"> getNames&lt;/span>&lt;span class="pun">()&lt;/span> &lt;span class="pun">{&lt;/span>
        &lt;span class="kwd">return&lt;/span> &lt;span class="typ">Arrays&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">asList&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="str">"John"&lt;/span>&lt;span class="pun">,&lt;/span> &lt;span class="str">"Mary"&lt;/span>&lt;span class="pun">);&lt;/span>
    &lt;span class="pun">}&lt;/span>

    &lt;span class="kwd">public&lt;/span> &lt;span class="kwd">static&lt;/span> &lt;span class="kwd">void&lt;/span>&lt;span class="pln"> main&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">[]&lt;/span>&lt;span class="pln"> args&lt;/span>&lt;span class="pun">)&lt;/span> &lt;span class="pun">{&lt;/span>
        &lt;span class="typ">MyType&lt;/span>&lt;span class="pln"> rawType &lt;/span>&lt;span class="pun">=&lt;/span> &lt;span class="kwd">new&lt;/span> &lt;span class="typ">MyType&lt;/span>&lt;span class="pun">();&lt;/span>
        &lt;span class="com">// unchecked warning!&lt;/span>
        &lt;span class="com">// required: List&lt;String&gt; found: List&lt;/span>
        &lt;span class="typ">List&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pun">&gt;&lt;/span>&lt;span class="pln"> names &lt;/span>&lt;span class="pun">=&lt;/span>&lt;span class="pln"> rawType&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">getNames&lt;/span>&lt;span class="pun">();&lt;/span>
        &lt;span class="com">// compilation error!&lt;/span>
        &lt;span class="com">// incompatible types: Object cannot be converted to String&lt;/span>
        &lt;span class="kwd">for&lt;/span> &lt;span class="pun">(&lt;/span>&lt;span class="typ">String&lt;/span>&lt;span class="pln"> str &lt;/span>&lt;span class="pun">:&lt;/span>&lt;span class="pln"> rawType&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">getNames&lt;/span>&lt;span class="pun">())&lt;/span>
            &lt;span class="typ">System&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">out&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">print&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="pln">str&lt;/span>&lt;span class="pun">);&lt;/span>
    &lt;span class="pun">}&lt;/span>
&lt;span class="pun">}&lt;/span></code></pre>

When we use the raw `MyType`, `getNames` becomes erased as well, so that it returns a raw `List`!

[JLS 4.6][6] continues to explain the following:

> **Type erasure also maps the signature of a constructor or method to a signature that has no parameterized types or type variables.** The erasure of a constructor or method signature `s` is a signature consisting of the same name as `s` and the erasures of all the formal parameter types given in `s`.
> 
> **The return type of a method and the type parameters of a generic method or constructor also undergo erasure if the method or constructor&#8217;s signature is erased.**
> 
> The erasure of the signature of a generic method has no type parameters.

* * *

## If it&#8217;s unsafe, why is it allowed to use a raw type?

Here&#8217;s another quote from JLS 4.8:

> The use of raw types is allowed only as a concession to compatibility of legacy code. _The use of raw types in code written after the introduction of genericity into the Java programming language is strongly discouraged. It is possible that future versions of the Java programming language will disallow the use of raw types._

_Effective Java 2nd Edition_ also has this to add:

> Given that you shouldn&#8217;t use raw types, why did the language designers allow them? To provide compatibility.
> 
> The Java platform was about to enter its second decade when generics were introduced, and there was an enormous amount of Java code in existence that did not use generics. It was deemed critical that all this code remains legal and interoperable with new code that does use generics. It had to be legal to pass instances of parameterized types to methods that were designed for use with ordinary types, and vice versa. This requirement, known as _migration compatibility_, drove the decision to support raw types.

In summary, raw types should NEVER be used in new code. **You should always use parameterized types**.

* * *

## Are there no exceptions?

Unfortunately, because Java generics are non-reified, there are two exceptions where raw types must be used in new code:

  * Class literals, e.g. `List.class`, not `List<String>.class`
  * `instanceof` operand, e.g. `o instanceof Set`, not `o instanceof Set<String>`

### See also

  * [Why is `Collection<String>.class` Illegal?][7]

 [1]: https://docs.oracle.com/javase/specs/jls/se8/html/jls-4.html#jls-4.8
 [2]: https://docs.oracle.com/javase/specs/jls/se8/html/jls-4.html#jls-4.5
 [3]: https://docs.oracle.com/javase/tutorial/java/generics/
 [4]: http://stackoverflow.com/questions/2770264/what-is-the-difference-between-e-extends-number-and-number/
 [5]: http://stackoverflow.com/questions/2660827/java-generics-covariance
 [6]: https://docs.oracle.com/javase/specs/jls/se8/html/jls-4.html#jls-4.6
 [7]: http://stackoverflow.com/questions/2745193/why-is-collectionstring-class-illegal/