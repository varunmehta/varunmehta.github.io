---
title: "DATETIME vs TIMESTAMP vs DATE & TIME - Part 2"
layout: post
date: 2008-08-14
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
- java
- mysql
star: false
hidden: false
category: blog
author: varunmehta
description: DATETIME vs TIMESTAMP vs DATE & TIME - Part 2 
---

Read my first part. 

Ok now the test are run and the results are out, I know we are all excited to know them, and I'm equally eager to print them too!!

The test did a simple select * from the tables.

{% highlight java %}
  public void fetchAll() throws Exception {
  String SQL1 = "SELECT * FROM dateandtime";
  String SQL2 = "SELECT * FROM datetime";
  String SQL3 = "SELECT * FROM timestamps";

  long start = 0;
  long end = 0;

  System.out.println("ONE");
  start = new Date().getTime();
  selectQuery(SQL1);
  end = new Date().getTime();
  System.out.println(" SQL 1 - dateandtime " + (end - start));

  System.out.println("TWO");
  start = new Date().getTime();
  selectQuery(SQL2);
  end = new Date().getTime();
  System.out.println(" SQL 2 - datetime " + (end - start));

  System.out.println("THREE");
  start = new Date().getTime();
  selectQuery(SQL3);
  end = new Date().getTime();
  System.out.println(" SQL 3 - timestamps " + (end - start));
}
{% endhighlight %}


The time to fetch kept on reducing with every subsequent calls, due to MySQL caching

```
SQL 1 - dateandtime 4526 ms
SQL 2 - datetime 2852 ms
SQL 3 - timestamps 3577 ms

SQL 1 - dateandtime 4168 ms
SQL 2 - datetime 2467 ms
SQL 3 - timestamps 3073 ms

SQL 1 - dateandtime 4080 ms
SQL 2 - datetime 2346 ms
SQL 3 - timestamps 3130 ms

SQL 1 - dateandtime 3949 ms
SQL 2 - datetime 2419 ms
SQL 3 - timestamps 3043 ms 
```

So looks like `DATETIME` wins in fetching speed.