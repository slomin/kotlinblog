---
layout: post
title: Android Architecture Components With Kotlin - Lifecycle
comments: true
---
Google recently released its official [guide to the Android app architecture](https://developer.android.com/topic/libraries/architecture/guide.html) with a bunch of libraries called [Architecture Components](https://developer.android.com/topic/libraries/architecture/adding-components.html). This looks very promising since Android has been missing a standard way of implementing some kind of clean architecture. There were many unofficial ways to implement [MVP](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter) and [MVVM](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93viewmodel) patterns, from which I had a chance to use a couple, including [Mosby](http://hannesdorfmann.com/mosby/).

The problem was lack of standards. When I switched a project I had to learn completely new MVP/MVC/MVVM implementation which did exactly the same thing I was used to, just in a different way. I always thought it would be nice if Google provided some "official" support for app architecture which the industry could adopt.

In this post, I'm going to explore the [ViewModel](https://developer.android.com/topic/libraries/architecture/viewmodel.html), [LifecycleOwner](https://developer.android.com/reference/android/arch/lifecycle/LifecycleOwner.html), and [LiveData](https://developer.android.com/reference/android/arch/lifecycle/LifecycleOwner.html) from the Architecture Components Library. All the code here is of course Kotlin.

*The code for this tutorial is available [here](https://github.com/slomin/Kotlin-Architecture-Lifecycle). The sample app requires Android Studio 3.0, at the time of writing this post I used Android Studio 3.0 Canary 5. If you want to use Canary version of Android Studio along your stable version on the same machine, check out [this video](https://www.youtube.com/watch?v=SBbWGxXCMqQ). I will update the GitHub repository to more stable versions of Android Studio 3.0 when available*.

As an example, I created a simple app which contains Activity and two Fragments. The app is showing two Fragments connected to [shared Activity](https://github.com/slomin/Kotlin-Architecture-Lifecycle/blob/master/app/src/main/java/com/kotlinblog/arch/SharedActivity.kt). The [first Fragment](https://github.com/slomin/Kotlin-Architecture-Lifecycle/blob/master/app/src/main/java/com/kotlinblog/arch/FirstFragment.kt) is displaying simple countdown timer, the [second Fragment](https://github.com/slomin/Kotlin-Architecture-Lifecycle/blob/master/app/src/main/java/com/kotlinblog/arch/FirstFragment.kt) has all the controls:

![Architecture sample app first screenshot]({{ site.url }}/images/android_architecture_1/screenshot_1.png){: .center-image }

When you tap "START" the app starts the counter:

![Architecture sample app second screenshot]({{ site.url }}/images/android_architecture_1/screenshot_2.png){: .center-image }

The state of the counter is preserved during orientation change, when the [shared Activity](https://github.com/slomin/Kotlin-Architecture-Lifecycle/blob/master/app/src/main/java/com/kotlinblog/arch/SharedActivity.kt) is being recreated:

![Architecture sample app third screenshot]({{ site.url }}/images/android_architecture_1/screenshot_3.png){: .center-image }

You can also stop the timer or log the timer state.

### App's architecture explained

First, we need to import the required library. To do this we add the dependency to the apps build.gradle file in dependencies section:
{% highlight groovy %}
// Android Architecture Components
compile "android.arch.lifecycle:extensions:$arch_version"
{% endhighlight %}

where `'$arch_version'` is the library's version. Google is currently providing Architecture Components as a separate library but after reaching v1.0 it will be part of the support libraries.

Our [shared Activity](https://github.com/slomin/Kotlin-Architecture-Lifecycle/blob/master/app/src/main/java/com/kotlinblog/arch/SharedActivity.kt) extends LifecycleActivity() from the library.

{% gist e8bbbd677ebc4c4df19de04d1af8daf1 %}

Our app's business logic is located in [SharedViewModel](https://github.com/slomin/Kotlin-Architecture-Lifecycle/blob/master/app/src/main/java/com/kotlinblog/arch/SharedViewModel.kt) class, which extends [ViewModel](https://developer.android.com/topic/libraries/architecture/viewmodel.html) class. Its purpose is to *"store and manage UI-related data so that the data survives configuration changes such as screen rotations"*. The business logic here is a simple countdown timer. We store the formatted time String as [MutableLiveData](https://developer.android.com/reference/android/arch/lifecycle/MutableLiveData.html), an Architecture Components holder which stores data that can be observed. The difference between [LiveData](https://developer.android.com/reference/android/arch/lifecycle/LiveData.html) is that it exposes setters. Note that we also use a `TimerStateModel` object (custom [Kotlin Data class](https://kotlinlang.org/docs/reference/data-classes.html)) which also survives orientation change:

{% gist de2609712ef9c54d85a1a435664dfd65 %}

In [FirstFragment](https://github.com/slomin/Kotlin-Architecture-Lifecycle/blob/master/app/src/main/java/com/kotlinblog/arch/FirstFragment.kt) we make the formattedTime observed. First we create `timeObserver` which updates our `tvTimer` TextView every time the `mFormattedTime` in our `SharedViewModel` is getting changed. We are obtaining instance of our `SharedViewModel` (see code line 10 below) and then we subscribe to the observer (code line 13). The `activity` cast as `LifecycleOwner` which we pass to the `observe` method is Kotlin's convenience method to get our `SharedActivity` instance. We are accessing `formattedTime` via our public getter.

{% gist d383bdb1c561a0d991f6a46cc92846f5 %}

In the [SecondFragment](https://github.com/slomin/Kotlin-Architecture-Lifecycle/blob/master/app/src/main/java/com/kotlinblog/arch/SecondFragment.kt) in `onViewCreated` method first we obtain an instance of our `SharedViewModel` and then we set all the appropriate onClickListeners (code lines 7-9).

{% gist 4cc4ca8ef8190b61dcebf5ccd4bb4345 %}

In this simple example we delegated all of the business logic to a `ViewModel`. Our fragments are only responsible for observing the data changes (using convenience of LiveData) and responding for user input. Everything is managed by the Architecture Components library so there is very little boilerplate. Also, it reduces the possibility of shooting ourselves in the foot by mismanaging app state, which in my experience is one of the most common bugs every Android developer experiences.

If you want to do some further reading about Architecture Components I recommend those excellent articles:

[Exploring the new Android Architecture Components library](https://medium.com/exploring-android/exploring-the-new-android-architecture-components-c33b15d89c23) by Joe Birch

[ANDROID ARCHITECTURE COMPONENTS – LOOKING AT VIEWMODELS – PART 2](https://riggaroo.co.za/android-architecture-components-looking-viewmodels-part-2/) and
[ANDROID ARCHITECTURE COMPONENTS – LOOKING AT LIFECYCLES – PART 3](https://riggaroo.co.za/android-architecture-components-looking-lifecycles-part-3/) by Rebecca Franks

[Styling Android articles](https://blog.stylingandroid.com/category/architecture-components/)
