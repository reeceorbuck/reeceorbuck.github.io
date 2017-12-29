---
layout: micropubpost
date: '2017-12-29T09:09:36.369Z'
title: An explanation of how I have this blog set up.
slug: an-explanation-of-how-i
---
This post is designed to remind myself exactly how I set this blog up, for when inevitably something goes wrong with it.

Micro.blog has two options for operating your blog, the best way is to let [@manton](http://manton.micro.blog) host it for you, but if you are more adventurous you can try to host it yourself. Many tutorials will not specify exactly which option they are helping you with so be careful.

So because I am adventurous, [reece.work](http://reece.work) is self hosted on GitHub pages and is a static Jekyll blog. Rather than having to build the site on my own machine, GitHub has a nifty feature that it builds over there, automatically once anything is committed to the repository. They also provide this service for free, and allow you to link your custom domain to it.

But that is only part of the story, as posting would still require a push to the repo, which is one step too many for easy publication from any device. The next link in the chain is a Node.js app that runs on azure that is set up to receive [micropub](https://www.w3.org/TR/micropub/) requests which it then will automatically push the post to GitHub. Another good link for explaining micropub is [here](https://indieweb.org/Micropub).

The app that I use is [webpage-micropub-to-github](https://github.com/voxpelli/webpage-micropub-to-github), which is still very early in development, and likely to really improve over time. I had to change a few things to allow it to post pictures from the micro.blog apps, and have them work correctly, so if there are updates I will need to make the changes again. If anyone stumbles across this post, you should know I really have no idea what I&#39;m doing and so I haven&#39;t done any forking or pull requests for the modifications I have made.

Okay, so simple enough so far, but obviously when you are posting from a new app you need to be able to prove that you own the website and so authorisation is required. This is the tricky part because I find it quite confusing as to where to point everything to get it to work. Apps that use the [IndieAuth](https://indieweb.org/IndieAuth) correctly such as [ownyourgram](http://ownyourgram.com) only require you to enter the name of your blog (so for me it is http://reece.work) and it will do the rest, but others ask for some other info that I am mostly guessing at. ClientID doesn’t seem to be much of an issue, it would be the url of the app that you are trying to connect, from what I can tell you can&#39;t fail if you get that one wrong. 

The micropub endpoint can be found from some html on the homepage of reece.work (see side note below) for but some apps will ask you for it anyway, so mine is the azure app which only points to my own blog - (http://micropub.azurewebsites.net/micropub/main).

Also token endpoint is [](https://tokens.indieauth.com/token), which is a service that encodes a token for you.

Now lastly, adding a json.feed to the website allows posts to appear in the micro.blog timeline once I added the site to my account.

## Side note about html tags to add to the blog home page
You need to add identifiers so indieAuth can use one to verify you. Also micro.blog requires one to prove it&#39;s your site so heres the full html of mine

```html
&lt;link rel=&quot;authorization_endpoint&quot; href=&quot;https://indieauth.com/auth&quot;&gt;
    &lt;link rel=&quot;token_endpoint&quot; href=&quot;https://tokens.indieauth.com/token&quot;&gt;
    &lt;link rel=&quot;micropub&quot; href=&quot;http://micropub.azurewebsites.net/micropub/main&quot;&gt;
    &lt;link href=&quot;mailto:reeceorbuck@me.com&quot; rel=&quot;me&quot; /&gt;
    &lt;link href=&quot;https://micro.blog/reece&quot; rel=&quot;me&quot; /&gt;
    &lt;link href=&quot;https://twitter.com/reeceorbuck&quot; rel=&quot;me&quot; /&gt;
    &lt;link href=&quot;https://instagram.com/reeceorbuck&quot; rel=&quot;me&quot; /&gt;
```

## Other questions I have: 
As in, things that I&#39;ll have to figure out as time goes on:

+ What are the best practice for images? The micro.blog feed only shows images that appear as inline html inside the content but I don&#39;t know whether they should be put in at the start or the end of text content, or if it doesn&#39;t matter. When posting images from the apps there&#39;s no way to specify where an image would appear inline.
+ I haven&#39;t figured out comments (through webmentions) yet. 
* Also when replying to someone else&#39;s post I&#39;m not sure whether this runs through my site at all.
* Editing. I can do this directly through the markdown file on the site, but am unsure how that would propagate through the micro.blog feed. Also if post editing is included in the micro.blog apps I&#39;m not sure if this will be able to integrate with my bridge solution.
* Can I tag posts?
* Not entirely sure how mentions work at all, such as if they need to be a reply to an existing post (and if not, where in the world are they), but I&#39;ll have to wait until someone actually mentions me I guess.

## Final words
So thats where I&#39;m at right now. I can post from the various micro.blog apps, editorial on my iPad and web apps such as [Quill](https://quill.p3k.io). I haven&#39;t been able to get it to work with MarsEdit yet, but I think at this stage it only works with micro.blog hosted blogs as it doesn&#39;t support micropub.



