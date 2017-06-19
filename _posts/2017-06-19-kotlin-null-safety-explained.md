---
layout: post
title: Kotlin null safety explained
comments: true
---

In my Java developer's career, NullPointerException is the single most common runtime error I encounter.  And according to [this research](http://blog.takipi.com/the-top-10-exceptions-types-in-production-java-applications-based-on-1b-events/), I'm not an exception (pun intended!). Even the inventor of [null reference](https://en.wikipedia.org/wiki/Null_pointer), computer science pioneer [Tony Hoare](https://en.wikipedia.org/wiki/Tony_Hoare) called it [The Billion Dollar Mistake](https://www.infoq.com/presentations/Null-References-The-Billion-Dollar-Mistake-Tony-Hoare).

Fortunately, Kotlin introduces the concept of **null safety**. If you are using pure Kotlin (without mixing it with Java code) you encounter two types of references:

1. **The Non-Null type:**
{% highlight java %}
var nonNullReference: String = "I can't be null!"
nonNullReference = null // Compile-time error
{% endhighlight %}

*The non-null string's type is written as `'String'`*

{:start="2"}
2. **The Nullable type:**
{% highlight java %}
var nullableReference: String? = "I'm a nullable string"
nullableReference = null // Compiles just fine
{% endhighlight %}

*The nullable string's type is written as `'String?'`, with question mark suffix*

This way we're sure that the **non-null** reference will never throw dreaded NullPointerException. But what happens if we try to call some function on the **nullable** reference? **It won't happen because it will not compile.** The compiler doesn't care if the reference is null or not:

{% highlight java %}
println(nullableReference.length) // Compile-time error
{% endhighlight %}

We can't call functions on nullable references without explicitly handling the nullability. There are 3 basic ways to do that:

1. **"Classic" null check:**
{% highlight java %}
if (nullableReference != null) {
    println(nullableReference.length)
    println(nullableReference.hashCode())
    println(nullableReference.capitalize())
}
{% endhighlight %}
This is the exact same way as every Java coder did thousands of times. Compiler knows all the uses of our `nullableReference` inside the `if` block are safe, cause we checked it's **not null** before the calls are being made.

{:start="2"}
2. **Safe call:**
{% highlight java %}
println(nullableReference?.length)
{% endhighlight %}
The Kotlin safe calls are being made using the special operator `'?.'` - in our case, the expression `println(nullableReference?.length)` will not crash at runtime but instead return `null`. If the `nullableReference` **wasn't null** it would return the string's length as `'Int?'` (which itself is a nullable integer).

{:start="3"}
3. **Non-null asserted call:**
{% highlight java %}
println(nullableReference!!.length) // NPE thrown at runtime
{% endhighlight %}

While using a double exclamation mark (a.k.a "double bang") we are stating that we're **100% sure** our `nullableReference` is **not null.** This is the same behaviour as classic Java call without doing null-check. In our case, **the app will crash and the NullPointerException will be thrown!** This notation was made ugly on purpose, it is basically an indicator of [code smell](https://en.wikipedia.org/wiki/Code_smell) and should be used only when you want your app crash at runtime whenever there's null reference. In most cases you should either:

* Use **non-nullable** types whenever possible or
* If you are using **nullable** type, do a **safe call** or a **null-check**

### But what if we are mixing Kotlin with Java?

Fortunately, when our Java code is properly annotated it will behave exactly the same as Kotlin code. Kotlin compiler recognizes many [popular annotation frameworks](https://github.com/JetBrains/kotlin/blob/master/core/descriptor.loader.java/src/org/jetbrains/kotlin/load/java/JvmAnnotationNames.kt), including [Android annotations framework](https://developer.android.com/studio/write/annotations.html). If developer properly annotates the code with `'@NotNull'` and `'@Nullable'` annotations, the compiler will see those references as if they were Kotlin types. Fortunately for us mobile developers, Android framework and many popular libraries are already annotated properly.

If for whatever reason the Java code you are using wasn't annotated, Kotlin introduces the concept of [platform types](https://kotlinlang.org/docs/reference/java-interop.html#null-safety-and-platform-types). This means that whenever you are using such code, it will be treated the same as in Java. This was done for convenience (so the code wouldn't be filled with question marks and double-bangs). The platform type string is marked as `'String!'`.
