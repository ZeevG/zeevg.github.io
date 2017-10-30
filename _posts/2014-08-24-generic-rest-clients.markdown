---
layout: post
title: Generic REST Clients
date: '2014-08-24 04:55:00'
tags:
- python
- rest
- web
- thoughts
---



Below is a repost of a conversation I had in the Curtin University Computer Science Facebook page.

I originally wrote this post in October 2013 and I'm still convinced a robust generic REST client would be a really good thing. It seems like the next logical step towards increasing the accessibility of data throughout the web, the end goal being a simple "plug and play" API interface that even novice programmers can use.

The reason I am posting this now is because I came across [Valor](https://github.com/jacobian/valor) - A Python HTTP client for APIs represented by JSON Schema by [Jacob Kaplan-Moss](http://jacobian.org/).

>Awesome project I just thought of!

>It's long so bear with me.

>Many web services have RESTful API's which return JSON data.  I use them all the time, and I think it's one of the best things about the web.

>When interacting with these services, you could just parse the JSON, get the data you need and leave it at that. But it's much nicer to bundle it all up in a wrapper, maybe even open source it. Then you will always have an easy to maintain interface to the API.

>This is all fine, but then, the internet is full of awesome data so you want to use another JSON API. You pretty much copy and paste your old API wrapper change what data structure/types it holds, the request urls and then you have a wrapper for the next service.

>So now you have two... and two to maintain.

>This is where I am at and I want to make a wrapper for a third service. So I am thinking perhaps it would be possible to write a generic JSON API client which you feed some kind of map/schema of the expected response and it will be that wrapper.  I also thought this could be a good chance to use metaclasses which I have been wanting to play with.

>Most of these services use predictable urls and simple response data so I think it is a doable project.

>I think this could be really useful for a lot of people and after a quick 2 min google there doesn't seem to be anything doing this.
Thoughts?


I did spend some time on this project (although not nearly enough).  It was harder than I initially expected (like most things).  One of the main problems was that there is no standard response formats for RESTful APIs.

If fact, depending on who you talk to REST can mean nearly completely different things!  Broadly though, there tends to be two types of APIs which are referred to as RESTful. Those that return text and those that return hypertext. Roy Fielding wrote the [original dissertation](http://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm) describing REST and is [quite vocal](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven) on this topic.

This distinction is very important for a generic REST client because hypertext APIs potentially don't require a schema at all.  A hypertext API should be self describing, and should be browsable by any hypertext client - with no prior knowledge of the API except an endpoint URL!

In an attempt to clearly differentiate these hypertext APIs (which are actually way more awesome) from boring non hypertext RESTful APIs the [HATEOAS](http://en.wikipedia.org/wiki/HATEOAS) (Hypermedia as the Engine of Application State) term is used.  To blatantly quote Wikipedia.
>HATEOAS is a constraint of the REST application architecture... The principle is that a client interacts with a network application entirely through hypermedia provided dynamically by application servers.

>A REST client needs no prior knowledge about how to interact with any particular application or server beyond a generic understanding of hypermedia. 

>By contrast, in a service-oriented architecture (SOA), clients and servers interact through a fixed interface shared through documentation or an interface description language (IDL).

Valor is orientated towards non hypertext APIs, this is the reason it requires a schema description of the API - referred to as an IDL in the quote above.  Valor is still great, it achieves what I wasn't able to do, and nicely solves the problem I was describing in my original Facebook post.

However I'm convinced HATEOAS APIs are where we should be going.  This would bring us closer to the magic place where data flows effortlessly between services.  From this point building a generic REST client would be simple.

