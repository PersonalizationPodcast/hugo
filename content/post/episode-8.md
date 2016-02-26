+++
date = "2016-02-25T12:21:07-05:00"
tags = ["Personalization"]
title = "Episode 8: Context, Context, Context"
+++

# Context, Context, Context

<iframe width="100%" height="166" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/248948406&amp;color=ff5500&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false"></iframe>

If Content is King, then Context is Queen. Personalization is all about matching
the right content or messaging to the right person, and doing that means you need
to know something about who that person is. In fact, the more you know, the more
likely you are to be successful.

That's not to say that all context is created equal though. Depending on your
organization and your audience, different pieces of information may be critical
or close to meaningless. As a simple example, a retailer may be heavily effected
by a customer's local weather. Cold and rainy, you may need a rain coat. Warm and
Sunny? Time for the beach!

Today's episode is all about cataloging the *kinds of things* that we can know
about the consumers of our digital experiences. The list is quite broad and it
will range from the fairly straight forward and obvious, into perhaps surprising
and sometimes creepy.

But first, let's look at the news to me.

## It's News to Me

### eTail West and Browser Push Notifications

Personalization has been an important strategy for retailers longer than for anyone else. In many ways, Amazon was the original pioneer of personalization with their early product recommendations, and many sellers and personalization vendors have latched onto that idea.

