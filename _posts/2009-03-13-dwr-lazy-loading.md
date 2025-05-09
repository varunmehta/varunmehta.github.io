---
title: "DWR and Lazy Loading"
layout: post
date: 2009-03-13
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
- java
- springframework
- dwr
star: false
hidden: false
category: blog
author: varunmehta
description: DWR and Lazy Loading
---

Time immemorial, we are all aware about the famous lazy load exceptions in Hibernate. Using a detached object does not exactly hide us from the issue. We are using DWR in our application and found that when marshalling (or unmarshalling if you insist) a detached object to JSON, [DWR](http://directwebremoting.org) was erratically trying to call a null (lazyly loaded) object, causing LazyLoadExceptions.

We did not want to use OpenSessionInViewFilter, so instead as a quick fix we did what one would first think of, "It's a demo, just eager load it!". Well the demo was over and now was the time to investigate a better solution, and we did find it.

When using DWR, there are BeanConverters available which are responsible for this marshalling process. There was one for Hiberante, called "hibernate3". http://directwebremoting.org/dwr/server/hibernate

The HibernateBeanConverter tries to avoid reading from un-initialized properties. (If you just want something that blindly reads everything then just use a plain BeanConverter).
When exporting a detached hibernate object to DWR, use type="hibernate3" and that should resolve the lazy load issues.