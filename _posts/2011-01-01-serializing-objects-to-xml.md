---
id: 122
title: Serializing Objects to XML
date: 2011-01-01T22:25:17+00:00
author: Greg Woods
layout: single
classes: wide
guid: http://gregwoods.co.uk/?p=122
permalink: /2011/01/serializing-objects-to-xml/
categories:
  - Programming
tags:
  - 'c#'
  - xml
---
Paste the following C# code directly in [LINQPad](http://www.linqpad.net/), change language to &#8216;C# Program&#8217; and run it.

<!-- code formatted by http://manoli.net/csharpformat/ -->

<pre class="csharpcode"><span class="kwrd">void</span> Main() {
    <span class="rem">//create test object hierarchy with data</span>
    var people = <span class="kwrd">new</span> List&lt;Person&gt;() {
        <span class="kwrd">new</span> Person() {
            Forename = <span class="str">"Greg"</span>,
            Surname = <span class="str">"Woods"</span>,
            Hobbies = <span class="kwrd">new</span> List&lt;Hobby&gt;() {
                <span class="kwrd">new</span> Hobby(<span class="str">"Sailing"</span>),
                <span class="kwrd">new</span> Hobby(<span class="str">"Skiing"</span>)
            }
        },
        <span class="kwrd">new</span> Person() {
            Forename = <span class="str">"Alison"</span>,
            Surname = <span class="str">"Woods"</span>,
            Hobbies = <span class="kwrd">new</span> List&lt;Hobby&gt;() {
                <span class="kwrd">new</span> Hobby(<span class="str">"Sleeping"</span>)
            }
        }        
    };    
    
    <span class="rem">//do the serializing magic</span>
    var x = <span class="kwrd">new</span> System.Xml.Serialization.XmlSerializer(people.GetType());
    var output = <span class="kwrd">new</span> StringBuilder();
    var xmlWriterSettings = <span class="kwrd">new</span> XmlWriterSettings() {
        Indent = <span class="kwrd">true</span>,
        IndentChars = (<span class="str">"\t"</span>),
        CloseOutput = <span class="kwrd">true</span>
    };
    XmlWriter writer = XmlWriter.Create(output, xmlWriterSettings);
    x.Serialize(writer, people);
    writer.Close();
    
    <span class="rem">//display the output in LINQPad</span>
    output.ToString().Dump();
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
    <span class="kwrd">public</span> Hobby()     {}        <span class="rem">//required for serialisation to work, even though not used by my test code</span>
    <span class="kwrd">public</span> Hobby(<span class="kwrd">string</span> name) {
        <span class="kwrd">this</span>.Name = name;    
    }    
}
</pre>