---
layout: post
title:      "Sinatra - Pulling it all together"
date:       2018-11-28 20:57:00 -0500
permalink:  sinatra_-_pulling_it_all_together
---


I’ve recently completed a Sinatra-based project which pulls together several technologies and techniques I’ve been studying.  Three primary technologies were employed:

* The Sinatra DSL
* Active Record to store data to an RDB
* REST conventions for routing

### Sinatra
Sinatra is a Rack-based Domain Specific Language(DSL)/Framework built to support development of web-applications written in Ruby.  Like Rails, Sinatra employs Ruby’s inherent support for meta-programming to provide the DSL it presents to the developer.  My understanding is that Sinatra is lighter-weight and, perhaps, more flexible than Rails which insists on several conventional structures like MVC.

### Active Record
Many developers do not know this but Active Record’s support for Object-Relational mapping, database migrations and validations can be used outside of Rails.  This was certainly news to me!

### REST
The REST conventions that we take for granted today originated from Roy Thomas Fielding’s PhD [dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm) in 2000.  Although much bigger than a set of routing conventions  - seriously, take a look at the dissertation - following these conventions leads to an understandable web app that promises to scale and remain maintainable.

### The App
The application I choose to implement with these tools and conventions is a fairly simple (but complete) online Flight Log that can be used by pilots to create and maintain a record of all their flying activity.  The app allows a new user to create an account with a password, log in to their own home page and then, create, read, update and delete flight logs.  The logs contains fields for date, origin airport, destination airport, number of landings, general remarks and duration of flight.  The user’s home page also provides some related statistics such as total number of flights, cumulative hours flown, etc.

It was great fun and enlightening to work with these technologies and see firsthand how quickly they allow creation of full featured web applications.  It seems that Sinatra has hit a perfect medium between being a bare bones framework and a near magical DSL such as Rails.  Now when I do use Rails I’ll have a much better understanding of what is going on under the covers.  If you’re interested you can check out the code on [GitHub](https://github.com/kjoewill/pilot-log).

