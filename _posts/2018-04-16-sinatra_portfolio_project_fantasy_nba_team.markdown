---
layout: post
title:      "Sinatra Portfolio Project: Fantasy NBA Team"
date:       2018-04-16 23:14:09 +0000
permalink:  sinatra_portfolio_project_fantasy_nba_team
---


Building my Sinatra Portfolio Project has been really rewarding.  It involved connecting most of the technologies we have learned so far, from understanding Database’s and Ruby, to HTML and CSS.  

After deciding on creating a Fantasy Basketball App, the first thing I did was write out an outline of how I wanted the app to work.  This gave me the opportunity to step back and see how I would structure the app. Through this higher level look at the app, I was able to decide what my models were going to be, and the basic structure of my routes.  I found that writing this out in advance and then drawing a diagram of how my models would interact made coding much easier, because I could refer back to this outline if I ever started to get confused about how the app was supposed to work.  I knew that this original outline was not written in stone, but it provided a great base to work from.

### Setting up the Gems
The first thing I did, after writing the outline, was to set up my Gem file with all of the code libraries I would need for the project.  In addition to Sinatra and Active Record, I used bcrypt for password encryption, Shotgun for spinning up the web app, sqlite3 for the database, tux for testing out my models and the database, rack-flash3 for alert messages, and a gem called ‘valid_email2’, to test for valid email addresses. Then I made sure that my environment file was requiring all of the appropriate files and gems and also establishing the connection with my database.

Next, I made sure that my file structure was correct and that I had a config.ru file that not only linked linked to the environment file, but also called and ran the controllers I would need to run my application. I also used  Rack::MethodOverride, so that I could use patch and delete requests in my routes.  This  interprets any requests with name="_method" by translating the request to whatever is set by the value attribute.  So a post request gets translated to a patch request or a delete request when we use this code in a form:  **input type="hidden" name="_method" value="patch"** .

### The Actual Coding

I started the actual coding by creating my models.  In my case, I had **users, teams and players**.  For this app, I wanted users to be able to log in, create teams, and see other user’s teams, but not be able to edit or delete other user’s teams.  So my models are structured like this:

* **a user has many teams.**
* **a user has many players through teams**
* **a team belongs to a user**
* **a team has many players**
* **a player belongs to a team**



### The Database and Migrations

After creating my models, I created the migrations for my database.  Since I had a clear idea of how my models related to each other, this was relatively simple.  I initially created a seed file, with a few players in it to play around with. However, I eventually found a csv file of a bunch of NBA players, and I knew that I would eventually use that to seed the database.  In order to do that, I created a Rake task called **seed_db**, that reads the csv file, iterating through each row, and creates a player for each row and then saves that player to the database.



### Routes
Once I had the database set up and seeded, I moved into creating the basic structure of my routes.  I created a main application controller that the other controllers would inherit from.   The I created route files for the user, the team and the player.  

#### User Routes

First I created the signup and login GET routes, and the basic structure for the HTML for corresponding erb files with the forms that the user would need to fill out.  Then I created the corresponding POST routes testing to make sure the user was filling out all of the necessary form fields.  Once the verification tests passed, the user is then created and saved to the database.  The login routes work similarly, making sure that the user enters in the appropriate information in order to log in. 

I also create two helper methods, that all of the routes could access, ** logged_in?** and **current_user**.  

**logged_in?** is used by routes to make sure that a user is logged in.

**current_user**   returns whoever the current user is, so that information can be used to populate the html pages with user information.


#### Team Routes

The team routes were a little more complicated.
First I wanted the user to be greeted with a list of all of the teams after they log in.  So the **'teams/'** route does just that, it iterates through a list  of all of the teams and provides the user with that list in the teams.erb file.

The user is then presented with the option of creating a team.  This route takes the user to a form where the user must enter in a Team name, and choose at least one player for their team.  The list of players is created by iterating through all of the players in the database and displaying their names in check boxes for the user to select from. Once the user has named their team and selected players, the form get’s routed to the **teams/new** POST route, where the users’ input data is used to create the team.  The team is then saved to the database.

From here, the user is redirected to the list of all of the teams.  The user has the ability from this list to edit or delete their own teams.  If they choose to delete their team, they are asked again to make sure that they want to delete the team, and then the request is routed to the **DELETE team route**, where the team is removed from the database.  If the user chooses to edit their team, they are sent to an edit page, where they can choose to change the name of their team or add or remove players.  This form data is routed to the **PATCH route**, where the user’s team is updated with the new information.

I created some helper methods specifically for the team routes that make sure that if a player is added to a team, that player is removed from the pool of available players.  The main helper method here is called **available_players**, and returns a list of available players that is used to populate the Create Teams page.

#### Player routes

The player routes are little more simple.  Basically, a user can see the stats of an individual player, edit a player or create a player.  I did not want to make it possible for a user to delete a player.  These routes follow a similar pattern to creating a team.

### Styling and Testing
After creating this basic structure and testing it out to make sure that it worked, I moved into styling the app with Bootstrap.  I used the navbar functionality to make it easier for the user to get around the app.  I used the button and form styling and the basic container/row/column structure to make the app look more appealing and be easier to use. Most of this happened in the erb files.  I used a layout.erb file to load in the bootstrap css and javascript files. 

### Conclusion

Over all, I learned a lot during this project.  And I really feel like the curriculum is coming together for me.





