---
layout: post
title:      "CLI Data Gem Project - SF Bay Area Concerts"
date:       2018-03-02 01:32:26 +0000
permalink:  cli_data_gem_project_-_sf_bay_area_concerts
---


The CLI Data Gem project was definitely the hardest project I’ve done so far for Flatiron.  Mainly because it involves bringing together so many things: Procedural Ruby, Object Oriented Ruby, Scraping, Regex and wiring everything together inside a Gem file structure.  

## About My Gem
My Gem allows the user to see the upcoming concerts for the San Francisco Bay Area.  It scrapes the website for Another Planet Entertainment (http://apeconcerts.com/).  

The app shows all of the upcoming concerts with the artist, the venue, the date of the show and if tickets are available.

It then allows the user to choose one of the concerts to see more information.  Depending on the information available, the user can see the ticket price, the artist’s personal website, where to buy the artists music, where to watch the artists music videos, as well as all of the artist’s social links.

## The Basic Structure
**I created three Classes:**
1. Scraper class for scraping any website data
1. Concert class for creating concert instances and creating a list of all concerts
1. CLI class for providing user interaction and displaying information to the user

** Each concert instance has the following attributes: **
* a concert url
* The artist’s name
* The location of the venue
* The date and showtime of the concert
* The availability of the concert, whether it is sold out or not
* The price the tickets start at for the concert.
* A Bio of the artist, if the user chooses to read it
* A link to the website of the artist
* A link to where to buy/download the artist’s music
* A link to where to watch the artist’s music videos
* Links to all of the artist’s social media: facebook, twitter, instagram


## The Flow of the App 
1. The app greets the user and then shows them a list of the upcoming concerts. 
1. Then the app asks the user to pick a concert to find out more information about it.
1. The app displays the specific information about that concert.
1.  The app then asks the user if they want to read the bio of the artist.  The reason that this functionality is separated, is that some of the bio’s are really long, and the user may not want to read all of that information.
1. The app then asks the user if they want to see the list of concerts again.
1.  If they say yes, it shows them the concert list, if not, it thanks them and says goodbye, exiting the program.




## Struggles
One of my bigger struggles was just understanding how the Gem itself worked. I was unclear of how the files related to each other and were wired together.  I did some research and watched other videos to help fill the gaps in my knowledge.  Scraping of the pages was also difficult, especially getting specific children of parent objects.  I also had to write code for situations where the artist did not have some of the attributes, like an instagram link for instance.

## Final Thoughts
I learned a lot during the course of this project.  Not only about Object Oriented Ruby and Gems, but also about problem solving.  One of my biggest takeaways was that sometimes you just have to take a step back and make sure that you understand something before you move forward with the actual coding.


Link to github: https://github.com/seanoughton/sf_bay_area_concerts_cli_app

