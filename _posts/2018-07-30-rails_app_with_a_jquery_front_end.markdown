---
layout: post
title:      "Rails App with a jQuery Front End"
date:       2018-07-30 16:00:16 +0000
permalink:  rails_app_with_a_jquery_front_end
---


This project was very challenging and it really shored up my knowledge of jQuery and AJAX.

What I found particularly challenging was the nature of the asynchronous response, and how and when to access that response.  Also the closures created by the AJAX get and post requests were challenging to get the hang of.

Despite those challenges, I found this project very exciting.  I really like the way that Javascript object model classes work and how similar they are to a ruby class.  Once I began to use them with the data returned from the AJAX requests, getting and using the data stored on each object instance was easy and very useful when it came to adding data to the page.

I did feel like Ruby and Rails were at odds with jQuery and AJAX, and that I needed to recreate some of the functionality and views that I had already created.  For instance, the erb file used to create a form, had to be recreated using javascript and Handlebars.  Also, the validations I had set up for creating a Comment, had to be recreated when using AJAX to make the request.

Not having to do a page refresh in order to get and create data is definitely an advantage, but I would have liked a tighter interaction between Rails and jQuery/AJAX.

I used Javascript Classes for the creation of Javascript model objects for Users, Pairings,Comments,Wines, and Cookies.  This was very useful for taking the data returned from the AJAX requests and turning it into objects that I could access elsewhere in the code.  It made it much easier to add data to the page and to work with associated data, for instance the has_many/belongs_to relationships.  Within the Comments Class, I created a prototype method that provides the functionality to format a Users name for the user that created the comment.

I used jQuery and AJAX to render index lists to the User's show page without a page refresh. A user can now click a button to see all of the pairings, comments, cookies and wines associated with a user without leaving the page. In order to make this faster and limit the amount of database calls, the application automatically loads the Users pairings, comments, cookies and wines into memory when the user show page loads.   This way when the user clicks on the button to show an index resource, the data has already been loaded.

I created previous and next buttons that use jQuery to get a show route for a pairing without having to a page refresh.  When clicking on these buttons, jQuery is used to clear out the old pairing data and an AJAX call is made to get the new pairing data.  When that data is received, it is loaded to the page with jQuery.

On the pairings show page, there is a button for adding a comment. When that button is clicked it adds a form to the page with jQuery.  When the form is filled out and submitted, the action is hijacked and AJAX is used to create the new comment in the database and add the new comment to the page.

On the pairings show page I added a button to show all of the comments belonging to that pairing.  When the button is clicked, an AJAX call is made getting all of the comments associated with that pairing.  When the data is received, jQuery is used to add that data onto the page.


Overall, I think that this project really increased my understanding of how Javascript and jQuery work.  I also gained a greater ability to use AJAX for getting and retrieving data.  
