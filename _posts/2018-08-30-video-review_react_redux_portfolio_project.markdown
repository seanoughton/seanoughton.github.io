---
layout: post
title:      "Video-Review: React Redux Portfolio Project"
date:       2018-08-30 16:35:44 +0000
permalink:  video-review_react_redux_portfolio_project
---


For my React Redux Portfolio Project I made an app for Agencies, Post Houses, Video Production Companies and Video Editors/Motion Graphic Artists.  This app allows the user to upload a video and have other people comment on the video and approve or not approve the video.  

The reason that I created this app was that when I was working as a Video Editor, it was really difficult to get consolidated feedback from clients and people on my Team.  I would get an email from the Producer, a text from the Account Manager and a Slack Message from the owner of the company.  None of these people knew what the other person was communicating and often times their feedback would be contradictory.  There was also no official approval process for the video to move forward to the next stage.  This app alleviates some of those headaches by providing one central place for people to view and comment on the video and to see what other people are saying about the video. The feedback for a video is all in one place, so the people working on the video, the editors, motion graphics artists, etc. all know where to look to find out what needs to be done next for the video.  The app also forces the users to enter in the timecode that their comment is referring to.  As a video editor, I spent countless hours trying to figure out where in the video the feedback was referring to, because the timecode for that feedback was not communated to me.

This app uses a Rails API backend that persists the data to the database.  The Rails part sets up the database and the API Routes, serializing the data to be sent back for every API call.  


The front end part of the app is a combination of React and Redux.  React is used to render all of the html on the page,  including interactions and CSS.  React Router is used to create the RESTful routes so that the user is sent to the appropriate URL.  

Redux is used to create a local store that holds all of the state needed for the application to run.  Async javascript is used to fetch the data from the API and then store that data in the Redux store as state.  There is an initial call to the database when the app fires, which gets all of the users, projects, videos and comments.  Then as elements are added, the app sends GET/POST/PATCH/ or DELETE requests to the API routes to Read, Create, Update or Delete data from the database.  At the same time, the data is updated in the Redux store.

The process of hitting the api and storing things in the Redux store involves using Actions and Reducers.  The Actions send the fetch requests to the API, either sending data to the database to be stored or getting data from the database to be returned as json objects.  Once the async javascript request is completed, the action calls the dispatch function, passing in a "type" and the return json data from the fetch request.  This dispatch action gets sent to the Reducer, which has a Switch statement.  If one of the Cases in the Switch statement matches the "type" then the code inside that Case is run.  The code inside the Case statement adds the data returned from the fetch request to the Redux store as state. So for instance, when a user is created, the flow is that a fetch request of Post is sent to the "/users" API url.  Once the user has been created and added to the database, the fetch request returns the json from the API, which in this case is a user object in json format.  That json is sent as an argument in the dispatch function to the User's reducer with a type of 'ADD_USER' .  In the User's Reducer, the 'ADD_USER'  Case statement is triggered, which takes the user object in json format and adds it to the Redux store.  Now the user has been created in the database and is also in the Redux store, and that user information can be accessed in the app by accessing the Redux store.

For Sign Up I used bcrypt in Rails to encrypt and salt the password and store the users in the database.  For login and to make sure that the appropriate user is logged in and accessing the correct data, I created a Current User element in the Redux store.  When a user logs in, a fetch request is sent to the users controller with the username and password.  The Rails Route uses authenticate from bcrypt to authenticate the user. If the user is authenticated the API call returns the user as a json object and that user is stored in the state as current_user. If the user is not authenticated in the Rails route, then the json that is returned is simply "false".  If false is returned, that is stored inside of current_user in Redux.  I set up some logic in App.js that determines which routes will be available.  If current_user is "false", then the only route that is available to render is the login/signup page. If the current_user is something other than false, then the user is logged in and has access to all of the routes for the app.  Logging out simply sets current_user to "false" in the store and then the app only renders the login/signup route.

Moving forward, I would like to have this app incorporate a search through video stock sites like Adobe Stock and link to the Vimeo API so that users can search for videos there.  I would also like to add the ability for a user to upload a video through the app rather than just add a video url.  

I learned a lot in this project, specifically how to make RESTful routes and set up the Rails API as a way to store and send data.  I plan an expanding on the app and adding more features in the future.




