---
layout:	post
title:	ping hosts文件各个配置项
description:	""
tags:	[linux, shell, ping]
---

{% highlight yaml %}
#!/bin/bash
#pingall
cat /etc/hosts | grep -v '^$' | grep -v '^#' | while read IP DOMAINS
do
    for DOMAIN in $DOMAINS 
        do 
            ping -c1 $DOMAIN > /dev/null  2>&1
            #echo $DOMAIN "("$IP")" "["$?"]"
            printf "%-50s%-20s%d\n" $DOMAIN $IP $?
        done
done
{% endhighlight %}