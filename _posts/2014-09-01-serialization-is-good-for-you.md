---
layout: post
title: "Serialization is good for you!"
description: "Trying to address some myths and misconceptions about serialization"
category: articles
tags: [programming, java]
---

I decided to write this short blog post to try to address some of the myths and misconceptions about serialization as well as share my point of view.  
<br>
I’ll concentrate on Java here but a lot of it will be similar for other languages.

###What is serialization 
When we talk about serialization we mean specifically object serialization where a java object is written as a sequence of bytes (binary or not) so that it can be persisted or transmitted and eventually deserialized back to replica of original object.  
<br>
Serialization will include on only objects data but also information about it’s type and types of data stored in the object.  
<br>
Serialization is most often used when transmitting objects across systems boundary eg. API returning JSON or XML. By returning object in common format like JSON we are making it easy for any client to deserialize it.  
<br>
[Java Serialization Tutorial](http://www.tutorialspoint.com/java/java_serialization.htm)

###Myth #1 - Serialization is slow
Sure there is a performance hit when you serialize an object, but you also get a performance hit when accessing almost anything else - disk, network resource, database.
<br><br>
Know your libraries - some serialization libraries can be orders of magnitude faster than others. Also you can find highly specialized and optimized libraries targeting only certain types of serialization.
<br><br>
Good article about high performance serialization - 
[Java Best Practices High Performance](http://www.javacodegeeks.com/2010/07/java-best-practices-high-performance.html)
<br><br>
Some good benchmark graphs to look over - 
[Benchmarking](https://code.google.com/p/thrift-protobuf-compare/wiki/Benchmarking)
<br><br>
Also very important thing to remember is that premature optimization is the root of all evil - so usually you shouldn't get too concerned with it until you have some data to back it up.

<iframe width="560" height="315" src="//www.youtube.com/embed/mFhiaTW2jgg" frameborder="0" allowfullscreen></iframe>

###Myth #2 - it’s not worth the overhead - my objects are simple
Sure your objects are simple now - so you’re tempted to just use string concatenation or StringBuilder to create that XML.

{% highlight java %}
return “<person><firstName>” + person.firstName + “</firstName><lastName>” + person.lastName + “</lastName></person>”;
{% endhighlight %}

This is a slippery slope and a very bad idea.  
Before you know it your object grows, it includes arrays of other objects and your code becomes unmaintainable soup that’s a breeding ground for bugs.
<br>
And starts looking more like that:
{% highlight java %}
StringBuilder xmlString = new StringBuilder();
xmlString.append("<person>");
xmlString.append("<firstName>");
xmlString.append(person.firstName);
xmlString.append("</firstName>");
if(person.bankAccount!=null){
	xmlString.append("<bankAccount>");	
	xmlString.append("<accountNumber>");
	xmlString.append(person.bankAccount.accountNumber);
	xmlString.append("</accountNumber>");
	xmlString.append("</bankAccount>");	
}
xmlString.append("</person>");

return xmlString.toString();
{% endhighlight %}
<br>
You get the point - this is as bad as it looks - and it'll only get worse over time, so do everyone a favour and stop it!
<br><br>
Blow code (using Jackson XML) will stay largely the same regardless how complicated your object gets over time.

{% highlight java %}
XmlMapper xmlMapper = new XmlMapper();
return xmlMapper.writeValueAsString(person);
{% endhighlight %}

###Myth #3 - I need more control over my output
All good serialization libraries provide a way for you to control your output - usually using attributes.

{% highlight java %}
@XmlAccessorType(XmlAccessType.FIELD)
public class Person{
        @XmlAttribute
        protected String firstName;

        @XmlAttribute
        protected String lastName;
}
{% endhighlight %}

this will produce the following xml:

{% highlight xml %}
<person firstName=”” lastName=””></person>
{% endhighlight %}

In 95% of cases control you are given is enough. For cases when it’s not - most libraries will let you create custom serializers giving you full control of the output.

###Summarizing
Serialization allows you to reduce the amount of code you have to write and test - thus reducing time and effort needed to add new functionality as well as reducing number of bugs - this is HUGE benefit in itself.  
<br>
Using a good library allows you to easily add support for other formats with little or no code - XML, JSON, YAML you name it they got it!  
<br>
In most cases popular libraries will outperform the code you wrote (if not then you should extract it and put it on github for others to benefit).

###And remember!

<figure>
	<img src="http://cdn.meme.am/instances/500x/54722260.jpg">
</figure>