Well, [eTail West](http://etailwest.wbresearch.com/) is just wrapping up this week, and many sessions focussed on data, omni-channel, personalization and related topics. Before looking at an interesting case study though, I came across a request on eTail's website to subscribe for push notifications. The only place I'd seen this before was Facebook, but in case you didn't know, it's now possible to send push notifications directly through a browser. This has generally just been the realm of mobile applications, so this opens up some interesting doors for marketers, though I'm not convinced it will really catch on yet.

In any case, I signed up for the same vendor eTail is using, which is called [PushCrew](https://pushcrew.com/), and have put it up on personalizationpodcast.com at least temporarily to try it out. You can go there and have a look if you're interested. I don't see any capabilities for targeting or personalizing push notifications at the moment, but clearly it would be possible to do this and may be of great interest to some of you out there.

### [How Sephora pairs individual, loyalty data to optimize segmentation](http://www.luxurydaily.com/how-sephora-pairs-individual-loyalty-data-to-optimize-segmentation/)
By Alex Samuely

> “[Data] is kind of a currency to us,” said Angel Singh, director of product
> analytics and optimization at Sephora. “We have a lot of data on our clients
> and we’re trying to figure out how to leverage it.”

...

> Data is imperative when it comes to pinpointing how best to target consumers, since many of them complete shopping journeys across multiple devices.

> “When we think about our clients, we know that they don’t just go into the store and buy something,” Ms. Singh said. “There is a journey.”

> Twenty-three percent of shoppers compare prices on mobile while standing in-store and before going to a bricks-and-mortar location. Additionally, 24 percent engage with a retail app each week, leaving a prime opportunity for marketers to connect with loyal customers.

> Sephora has extended its omnichannel reach to include optimized emails, a new subscription box, a mobile app and mobile Web site.

> The brand also offers a popular loyalty program, Beauty Insider, which rewards users with points for each dollar spent. Points can then be redeemed for sample-size products.

Now we come to the clincher:

> Sephora is focusing on digging up real-time data, which has previously proven to be a trickier process due to silos. Having access to individual data would help the brand – as well as in-store associates – give shoppers a personalized experience based on their *skin types, beauty regimes and past purchases.*

> “We want to recognize everybody,” Ms. Singh said.

I pull that quote specifically because it captures the point of this episode: Context. Sephora wants to know who people are, and for them that means some very specific things. For your organization, it will certainly be different, but narrowing down which variables matter is the key.

## All about Context

So, what can you know about your visitors? It turns out that it's really quite a lot. We're going to start by looking at the raw materials, and work outward to see what can be learned based on that.

So, let's start with a simple HTTP header which may look something like this:

```
GET /tutorials/other/top-20-mysql-best-practices/ HTTP/1.1
Host: net.tutsplus.com
User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.1.5) Gecko/20091102 Firefox/3.5.5 (.NET CLR 3.5.30729)
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Referer: https://www.google.com
Keep-Alive: 300
Connection: keep-alive
Cookie: PHPSESSID=r2t5uvjq435r4q7ib3vtdjq120
Pragma: no-cache
Cache-Control: no-cache
```

(source: [tutsplus.com tutorial](http://code.tutsplus.com/tutorials/http-headers-for-dummies--net-8039))

From this very simple request header, the spec for which was last edited in 1994, we can learn an awful lot:

### User Agent
This short line of text can be hard to read, but thankfully others have done the hard work of being able to do this, and by running this text through various services such as [UA Detector](http://uadetector.sourceforge.net/), we can learn things like:

- Browser
- Browser Version
- Device
- Operating System

### Accept-Language
What language has the visitor set their browser for? This is a great source of information for what they may prefer and allows you to give them content in that language.

### Referrer
Where did they come from? Search Engine? Social Media? Another page on your site? An Ad?

On top of the page they came from, you can also look at parameters in the url such as Campaign and Source, which are often used by analytics, but can also be used for personalization.

### Cookies
First and 3rd party cookies are also passed in here. Cookies are how the browser and the server maintain "state", which means that the server can recognize the same person from page to page. This becomes incredibly important in a moment when we talk about behavior.

### IP address
While not always in the headers, we have IP addresses available from the request itself. While the IP Address itself may look like just numbers, we can use it to infer, with relatively good accuracy, the geographic location of the visitor using a database such as the one from Maxmind.

You can [test it for yourself to see how it does](https://www.maxmind.com/en/locate-my-ip-address). For me it nailed my postal code, city and state. It also returned a latitude and longitude, but missed me by about 5 miles. This is because it's the lat/long for the zip code and no closer, so you shouldn't expect huge precision from this method.

Other services, such as [Demandbase](demandbase.com) build databases of IP addresses for organizations and can determine what company is viewing this page, giving you access to information like Company Name, company size, industry, number of employees and more. This *huge* for B2B companies.

### Geography
Speaking of geolocation, we can also ask the visitor to share their more precise location. This is often done in mobile applications, but can be done on the desktop as well.

### Past Behavior
By keeping track of who we've seen and what they did, now we can build up a picture of who this person is and what they're really looking for. This may well be the holy grail of context for the majority of organizations, but is also considerably more difficult.

Future episodes will discuss machine learning and how this can be applied, but simpler rules based approaches can also be extremely valuable. For example, if a visitor has already bought one product, you can stop showing them that product and show others that are of interest. If they've spent most of their time on a particular topic on a news site, you might show them more news from that subject.

### What if Cookies get cleared?
Usually if someone clears their cookies, if they come to your site again they will look like a brand new user.

A variety of technology exists to try to get around this, generally referred to as "device fingerprinting". [The Wikipedia page for Device Fingerprinting](https://en.wikipedia.org/wiki/Device_fingerprint) does a good job of explaining what it is and the privacy violation risks. That's going to be a topic of a future episode, but for the time being, think twice before doing something like this.

### Ask them questions
Everything above is basically "inferred" information from what you see a visitor do. You can also just ask them. This is generally done when a user registers for a site and needs to fill in things like name, email address, age, etc. You can also employ the technique of "progressive profiling", which means you ask for a little more information each time. LinkedIn is very good at this.

You can also effectively ask questions without requiring a log in. One great example is by providing links in a navigation structure which request that someone identify which type of customer they are. This can then be captured and as long as you still have that visitor cookied, you can remember their selection.

### Behavior Off-site
#### 3rd Party Cookies
[Little Blue Book](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCDA/pdf/Misc/bluekai-little-blue-book.pdf) provides an extensive encylopedia of data sources that can be tapped into, largely focussed on 3rd party advertising cookies.

These can be great, but beward 3rd party cookie decline.

#### Social Mining
An example company is [Clearbit](clearbit.com). Go there and type in your email address and see what you get. For me it accurately nailed my website, company, twitter handle, as well as information about my company.

![Clearbit Data Lookup](/images/clearbit.png)

What's more, from knowing my twitter handle, one could go and look at my past tweets, who I follow, what I like and dislike (at least, what I've shared on twitter.)

This whole area of social mining is a huge field and there's much more depth possible there.

#### Social Sign-on
Besides the public facing data available from sites like Facebook and Twitter, if you ask a customer to sign on using a social sign-on widget like Facebook, Twitter or Google, or using a service like [Janrain](janrain.com) or [Gigya](gigya.com), you can ask for visitors to share additional information from their social profiles.

#### SpyJax
Before leaving this session, I want to call out a crazy little trick I discovered a while back that has been dubbed "[spyjax](https://davidwalsh.name/ajax-evil-spyjax)". This is a technique that uses only javascript and css, taking advantage of the fact that browsers will make visited links a different color by default. Using Javascript, you can then read in if that color has been changed and discover what websites a user has been to. Now, you have to hardcode this list and it's of limited value. It's also an awful idea and a violation of privacy. It's still a facinating little trick though.
