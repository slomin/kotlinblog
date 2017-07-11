---
layout: post
title: Android Things - Quick Overview And Getting Started
comments: true
---
On December 2016 Google released first Developer Preview of [Android Things](https://developer.android.com/things/hardware/index.html), their [IoT platform](https://en.wikipedia.org/wiki/Internet_of_things), based on the Android operating system. I'm not going to elaborate here on details, you can find all you need on the [official website](https://developer.android.com/things) but there are 3 interesting points to make about the fairly new OS:

1. It's done by Google. There are dozens of IoT platforms now in the "Linux box" category, but somehow I have a feeling that Google is the most capable entity to provide standard OS for IoT applications.
2. In 2017 there are two categories of IoT devices. The small, mostly battery powered devices (think smart sensors, beacons etc), based on microcontrollers (right now [ARM Cortex-M](https://en.wikipedia.org/wiki/ARM_Cortex-M) architecture seems to be dominating that field). Those devices have sub-1MB storage capacity and sub-100KB RAM capacity, running clock speeds below ~100MHz. The second category is "Linux box" devices, which are basically smartphone class right now (think something like mid-end smartphone circa 2013) with the capacity to run sophisticated software (i.e. [Convolutional neural network](https://en.wikipedia.org/wiki/Convolutional_neural_network), advanced networking etc.). Android Things is targeting the latter category.
3. It is basically and Android OS, running [ART runtime environment](https://en.wikipedia.org/wiki/Android_Runtime), which means we can leverage all the Android tools, methodologies and libraries we love and use every day. And most importantly, we can write Kotlin for it!

### How to get started with Android Things? ###

First, I recommend watching this presentation from Google I/O 2017 with the current overview of the platform:

<iframe width="560" height="315" src="https://www.youtube.com/embed/sjpNek_7z-I" frameborder="0" allowfullscreen="allowfullscreen"></iframe>{: .center-image }
*Google I/O 2017 Android Things presentation*
{: .center-caption }

Second, you need to buy some hardware. But if you don't have experience with electronics I don't recommend starting straight from Android Things capable device. I recommend starting with inexpensive [Arduino](https://en.wikipedia.org/wiki/Arduino) starter kit. There are two reasons why:

- You will learn all the essentials (basics about [electronics engineering](https://en.wikipedia.org/wiki/Electronic_engineering), different parts, current, wiring a breadboard) on a cheap device that loads your code and boots in a matter of seconds. If you mess something up you won't burn fairly expensive device like Raspberry Pi. And all the basics are the same on both platforms.
- You will be able to use the same parts for Android Things development. Same breadboards, jumper wires, LEDs, resistors, LCDs etc.

![Arduino kit by Kuman]({{ site.url }}/images/android_things_1/things_1.jpg){: .center-image }
*Arduino kit by Kuman*
{: .center-caption }

I recommend cheap Arduino UNO R3 clone starter kit. I bought a starter kit from [Kuman](www.kumantech.com) for around ~30USD from Amazon, and the quality of the Arduino board was quite nice. In my opinion, the UNO R3 version is best for learning purposes (there are dozens more Arduino boards) cause this one is the "standard", easy to learn (pins are clearly marked so it is super easy to wire it up) and most of the tutorials use this board. When choosing your Arduino kit, make sure it has some [female to male jumper wires included](https://statics3.seeedstudio.com/product/jumperwire125mm_01.jpg) since the Raspberry Pi 3 uses male [GPIO](https://en.wikipedia.org/wiki/General-purpose_input/output) ports. Arduino uses custom [IDE](https://en.wikipedia.org/wiki/Arduino#Software_development) and the language you program in is based on C and C++. The IDE is very mature and a pleasure to develop in. After getting your starter kit, I would recommend going through this [tutorial series](https://www.youtube.com/watch?v=fCxzA9_kg6s&list=PLSAVqwUTEeq4pYaMaC-CwJmyDpnodMJUq) by Jeremy Blum. It goes through all the basics of electronics engineering, almost all the knowledge you acquire will be directly transferred to Android Things development.

![Arduino wired up with LCD]({{ site.url }}/images/android_things_1/things_2.jpg){: .center-image }
*Arduino wired up with the LCD screen*
{: .center-caption }

After playing a bit with Arduino and going through the basics you can switch to Android Things. For the first development board, I would recommend [Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/). It is very popular device, you can get it in any country for about 30-40USD. On a recent [Android Developers Backstage podcast](http://androidbackstage.blogspot.com/2017/06/episode-71-things.html), Android Things guys mentioned that this device is by far the most popular now in the community, which makes troubleshooting a lot easier. All the flashing and development instructions are available on the [official website](https://developer.android.com/things). As always, [Stack Overflow](https://stackoverflow.com/questions/tagged/android-things) is very helpful, especially now, during the preview phase were the official docs aren't mature yet.

![Raspberry Pi 3 blinking led]({{ site.url }}/images/android_things_1/things_3.jpg){: .center-image }
*Hello world of electronics: a blinking LED*
{: .center-caption }

![Raspberry Pi 3 with Arduino kit LCD]({{ site.url }}/images/android_things_1/things_4.jpg){: .center-image }
*Arduino 1602 LCD screen wired for Raspberry Pi with Android Things*
{: .center-caption }
