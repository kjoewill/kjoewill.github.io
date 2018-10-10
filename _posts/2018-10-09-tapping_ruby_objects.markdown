---
layout: post
title:      "Tapping Ruby Objects"
date:       2018-10-09 17:54:20 -0400
permalink:  tapping_ruby_objects
---


Lately I have been spending quite a bit of time with Ruby and I am seriously enjoying working with this pure OO language and its elegant support for blocks.  I was first exposed to blocks and iterators nearly twenty years ago when I started working with Smalltalk.  Coming from more procedural languages, I was blown away by this new paradigm and went absolutely crazy for blocks and iterators.  Since that time, when I thought of OO and code blocks I also, of course, thought of iterators.  I probably overdid it.


Recently I have come across the Ruby #tap method and a completely different use for code blocks.  The first few times I saw it in use I just glossed over it without much thought.  It was not conforming to my mental model of block usage and seemed very odd and perhaps even pretentious. Then I ran into it several more times and saw it employed and by developers I admired; this got my attention.  Eventually I was completely won over and now I find myself looking for opportunities to employ #tap ... I am probably overdoing it again!

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

I have programmed this same pattern probably thousands of times and it has always felt reasonable but also a bit troubling.  In this implementation I employ a method-scoped variable to hold onto the instance while I modify its state ... but I really like to minimize method variables. Also, and most irksome, is the last line where I force return of the instance by dangling a reference to it, 'aParrot', at the end of the method.

Utilizing #tap makes this method much cleaner and better overall, from my point of view, in both respects.   Here's the equivalent method with tap:

```
  def self.new_from_array_tap(array)
    self.new.tap do |i|
      i.name = array[0]
      i.age = array[1]
    end
  end
```

First, although I still employ a variable, now its scoped to the block rather than to the method.  More narrow scoping is always better.  Secondly, I no longer need the pesky dangling reference to ensure return of the instance.

Here's the contract from the #tap methods perspective:  
> Call me on on any instance and pass me a block.  I'll run that block and pass it the instance as a block variable.  Once the block completes I'll return the instance.
> 

Here's the Ruby implemtation of the tap method:

```
class Object
  def tap
    yield self
    self
  end
end

```

Its so simple and so elegant and so obvious!  I doubt I ever could have invented it. 





