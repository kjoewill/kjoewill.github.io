---
layout: post
title:      "Scraping By"
date:       2018-09-21 16:42:42 -0400
permalink:  scraping_by
---


I completed a project recently where the main requirement was to scrape a public website and provide two levels of useful information to a user via a command line.  Also, I would need to program in Ruby and take an object oriented approach.  I started with these very high level requirements and then upped the ante a bit by choosing to use some pubic web service for the second level of information.

First, I conjured up and idea for an application that, while a bit contrived, would make some sense in the real world.  What I came up with was a tool that a private pilot might use to help plan a flight in poor weather.  The pilot user would ask (via the command line) for all the airports within one of the 50 United States that support poor weather operations; that is, airports that provide electronic navigation support via satellite, radio, etc.  The pilot could then review these available airports and ask for current weather information for any of them.  I was pretty quickly able to find a candidate website (Global Air)  for the high level airport capability info and a web service (AVWX) for current weather.

I initially took an outside in approach and began with a simple CLI (command line interface) in mind.  Then I created my domain model which consisted of just a handful of classes.  Not surprisingly the center of this model is the class Airport.  A small number of other classes act in supporting roles such as a Scraper and WeatherAPI classes.

![alt text]](https://github.com/kjoewill/ifr_airports/raw/master/images/model.jpg)

I “wired’ up the CLI with mocked instances of my Airport class and got the basic CLI commands working.  Once happy with that flow I turned to the Scraper and WeatherAPI classes and was excited to see this also come together quickly.  The heavy lifting was all done by the Nokogiri gem for scrapping Airport information and the built in Ruby Net::HTTP and JSON classes to interact with the web service.  Using these utilities and Ruby allowed me to produce the app with surprisingly few lines of code.  My Airport, Scrapper and WeatherAPI classes are each fewer than 40 lines!  Lots of functionality and few lines of code.  This is what makes programming a joy.

