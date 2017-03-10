---
layout: post
title:  "Conquering the Blank Slate: My First Gem"
date:   2017-03-10 19:07:05 +0000
---


The first time you ride a bike, you use training wheels. The first time you go bowling, you use bumpers. The first time you code a method or class, you start with an environment and project structure already set. But what about when it’s not the first time? It’s approximately the 120th time you’re engaging with code – that is if we’re counting Learn-co labs ;). It’s time to shed the training wheels and create your first gem.

**The Process**

My parents served as my inspiration for the topic of my first gem. Each night, they look up which TV shows are airing new episodes and religiously watch their favorites. They’re always asking for recommendations from friends on new, popular shows. In my millennial brain, I think - just Google it! And so I did. I found a list of the top trending shows with new episodes airing that night at [TV Guide](http://www.tvguide.com/trending-tonight/). Great! I had the data for my gem.

For the CLI Data Gem Project, I started with a blank slate. I knew there was something about a Gemfile, spec, bin, and lib, so I started creating files. But wait, there had to be a better way to do this. I remembered a favorite quote from Larry Wall: “the three chief virtues of a programmer are: laziness, impatience, and hubris.” It was time to tap into my inner programmer and find the simplest way to do this. Queue Avi’s [CLI Data Gem Walkthrough](https://www.youtube.com/watch?v=_lDExWIhYKI).

The solution to my environment confusion: Bundle. Kudos to the creators for saving us all from file-creating madness. With the help of a few tips from Avi, I was set up and ready to get down to building my classes. 

I wanted the interface to be simple. Call the gem and receive a numbered list of top trending TV shows airing tonight with their times and networks. Type in the number of the show you’d like to learn more about and receive details on the specific episode. After a few days of work, I had my `tv_tonight` gem completed.

**The Gem**

The Episode class is responsible for scraping the TV Guide trending shows page and collecting instances of Episodes. When scraped, each instance is created with attributes for the series, airing time, airing network, episode description and a url for more information. The all method of the Episode class returns all instances collected.

The CLI class is responsible for interacting with the user and calling on instances of Episodes. When starting the tv_tonight gem, the `TvTonight::CLI `call method is used, calling `TvTonight::Episodes.scrape_episodes` to create the current array of trending shows. The CLI then lists each of these shows, in order of highest trending, and asks the user which one they would like to know more about. It then collects the user input and returns greater detail about the specific show and episode that will be airing that night. From here, the CLI loops asking for input and allowing the user to exit. Upon receiving the input `“exit”`, the CLI provides an outgoing `“Happy Watching!”` message and closes. 

**Possible Additions**

When creating the gem, I considered a separate Series class where each Episode belonged to a Series. The Series would have attributes for start date, number of seasons, its collection of Episodes, and a separate description about the overall series. 

The interface could be extended further to include attributes such as a list of cast members, the Episode’s cast would always be included in the Series cast, but not all members of the Series’ cast would be in each Episode. An even greater extension would be to create instances of Actors with names, birthdays, and the Series/Episodes on which they appear. 

For the sake of this project, it did not seem necessary to extend such capabilities. My goal was to find out what is new and popular on tv tonight, not recreate IMDb. 

**Final Thoughts**

Overall, I’m satisfied with the functionality and output of my gem. The most intimidating part of the project was setting up the environment and sorting out where to require various gems. Once things were set, it was comfortable getting back into the flow of creating object classes and their methods. I intend to publish my gem after my assessment and any additions or refactoring. 

First blank slate project – Conquered!

