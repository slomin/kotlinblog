---
layout: post
title: 10 reasons why Kotlin will be big
comments: true
---
In this post, I'm going to list 10 reasons why **in my opinion** Kotlin will become a popular programming language. Keep in mind those are my personal views.

1. The main reason: [Java programming language](https://en.wikipedia.org/wiki/Java_(programming_language)) appeared 22 years ago which makes it quite an old technology. Java was improved upon a lot since 1995 but had to maintain most of its core features and syntax. The code written in Java is famous for not being very readable and maintainable. I'm not going to elaborate here, it would require a separate post to list all the issues with Java as a programming language in 2017.

2. Kotlin is extremely easy to learn for an experienced Java developer. Basically, Kotlin could be called "Java 2.0 without the syntax compatibility". I'm not the best Java developer out there nor the most experienced, but it took me around 5 days of playing with Kotlin (in the evenings, for about 2-3 hours each session) to be able to write production Kotlin code that was on pair with my Java code in terms of quality. There are a lot of new features and concepts (especially if you come from Java < 1.7-1.8) but you can learn them gradually. Kotlin doesn't have a steep learning curve similar to Scala. If you're a decent Java or C# coder you will be able to grasp it really quickly.

3. Kotlin is developed by [very competent people](https://www.jetbrains.com/) with a lot of support behind them. Four weeks ago at Google I/O 2017 Android Development Tools team announced official [Kotlin support](https://developer.android.com/kotlin/index.html#kotlin-android-support-announced-at-google-io) for Android. It is well proven that Open Source projects (especially programming languages) have greater success rate with support from big commercial organizations.

4. One of the main design principles behind Kotlin is Java interoperability. I can tell from my own personal experience that this is not just some marketing BS. It really works well with Java! And by "Java interoperability" guys at JetBrains mean mixing Java and Kotlin in your codebase as well as using Java libraries in your 100% Kotlin app (my experience here is limited to Android development but I have no reasons to doubt it will behave the same in some more "classic" Java uses).

5. Android OS is HUGE! Right now there are around [2 billion](https://www.theverge.com/2017/5/17/15654454/android-reaches-2-billion-monthly-active-users) Google Android devices in the wild. Add around 500 to 700 million devices without "Google Experience" package and it is by far most popular computer OS in history. And it will be more popular - install base will probably double by the end of 2021. Google is also developing other platforms based on Android OS, most notable [Android Things](https://developer.android.com/things/). And Android development needs a modern programming language. Kotlin is an obvious choice here.

6. Kotlin is being designed to be ubiquitous and universal. Right now it compiles to Java bytecode and can run on any JVM which supports Java 1.6 or later. It also compiles to JavaScript. Kotlin team is also working with [LLVM](https://en.wikipedia.org/wiki/LLVM) on [Kotlin/Native](https://github.com/JetBrains/kotlin-native). All those efforts might in the future result in something that might be called "semi-universal computer language", meaning it could be used in most development tasks (frontend, backend, high and low-level development).

7. Kotlin is modern computer language which has all the "cool" features needed in 2017. Java <1.8 is not. Simple as that.

8. Kotlin is [designed with safety](https://zeroturnaround.com/rebellabs/jvm-languages-report-extended-interview-with-kotlin-creator-andrey-breslav/) as its core principle (similar to [Swift](http://khanlou.com/2017/04/safety-in-swift/)). Some people [don't like](http://blog.cleancoder.com/uncle-bob/2017/01/11/TheDarkPath.html) languages designed to shelter programmers from their own stupidity, but I personally am a big fan of such solutions. We are imperfect people and operate in the imperfect world (limited resources, deadlines, unskilled developers on our teams) and this kind of tradeoff in most cases is an advantage.

9. Kotlin was designed by a [commercial entity](https://www.jetbrains.com/) with a goal of being an industrial language used for real-life applications. This might sound like something that is a marketing jibberish, but IMO, some of the languages designed by academics have a little bit different DNA and aren't that suitable for real world applications as Kotlin.

10. Kotlin is FAR MORE readable than Java code. There are multiple reasons for that - its syntax is more concise, there is a lot of syntactic sugar built in (i.e. Data objects). In my personal experience, when I refactor my Android code using Kotlin I end up trimming around 20 to 40% of my code "volume", without resolving to any nasty one-liners or ugly hacks.

To sum it all up, there are computer languages which have some of those advantages, but so far there was no single language which combined them all. The rapid and wide Kotlin adoption only proves my thesis - **Kotlin WILL be big!**
