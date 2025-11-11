---
title: "CollectionUtils (apache commons)"
layout: post
date: 2008-06-08 17:46
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
- java
star: false
category: blog
author: varunmehta
description: CollectionUtils 
---

We had a problem at work today, where we needed to find the difference between two collections and remove the uncommon ones from the first one and add the uncommon ones from the first to the second.

This is related to hibernate add-remove-update for collections. Read here about it

* Set A = {R, G, B} 
* Set Z = {R, G, Y}

Final Set to the DB is = {R, G, Y}, well looks simple so we just send the second set Z, yeah but the catch is it needs to maintain the instance of A and finally send back A to the hibernate layer again, so all the manipulations happen on it.

Mathematically solving the problem, we need an intersection of A & Z {R, G} and a union of the relative complement of A & Z {R, G } + {Y} = {R, G , Y}

Using Java we can solve this using three approaches.
* For Loop
* CollectionUtils
* JDK collections native (1.6)

### For Loop

{% highlight java %}
private static void forLoop(List<Set<String>> all) {
    Set db = all.get(0);
    Set web = all.get(1);

    Set tempCollection = new HashSet<String>();
    tempCollection.addAll(db);

    for (String t : tempCollection) {
        if (!web.contains(t)) {
            db.remove(t);
        }
    }

    for (String t : web) {
        if (!tempCollection.contains(t)) {
            db.add(t);
        }
    }
} 
{% endhighlight %}


### CollectionUtils

{% highlight java %}
private static void collectionUtils(List<Set><String>> all) {
    Set db = all.get(0);
    Set web = all.get(1);

    CollectionUtils.retainAll(web, db);
    db.addAll(web);
}
{% endhighlight %}


### JDK Collection Native

{% highlight java %}
private static void jdkNative(List<Set><String>> all) {
    Set db = all.get(0);
    Set web = all.get(1);

    db.retainAll(web);
    db.addAll(web);
}
{% endhighlight %}


## Internals
This is what the web and db collection were made up of.

### Create Collections
{% highlight java %}
private static List<Set<String>> createCollections() {
    List<Set<String>> all = new ArrayList<Set<String>>();

    Set<String> db = new HashSet<String>();
    Set<String> web = new HashSet<String>();
    for (int i = 0; i < 10000; i++) {
        db.add(String.valueOf(i));
    }

    for (int i = 5000; i < 15000; i++) {
        web.add(String.valueOf(i));
    }

    all.add(db);
    all.add(web);

    return all;
}
{% endhighlight %}


### Main method
{% highlight java %}
public static void main(String[] args) {
    long start = 0;
    long end = 0;

    List<Set<String>> all = createCollections();

    start = new Date().getTime();
    forLoop(all);
    end = new Date().getTime();
    System.out.println("TIME BY forLoop " + (end - start));

    start = new Date().getTime();
    jdkNative(all);
    end = new Date().getTime();
    System.out.println("TIME BY jdkNative " + (end - start));

    start = new Date().getTime();
    collectionUtils(all);
    end = new Date().getTime();
    System.out.println("TIME BY collectionUtils " + (end - start));
}
{% endhighlight %}

## Results
I ran a performance test on both,
* forLoop - 18 ms
* collectionUtils - 72 ms
* jdkNative - 5 ms

So avoid using the CollectionUtils. See what is more important: cleaner code or faster code. 