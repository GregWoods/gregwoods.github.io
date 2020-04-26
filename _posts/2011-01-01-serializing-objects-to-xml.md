---
id: 122
title: Serializing Objects to XML
date: 2011-01-01T22:25:17+00:00

layout: single

guid: http://gregwoods.co.uk/?p=122
permalink: /2011/01/serializing-objects-to-xml/
categories:
  - Programming
tags:
  - 'c#'
  - xml
---
Paste the following C# code directly in [LINQPad](http://www.linqpad.net/), change language to 'C# Program' and run it.

```c#
void Main() {
    //create test object hierarchy with data
    var people = new List<Person>() {
        new Person() {
            Forename = "Greg",
            Surname = "Woods",
            Hobbies = new List<Hobby>() {
                new Hobby("Sailing"),
                new Hobby("Skiing")
            }
        },
        new Person() {
            Forename = "Alison",
            Surname = "Woods",
            Hobbies = new List<Hobby>() {
                new Hobby("Sleeping")
            }
        }
    };

    //do the serializing magic
    var x = new System.Xml.Serialization.XmlSerializer(people.GetType());
    var output = new StringBuilder();
    var xmlWriterSettings = new XmlWriterSettings() {
        Indent = true,
        IndentChars = ("\t"),
        CloseOutput = true
    };
    XmlWriter writer = XmlWriter.Create(output, xmlWriterSettings);
    x.Serialize(writer, people);
    writer.Close();

    //display the output in LINQPad
    output.ToString().Dump();
}

//Common classes used for the Serialize and Deserialize code examples
public class Person {
    public string Forename { get; set; }
    public string Surname { get; set; }
    public List<Hobby> Hobbies;

    public Person() {
        Hobbies = new List<Hobby>();
    }
}

public class Hobby {
    public string Name {get; set; }
    public Hobby()     {}        //required for serialisation to work, even though not used by my test code
    public Hobby(string name) {
        this.Name = name;
    }

```
