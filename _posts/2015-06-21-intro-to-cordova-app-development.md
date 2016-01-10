---
comments: true
date: 2015-06-21 13:00:15+00:00
layout: post
title: Intro to Cordova app development
categories: apps
tags: [AngularJS, Bootstrap, Cordova, Javascript]
---

After a friend kept recommending Cordova for cross-platform app development, I finally caved in and decided to give it a go. I had minimal prior experience with web development (basic understanding of HTML, barely any experience with Javascript and CSS) but have been programming with C++ for years. I've been working away on an app for a few weeks now and think I'm in a pretty good position to share tips with others willing to try it out.

I found a bunch of useful blog posts explaining the fundamentals of Cordova development as I began my research, but struggled to find tutorials that pulled together technologies to make intermediate/advanced app development easy. In this short series of posts, I'll detail my chosen frameworks and development process to hopefully help others to hit the ground running.


# What is Apache Cordova?

![Cordova](/images/posts/cordova-logo.png)

Cordova is a set of tools that enable developers to package websites into apps that can be distributed through mobile app stores. This includes iOS, Android and Windows Phone. The generated apps simply create a full screen web view and display the pages the developer has packaged.

There are a bunch of solutions out there for packaging websites into mobile apps. However, Cordova has the lions share of the market and a strong development community around it. One of the great things about Cordova is how easily it can be extended. There are a wealth of plugins available that provide Javascript bindings to device sensors, such as cameras and gyroscopes, and OS features, such as sharing dialogs (email, Facebook, Dropbox, Twitter etc.).

You may have heard of PhoneGap and that it's somehow related to Cordova. There's a pretty good blog post [here](http://phonegap.com/2012/03/19/phonegap-cordova-and-what’s-in-a-name/) that explains the relationship between them, so I'll skip over it :)

# Framework research

HTML5, CSS, Javascript - the basics of those technologies were trivial to get my head around. Relying on these technologies alone is a terrible idea though. Modern web pages and apps are expected to be dynamic, full of swish animations and capable of doing a bunch of other fancy things. Like any form of programming, attempting to reinvent the wheel when smarter people have already spent countless hours developing and refining frameworks to address these problems would be a huge waste of time.

There are hundreds of Javascript frameworks out there to speed up development. It's great that the community is active enough to create this much variety, but it made it a nightmare to figure out where to begin. I spent a lot of time prototyping different solutions until I found a combination that worked for me.

So, there were a few things I was after from my UI framework/s:
	
  1. [MVC](https://en.wikipedia.org/wiki/Model–view–controller) (Model-View-Controller) or similar pattern to easily separate interface design from application logic
  2. Easy to implement and maintain
  3. A simple mechanism for page/view routing
  4. An easy way to style the app so it didn't look terrible


## AngularJS

[![](https://angularjs.org/img/AngularJS-large.png)](https://angularjs.org)

[AngularJS](https://angularjs.org) is Google's Javascript UI back-end framework. Essentially, it's a middleman between Javascript logic and HTML presentation. It enables developers to easily generate dynamic HTML pages. This can be as simple as referencing Javascript variables in HTML elements or as complex as dynamically generating entire pages. There are a bunch of other things the framework can help you with. One of the most important features for me is [page routing](https://docs.angularjs.org/api/ngRoute).

UI back-end frameworks I trialled and since moved away from include; [JQuery](http://jquery.com), [Handlebars](http://handlebarsjs.com), [Underscore](http://underscorejs.org), [Backbone.js](http://backbonejs.org). Backbone was pretty good and I used it to bring up most of my app, but I found my code was quite cumbersome. So far, Angular has proven to be a much cleaner solution.


## Bootstrap

[![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ea/Boostrap_logo.svg/2000px-Boostrap_logo.svg.png)](http://getbootstrap.com)

[Bootstrap](http://getbootstrap.com) is Twitter's UI front-end framework for webpage styling, layout and animation. As it's focussed on presentation, it is a perfect fit Angular back-end code.

Before switching to Bootstrap, I was writing my own CSS code. This was ok for a while but quickly became a problem when I wanted elements to dynamically scale based on the current device's aspect ratio and resolution. Bootstrap is the ideal framework for handling headaches like this. It's trivial to customise the default styling too.


# Conclusion

I've touched on my reasons for giving Cordova a go and briefly explained why I settled on AngularJS and Bootstrap for UI front-end, back-end and page routing. I should be able to put a few example projects for future posts :)
