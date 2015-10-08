---
layout: post
title: "Useful tools: pt-archiver"
date: 2015-10-07
---

If you have found yourself [using mysql as a job queue](https://blog.engineyard.com/2011/5-subtle-ways-youre-using-mysql-as-a-queue-and-why-itll-bite-you/), eventually you have to deal with the unpleasantness of removing old data from your database.  

Don't do this:

{% highlight sql %}
delete from tablename where created < 'whatever'
{% endhighlight %}

Depending on your database, writes may get locked out and if nothing else your DBA's will thank you for not making the mysql slaves lag behind master.

A nice tool for jobs like this is Percona's [pt-archiver](https://www.percona.com/doc/percona-toolkit/2.1/pt-archiver.html).  Its a beautifully simple tool that does one thing and does it well.  It can move data out of your database efficiently and without negatively impacting app performance.

I am using something like the following to archive data into a read only analytics database.
{% highlight bash %}
pt-archiver --source=... --dest=... --columns=just,the,ones,i,need \
 --limit 1000 --commit-each --no-check-columns --where "1=1"
{% endhighlight %}

Hope this helps someone find [pt-archiver](https://www.percona.com/doc/percona-toolkit/2.1/pt-archiver.html).