---
layout: post
title:      "LEARNING SQL & ORM"
date:       2018-03-16 23:20:07 +0000
permalink:  learning_sql_and_orm
---


I found that the SQL and ORM sections really started to pull things together for me.  Knowing how our programs are going to interact with a database and seeing how the creation, saving and reification of instances happens was really satisfying.  

## SQL
It took me a little while to get the hang of SQL queries, but I found that using DB Browser for SQlite and playing around with database really helped.  Being able to see in real time what is happening and at the same time the database schema and data, was really helpful.  It was especially helpful with the aggregate functions.

## ORM
The logic behind the database storage and how it is mapped to the way that we have been building our classes and instances is really cool.  It also just makes a lot of sense.  Not storing all of the object instances in memory, and only reifying them when needed makes sense in terms of memory and program speed.

Abstracting the functions of ORM so that all classes can inherit from that also makes perfect sense as a concept.  The metaprogramming required to do this is really intricate and exquisite.  Building upon the metaprogramming knowledge that was taught up to this point, and extending it to the database mapping was a challenging concept, but really makes sense to me now.

## LOOKING FORWARD
What was even better was finding out that ActiveRecord could abstract all of the this functionality even further.   I can’t wait to see how this plays into the upcoming sections of Rack, Sinatra and Rails.

