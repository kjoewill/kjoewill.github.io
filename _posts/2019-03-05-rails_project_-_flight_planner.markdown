---
layout: post
title:      "Rails Project - Flight Planner"
date:       2019-03-05 14:14:23 -0500
permalink:  rails_project_-_flight_planner
---


I took the opportunity to cement some fundamental Rails skills and also to stretch a bit by leveraging the Google Static Maps interface.  As if these two activities were not enough fun for one project, I was also able to revisit spherical trigonometry in order to calculate distances between two points on the globe.

In a nutshell, the application allows a private pilot to plan between two selected airports in a selected aircraft.  When a new flight plan is created the google maps API is leveraged to provide a view of the most direct path between the two airports.  Here's an example:

![]https://drive.google.com/uc?id=14vtPJuEGXCtcNoNo2Sdd_RuKiML4pRPV)

After providing two distinct points on the planet in terms of a atitude/long pairs, Google Maps does all the heavy lifting with regard to providing the image, the two marked points and the shortest path between the point.  The path appears curved on a flat map because its representing a direct line as if it was drawn on a globe.

I did not find an easy way to extract the distance of the path from Google Maps so the application calculates this value using a slick set of equations called the [Haversine Formula](https://rosettacode.org/wiki/Haversine_formula).  The calculated distance is used to calculate expected flight times and also provide a log of total distance flown over all flights.

Besides basic flight planning, a registered user can also use the application to report issues with a flown aircraft such as underinflated tires or malfunctioning avionics

Here a UML diagram of the application:

![](http://drive.google.com/open?id=14vjnm1tg2B6U6ONM-z5KslqsDeFiys2j)

And here's the [GitHub repo](https://github.com/kjoewill/flight-planner) if you'd like to look at the source.



