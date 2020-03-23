---
id: 137
title: Deserializing XML to Objects
date: 2011-01-01T22:34:17+00:00

layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=137
permalink: /2011/01/deserializing-xml-to-objects/
categories:
  - Programming
tags:
  - 'c#'
  - xml
---
Save the output of the [Serialize](http://gregwoods.co.uk/2011/01/serializing-objects-to-xml/) post to a file called sample.xml

Paste the following C# code directly in [LINQPad](http://www.linqpad.net/), change language to 'C# Program' and run it.

<!-- code formatted by http://manoli.net/csharpformat/ -->

<pre class="csharpcode"><span class="kwrd">void</span> Main()
{
    var streamReader = <span class="kwrd">new</span> StreamReader(<span class="str">@"c:\sample.xml"</span>);
    var people = <span class="kwrd">new</span> List&lt;Person&gt;();
    var x = <span class="kwrd">new</span> System.Xml.Serialization.XmlSerializer(people.GetType());
    var objects = x.Deserialize(streamReader);

    objects.Dump();
}

<span class="rem">//Common classes used for the Serialize and Deserialize code examples</span>
<span class="kwrd">public</span> <span class="kwrd">class</span> Person {
    <span class="kwrd">public</span> <span class="kwrd">string</span> Forename { get; set; }
    <span class="kwrd">public</span> <span class="kwrd">string</span> Surname { get; set; }
    <span class="kwrd">public</span> List&lt;Hobby&gt; Hobbies;
    
    <span class="kwrd">public</span> Person() {
        Hobbies = <span class="kwrd">new</span> List&lt;Hobby&gt;();
    }
}

<span class="kwrd">public</span> <span class="kwrd">class</span> Hobby {
    <span class="kwrd">public</span> <span class="kwrd">string</span> Name {get; set; }
    <span class="kwrd">public</span> Hobby()     {}        <span class="rem">//required for serialisation, even though not used by my test code</span>
    <span class="kwrd">public</span> Hobby(<span class="kwrd">string</span> name) {
        <span class="kwrd">this</span>.Name = name;    
    }    
}
</pre>