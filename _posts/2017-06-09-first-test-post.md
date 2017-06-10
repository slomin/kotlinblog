---
layout: post
title: First post - Hello World!
comments: true
---
Hi! This is first test post on this blog!

Testing embedded YouTube video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/NqlRg1_bCC4" frameborder="0" allowfullscreen></iframe>

### Code

This is just a sample of some `Kotlin` code snippet.

{% highlight java %}
// Standard onClickListener
view.setOnClickListener(object : View.OnClickListener {
    override fun onClick(v: View?) {
        toast("Hello World!")
    }
})

// Proper "Kotlinish" onClickListener (with Anko)
view.setOnClickListener { toast("Hello World!") }
{% endhighlight %}

More to come...
