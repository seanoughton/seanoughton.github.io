---
layout: post
title:      "Fail Fast : in Coding and in Life."
date:       2018-02-14 00:37:13 +0000
permalink:  fail_fast_in_coding_and_in_life
---


## What it means
It’s human nature to not want to fail.  However, this can lead to throwing good money after bad, and continuing down a road that you know is wrong, just because you don’t want to give up. I know that this has been an issue of mine.  However, I am learning to fail, and to fail fast. And I am beginning to like it and understand it’s value.

Failing fast isn’t about the larger issues in your life or in programming, rather it is about the little problems.  Failing on the smaller things, learning from it and incrementally progressing allows you to succeed on the larger issues.  This is true for coding and for life.  Instead of trying to do an exhaustive information search and trying to create the perfect plan, you put together a simple plan and put it into action and see what works. If your plan doesn’t work, then you try something else.  

## Failing Fast in Coding: Why?
Failing fast encourages simple code designs that work.  It assists with debugging your code, because as soon as your program hits a problem, it stops and provides you with an error message that will help to diagnose the problem. 

Fixing a bug during development, is exponentially easier and cheaper than trying to fix it when the code is in the production phase.  In the production phase, one bug could build on another, and you may create a problem when trying to fix the first one, especially if you don’t know what is causing the problem.  This could be particularly troublesome if your program is saving data to a database, and the bug is causing the data to be corrupted. The final result, is that it leads to more reliable software, reduces development time and costs.

## Test Driven Development (TDD)
Failing fast is part of a programming approach called Test Driven Development.  With TDD, you don’t start out by trying to write code that will solve your problem. Rather, you first state the expectations that you want your code to meet.  The expectations you write describe what the code will do when it is working, and it tests for a specific function of your code.

After you write the expectations, then you write the code that meets those expectations.  When you write the test, it’s like a story outline and your objects are the characters.  In the outline you write out what you want your characters(your objects) to accomplish and then you write the story that makes your characters do that.  In your code, you write the code that expresses that narrative.

This type of software development allows you to focus on the goals of your code fully, without having to think about how you are going to implement those goals. Instead of trying to state the problem and the solution at the same time, you can just focus on the problem. This forces you to think about what you want your program to do and how you want it to behave, before you start coding.

TDD leads to code that is flexible, with the ability to incorporate future changes.  It also makes it easier for other developers to understand your code.

## Ruby and RSpec
Ruby has a testing framework called RSpec which is a Ruby Library providing the functionality necessary to write tests.  RSpec has a set of methods designed for testing your code.

One of those methods is called **#describe**, which has an argument that describes what you are testing.

Inside the block for the #describe method is the **#it** method, whose purpose is to state the expectation of what you are testing.  The block for the** #it** method contains three other methods **#expect, #to** and **#eq.**

The **#expect** method has an argument that is the thing you are testing or comparing.

The #**to** and **#eq** methods are chained to the **#expect** method.  They complete the comparison, by testing what we expect the variable to be equal to.  The **#eq** method is a matcher, that specifies the expectation.

The test compares the result of running the code with a known outcome.  If the code passes the test, then we know that the code is behaving as expected. 


## Failing Fast: Life Lessons
Failing fast is not just a programming technique/approach, it can be seen as a life philosophy.  Failing fast and often, takes the stigma out of failure, rather showing that the knowledge gained from a failed attempt increases the probability of future success. Being able to try out new ideas fast and pivot to something else when that idea isn’t working increases your probability of success.

I read that failing fast is based on a Japanese Manufacturing model called Kaizen.   Kaizen comes from two japanese words: Kai (improvement) and Zen(good). Overtime Kaizen came to be known as “continuous improvement”, meaning the application of small, daily changes that result in major improvements over time. I like this idea of small changes, tested daily, failing or passing, and learning from those experiences in the larger goal of being a better developer.  It makes me a more confident learner.




