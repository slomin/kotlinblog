---
layout: post
title: Testing Room and LiveData with Kotlin
comments: true
---

In this post I'll show how to unit test Google's [Room persistence library](https://developer.android.com/topic/libraries/architecture/room.html) with [LiveData](https://developer.android.com/topic/libraries/architecture/livedata.html) in Android project written in Kotlin. You can find the project's code on my [GitHub](https://github.com/slomin/Testing-Room-LiveData).

The app is just storing user's name in our Room database. The [View](https://github.com/slomin/Testing-Room-LiveData/blob/master/app/src/main/java/com/kotlinblog/roomlivedata/MainActivity.kt) is observing LiveData retrieved from the database by the [ViewModel](https://github.com/slomin/Testing-Room-LiveData/blob/master/app/src/main/java/com/kotlinblog/roomlivedata/MainViewModel.kt).

The database is empty, when we tap "SHOW LOG" it is showing "null":

![Room and LiveData testing first screenshot]({{ site.url }}/images/testing_room_and_livedata/screenshot_1.png){: .center-image }

After adding the user, the UI is refreshed and the "SHOW LOG" is showing our new user:

![Room and LiveData testing second screenshot]({{ site.url }}/images/testing_room_and_livedata/screenshot_2.png){: .center-image }

Lets take a closer look how this functionality is implemented. First we have our User object:

{% gist 470295f96f1946e5a6cacc91b821ab5f %}

It contains a mutable field userName.

Then we have our UserDao class which is a [Data Access Object](https://en.wikipedia.org/wiki/Data_access_object):

{% gist e7b68512221e9bd39378b384f93a8f82 %}

It is a Java class. The reason for that is Android Studio is not yet (at time of me writing this blogpost) code highlighting and completion for Room SQL queries in Kotlin. There are 3 standard SQL methods (insert, delete and update) but also two more interesting: getUser() and getUserAsLiveData(). The latter is returning User object wrapped inside a [LiveData](https://developer.android.com/topic/libraries/architecture/livedata.html). I'll explain that later in this post.

Then we have our database:

{% gist 52dd5cc450a1b7bbb2c194c93c71b2eb %}

It contains one entity (User) and one Dao (UserDao). The companion object is just a quick way to have an instance of our database as a singleton. In production you probably should use some dependency injections framework (such as Dagger 2) to provide your database instances.The rest of the code is pretty straightforward.

Now lets switch to the unit testing part. First we need to create our database for testing purposes. Let's use abstract class here for code reusability:

{% gist 20599d50f8c7b8385c6995e68cad99ef %}

For testing purposes we are using Room's inMemoryDatabaseBuilder. It will create non-persistent instance of our database, which will be discarded after the test will pass.

Then we create our [UserDaoTest](https://github.com/slomin/Testing-Room-LiveData/blob/master/app/src/androidTest/java/com/kotlinblog/roomlivedata/dao/UserDaoTest.kt) class by extending abstract [DbTest](https://github.com/slomin/Testing-Room-LiveData/blob/master/app/src/androidTest/java/com/kotlinblog/roomlivedata/dao/DbTest.kt) class. Don't forget to use `open` modifier and annotate the class with `@RunWith(AndroidJUnit4::class)`.

Testing inserting and deleting user is pretty straightforward:

{% gist 0ba894db683cffe2090879620ac10e75 %}

Room's "in memory" database allows main thread operations so we can just call `appDatabase.userDao().user` to retrieve the User object. The problem arises when we want to call `getUserAsLiveData()` method. This method returns LiveData object. Room calculates the value wrapped in LiveData lazily, only when there is an observer. Fortunately using Kotlin's [extension functions](https://kotlinlang.org/docs/reference/extensions.html) we can solve this problem in elegant way.

Let's provide [a LiveData extension](https://github.com/slomin/Testing-Room-LiveData/blob/master/app/src/androidTest/java/com/kotlinblog/roomlivedata/extensions/LiveDataExtensions.kt) that will observe the value stored in LiveData, blocks the thread and returns the value:

{% gist dd782438d79a92f28e6301c140d77cc9 %}

Now we can use that in our test case:

{% gist 47ff4e3d48d1e4e31d4e1df4c6cb2818 %}

First we call `val userWrappedInLiveData = appDatabase.userDao().userAsLiveData` which returns LiveData<User> object. Then we apply our extension function to get User object: `val userFromDb = userWrappedInLiveData.getValueBlocking()`. As we can see, all three tests are passing:

![Tests results]({{ site.url }}/images/testing_room_and_livedata/screenshot_3.png){: .center-image }
