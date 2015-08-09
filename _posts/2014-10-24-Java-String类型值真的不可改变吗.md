---
layout: post
title:  Java String类型值真的不可改变吗
description:    ""
tags:   [Java, String]
image:
  background: triangular.png
---

一直认为java 中String类型的值不能修改，主要是因为String是final的，而且里面没有设置值的set方法。但是可以通过反射机制改变值。

例1:

{% highlight java %}
public class Test {
	public static void main(String[] args) throws Exception {
    	String s="0123456789";
    	System.out.println("改变前:s=" + s);
    	Field f = s.getClass().getDeclaredField("value");
    	f.setAccessible(true);
    	f.set(s, new char[]{'a', 'b', 'c'});
    	System.out.println("改变后:s=" + s);
	}
}
{% endhighlight %}

例1	结果:

{% highlight java %}
改变前:s=0123456789
改变后:s=abc
{% endhighlight %}

例1 原因:

String 类里有个 private final char value[]成员变量, String 类的值都是保存在这个value属性中。可以通过反射来改变这个值，达到改变String类值的目的。同理，通过这种方式，我们可以改变自定义对象的私有成员变量。