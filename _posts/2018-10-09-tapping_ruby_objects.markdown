---
layout: post
title:      "Tapping Ruby Objects"
date:       2018-10-09 17:54:20 -0400
permalink:  tapping_ruby_objects
---


Lately I have been spending quite a bit of time with Ruby and I am seriously enjoying working with this pure OO language and its elegant support for blocks.  I was first exposed to blocks and iterators over twenty years ago when I started working with Smalltalk.  Coming from more procedural languages, I was blown away by this new paradigm and went absolutely crazy for blocks and iterators.  Since that time, when I thought of OO and code blocks I also, of course, thought of iterators.  I probably overdid it.


Recently I have come across the Ruby #tap method and a completely different use for code blocks.  The first few times I saw this method in use I just glossed over it without giving it much thought.  It was not conforming to my mental model of block usage and seemed odd and maybe a bit pretentious. Then I ran into it several more times and saw it employed and by developers I admired and this got my attention.  After a little exploration I was completely won over and now I find myself looking for opportunities to employ #tap ... I am probably overdoing it again!

Here's the use-case that sold me:  ... suppose you need to:

* create a class  instance
* modify that instance
* return that instance

Here's how I would typically code such a use case in the "new_from_array" class method:

```
class Parrot

  attr_accessor :name, :age

  def self.new_from_array(array)
    aParrot = self.new
    aParrot.name = array[0]
    aParrot.age = array[1]
    aParrot
  end

end

array = ["Sam", 38]

sam = Parrot.new_from_array(array)
puts "#{sam.name} , #{sam.age}"  #=> Sam , 38

```

I have programmed this same pattern probably thousands of times and it has always felt reasonable but also a bit troubling.  In this old implementation I would employ a method-scoped variable to hold onto the instance while I modify its state ... but I really like to minimize method variables. Also, and even more irksome is that I need to add a "dangling" reference to the new instance at the end of the method to force return of the instance.

Utilizing #tap makes this method much cleaner and better overall, from my point of view, in both respects.   Here's the equivalent method with tap:

```
  def self.new_from_array(array)
    self.new.tap do |i|
      i.name = array[0]
      i.age = array[1]
    end
  end
```

Although I still employ a variable, now its scoped to the block rather than to the method and more narrow scoping is always better.  Also, I no longer need the pesky dangling reference at the end of the method since #tap returns the instance for me!

Here's the contract from the tap method's perspective:  
> Call me on on any instance and pass me a block.  I'll run that block and pass it the instance as a block variable.  Once the block completes I'll return the instance.
> 

Here's the Ruby implementation of the tap method:

```
class Object
  def tap
    yield self
    self
  end
end

```

This amazes me!  The tap method is four lines long.  It contains only six words!  It's so simple and so elegant and so obvious (in hindsight).  I doubt I ever could have invented it. 





