---
title: "Multi-Tenancy"
layout: post
date: 2010-10-05
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- agile
- technical
star: false
hidden: false
category: blog
author: varunmehta
description: Multi-Tenancy
---

I'm not trying to redefine the concept or write a new white paper on multi-tenancy. Most of the article points you to few of the best articles and white papers on the internet that I've come across. Different companies have different approaches and ideas on how to handle this. I try to handle this from a data separation perspective first and then take it to the application level.

If you are new to the concept of SaaS itself, then you have some reading to do, before you read further. Can I suggest [Wikipedia](http://en.wikipedia.org/wiki/SaaS) to being with first

Working on a SaaS model, multi-tenancy plays a major role to allow (their) multiple clients to live on the same system. There are various white papers and articles out there on the internet discussing on strategies on how to implement them. I've listed a few for your bed time reading;
* [http://en.wikipedia.org/wiki/Multitenancy](http://en.wikipedia.org/wiki/Multitenancy)
* [http://msdn.microsoft.com/en-us/library/aa479086.aspx](http://msdn.microsoft.com/en-us/library/aa479086.aspx)
* [http://wiki.developerforce.com/index.php/Multi_Tenant_Architecture](http://wiki.developerforce.com/index.php/Multi_Tenant_Architecture)

Let me try to give you a real world analogy on what multi-tenancy is and what issues you face with it.

Consider your self as a big rental management firm, who can rent all the apartments in the building, so how's that with a software?

But my problem was how to implement it in my application with minimum effort or interference from other developers. I did not want multi-tenancy code seepage into my regular code. The whole point is to keep is as sanitized as possible. One of the really quick and dirty ways was the make every front end developer pass that as a parameter to the backend, but that is not something any developer would want to introduce in his app.

 * It's an added dependency across the application for every developer to pass the parameter
 * If a developer forgets to pass the parameter, the system starts to fail.

We want to keep the developer interference as minimum as possible (read none!), and keep the application as simple as possible to transform from a single to multi-tenant back and forth. To handle this we use the HttpSessions, ServletFilter & ThreadLocal.

I'll try to cover the code in the next post, but here is how the flow of logic will occur.

1. When the user logs in, get the "tenant code" and store it in the user's web session
2. Next the request when reaches the filter, the "tenant code" is read and stored in a ThreadLocal
3. This ThreadLocal is accessible through out the "request roundtrip".
4. Use hibernate to set the "tenant" in the Filters and get the filtered data.
