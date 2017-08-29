---
layout: post
title: Running TensorFlow on Android Things
comments: true
---
In May of 2017 Google announced its TensorFlow library's version dedicated for mobile devices, back then called TensorFlow Lite. Later they rebranded it as [TensorFlow Mobile](https://www.tensorflow.org/mobile/). Google used a process called [Quantization](https://www.tensorflow.org/performance/quantization), which is basically a way to represent neural network's structure using lower than 32bit floating point computer formats. In the case of TensorFlow Mobile, the 8bit fixed point format is being used.

The whole point of this library is to use it on low-power devices with limited storage since "traditional" deep neural nets can be both huge in size (hundreds of megabytes) and very demanding in computationally (which requires powerful hardware and a lot of energy).

I decided to give it a try on my [Raspberry Pi 3](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/) board running [Android Things developer preview 4.1](https://developer.android.com/things/preview/index.html). The code I used and the schematics are available [on my GitHub](https://github.com/slomin/sample-tensorflow-imageclassifier). The network used is pre trained [Google Inception model](https://arxiv.org/pdf/1409.4842.pdf).

Here is the setup I used. The camera is an old [5-megapixel module](https://www.raspberrypi.org/documentation/hardware/camera/) from 2013. The picture quality isn't too great by today's standards. I used slightly modified soldering gripper as a makeshift tripod.

![Architecture sample app first screenshot]({{ site.url }}/images/android_things_2/tensor_1.jpg){: .center-image }
*Quick and dirty setup*
{: .center-caption }

![TensorFlow first prediction]({{ site.url }}/images/android_things_2/tensor_2.jpg){: .center-image }
*It recognizes the conch shell with 51% certainty*
{: .center-caption }

Schematics of the project:

![Schematics]({{ site.url }}/images/android_things_2/tensor_schematics.png){: .center-image }

Here are some other examples of the network at work:

![Coffee mug example]({{ site.url }}/images/android_things_2/tensor_3.jpg){: .center-image }

![Orange example]({{ site.url }}/images/android_things_2/tensor_4.jpg){: .center-image }

Of course, the network isn't perfect:

![Egg example]({{ site.url }}/images/android_things_2/tensor_5.jpg){: .center-image }

The whole app's size is ~70MB. Keep in mind all the app's work is done offline, contained in a tiny RP3 body. I think future looks particularly promising with the advances in hardware (new cheaper and more powerful IoT platforms) and machine learning algorithms.
