---
layout: project
title: WebSockets Demo
heading: WebSockets Demo
tagline: Look into my WebSockets
description: A fun WebSockets demo application showcasing both server
  and client-side WebSocket interaction.
github:
  title: Fork on Github
  href: https://github.com/JangoSteve/websockets-demo
---

# WebSockets Demo

This is a demo app to accompany the [WebSockets and Methods for
Real-Time Data
Streaming](http://www.meetup.com/SEM-JS/events/115354852/) talk at the SE Michigan JavaScript users
group.

<h2><a href="/websockets-slides" target="_blank">WebSockets Slides</a></h2>

## Background

This app consists of a server and a client. The server happens to be
written in NodeJS, since this is a demo for a JavaScript users group
after all, but it could have easily been writtin in Ruby, Python, or
some other language and the lessons would remain the same.

The client is a single HTML webpage, which can be opened directly in
the browser. The page uses the HTML5 WebSocket spec to connect and
stream data to and from the server in real-time.

## Requirements

This app is intended for demonstration purposes, and thus the front-end
uses no 3rd-party WebSockets library, such as Socket.IO; it's just
plain, good old fashioned JavaScript. As a result, this should not be
considered cross-browser compatible. It's been built and tested using
Chrome on Mac OSX.

To run the server, you will need to have [NodeJS](http://nodejs.org/)
and [NPM](https://npmjs.org/) installed.

## Getting Started

Grab the repo from Github:

{% highlight bash %}
git clone git://github.com/JangoSteve/websockets-demo
{% endhighlight %}

Then `cd` into the project's root directory and install:

{% highlight bash %}
cd websockets-demo
npm install
{% endhighlight %}

Once everything is installed, run the server:

{% highlight bash %}
npm start
{% endhighlight %}

And finally, open the client page (assuming Chrome is your default
browser; if not, try browsing to the page in your Finder, right click,
and open with Chrome (then again, it may run in Firefox or some other
browser too, who knows)):

{% highlight bash %}
open index.html
{% endhighlight %}

To see the WebSockets in action, try opening the client page a bunch of
times in different tabs:

{% highlight bash %}
open index.html
open index.html
open index.html
open index.html
open index.html
open index.html
open index.html
open index.html
{% endhighlight %}

Optionally, you may also open the client page over the
network, e.g. locally or over wifi, if you have the server
running. Visit http://localhost:8080, or look
up your local network address (e.g. 192.168.1.1) using `ifconfig`
and visit your address on port 8080. 

## Client Modules

The idea of the app is that everyone who opens the page will be
connected to the same WebSocket server. The WebSocket server simply
provides the plumbing, via WebSockets, to enable clients to pass and
receive messages to and from every other connected client.

A message is an arbitrary JSON representation of some data. The only
required data in a messaged created by a client module (for the purposes
of this app), is a `type` attribute.

Besides the type attribute, the only other attribute which has any
special meaning to the server is the optional `target` attribute. If
included, the server will only send the event to the client with the id
specified by the target. If the `target` attribute is not present, the
event will be sent to all connected clients.

There are three client modules included by default in this app that are
required for the app to function:

* connected.js - receives the connected event when the client connects
  to the WebSocket server.
* connection.js - receives an event that is sent by the server each
  time another client connects.
* closed.js - sends an event to the server when a client disconnects,
  and receives the event for the remaining clients.

In addition to the required client modules above, one other module is
included simply as a demonstration of what an add-on module would look
like:

* click.js - allows clients to click the squares representing other
  clients to send them a `click` type event.

The way the app works is that, anyone could create a new module and
include it on their own client page, allowing them to send arbitrary
events to other users.

The author could then distribute their client module to other users, and
any who also include the module in their client page would be able to
receive the events (technically all clients would receive the events
already, they would just need to include the module for their client to
do anything as a result of receiving the event).
