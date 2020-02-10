---
layout: post
title: "My First Post"
date: 2020-01-05
---

I'm excited to begin blogging!

You may be familiar with the `COPY` SQL command, which allows you to copy data to and from files (in this case, I wanted it to be in a CSV format). It works like this:

{% highlight sql %}
COPY (SELECT * FROM dogs)
TO '/absolute/path/dogs.csv'
WITH (FORMAT csv, HEADER true);
{% endhighlight %}
