---
layout: post
title:  "A Word on Scalability: Scope and You"
date:   2025-01-16 04:09:57 +0100
categories: jekyll update
---

As promised in my earlier blog post on <a href="https://adamgguk.github.io/jekyll/update/2025/01/16/audioFeedback.html"> my audio project</a>, this blog post will be about scalability in games programming, how it's achieved, and its importance.<br><br>

<b>What is scalability?</b><br><br>
The word scalability, according to Oxford Languages, means <i>"the ability of a computing process to be used or produced in a range of capabilities".</i> Specifically, this refers to a piece of code's ability to handle increasing or varying levels of demands, according to its utility.
For online games, this can, for instance, refer to properly managing server load (more players), while hardware scalability refers to designing the game to run properly on a wide range of devices and platforms.<br><br>
The focus of this blog post, however, is on code scalability. In broad terms, code scalability refers to a series of principles a programmer should follow, in order to create code that works in a wide variety of scenarios/scopes, as well as code that will accomodate the increase of a game's scope.<br>
Scalability also has a wide range of benefits, including ease of adding features, simplified debugging, reduction of technical debt, and the ability of less technically inclined people to tweak the code (not that I'd ever let an artist touch MY code).<br><br>

<b>An example of scalability</b><br><br>
<i>QUICK NOTE: I will be using Unity-specific C# for these examples, but the principles apply for any OOP language.</i><br><br>
Let's take a look at some examples of good scalability and bad scalability.<br><br>
Let's say we're building an enemy for an RPG. The simplest way to implement this enemy would be something like this:<br>
<br>
<i>
public class Enemy<br><br>
{<br>
string enemyName = "Goblin" <br>
int level = 5;<br><br>
 
 &nbsp;&nbsp;<i> public void Attack()<br>
 {<br>
  Debug.Log("Goblin attacks!") <br>
 }<br><br>
}<br><br></i>
This code is very barebones, but implements an enemy class. However, it's very, very bad and inflexible code - so bad, in fact, that the code-savvy among us are probably screaming furiously at the screen.<br>
In short order, the issues with the code are:<br><br>
<b>Hard-coded, private values</b><br><br>
We have an Enemy class, however both its name and level are hard-coded, which means it's part of the code. Just like magic numbers, this is very bad for a few reason. The first reason is that we can't manipulate it, and since we can't manipulate it, we can't test/balance it without going into the code and changing the value every time. It's also hard for outsiders and non-coders to read, compared to a variable with a fitting name, such as "enemyName" or "enemyLevel".<br><br>
This leads to the second point - the code is hidden away due to its access level. Keeping as many variables private as possible is good, though in this case it's bad. What if your designer wants the name to "Orc"? They'd have to go into the code to do it. With the "public" keyword, we could expose the variable in the editor, thus making it easier to change.<br>
In order to make the class scalable, we would create a new class that <b>inherits</b> from the Enemy class, and we can then define our variables there instead. However, there's still another issue.

<b>Writing specific code in non-specific class</b><br><br>
Did you notice that the code in the Attack-function specifically mentions "goblin"? This is an example of using specific code in non-specific classes. Say we have an Animal-class, and we'd be looking to define a bunch of different animals that inherit from this class. If we then have a function in the Animal-class called Bark, that would mean every class that inherits from Animals would be able to bark, which is great for dogs, but not so great for elephants.<br>
The point I'm trying to make is that you want to define the <b>overarching</b> variables and functions in the base classes, and then add <b>specific</b> variables and functions in their children.<br><br>
Using these principles, we would then have code that looks like this:

public class Enemy<br><br>
{<br>
public string enemyName; <br>
public int level =;<br><br>
 
 &nbsp;&nbsp;<i> public void Attack()<br>
 {<br>
  Debug.Log(enemyName + " attacks!") <br>
 }<br><br>
}<br><br>

and<br><br>
<i>
public class Goblin : Enemy<br><br>
{<br>
 
 &nbsp;&nbsp;<i> public void GoblinChop()<br>
 {<br>
  insert code here <br>
 }<br><br>
}<br><br>

Using these principles, we have now designed a very simple system that can accomodate several different kinds of enemies. So let's quickly go over some other principles that are good to follow:<br><br>

<b>Keep the code clean and commented</b><br><br>
I cannot stress the importance of clean, commented code, especially if others have to read it. This can save <b>hours</b> of work. Strive to stick to naming conventions, use sensible variable- and function names, and make sure to comment <b>why</b> the code does what it does.<br><br>
<b>Reuse code wherever possible</b><br><br>
Having to learn new functions takes time, so why not reuse the ones you already know? This is where <b>generic programming</b> and <b>templating</b> comes in handy, as we can define template functions which we can then define when we need to!<br><br>
<b>Strive for simplicity</b><br><br>
Whenever you write new code, you should ask yourself the following question: "Is this too complex? Could this be done in a simpler way?" The answer is usually yes. While complex code is great to show off to others, simple code is easy to ready and, in many cases, will be easier to maintain. Therefore, stick to simplicity.<br><br>

That concludes my blog post on scalability.