---
layout: post
title:      "Tapping Ruby Objects"
date:       2018-10-09 21:54:19 +0000
permalink:  tapping_ruby_objects
---


Lately I have been spending a great deal of time with Ruby and I am really enjoying working with this pure OO language and its elegant support for blocks.  I was first exposed to blocks and iterators nearly twenty years ago when I started working with Smalltalk.  Comming from more procedural languages, I was blown away by this new paradigm and went absolutely crazy for blocks and iterators.  Since that time, when I thought of OO and code blocks I also, of course, thought of iterators.  I probably overdid it.


Recently I have come accross the Ruby #tap method.  The first few times I saw it in use I just glossed over it without much thought.  It was not conforming to my mental model of block usage and seemed very odd and perhaps even pretentious. Then I came accross it several more times and saw it employed by very respected developers; this got my attention.  Eventually I was won over and now find myself looking for opportunities to employ it ... I am probably overdoing it again!

Here's the use-case that sold me on #tap:  ... suppose you need to:

* create a class  instance
* modify that instance
* return that instance

Here's how I would typically code such use case in the "new_from_array" class method:

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

I have programmed this same pattern probably thousands of times and it always felt reasonable but also a bit troubling.  I employ a method-scoped variable to hold onto the instance while I modify its state but I really like to minimize method variables.  Most irksome is the last line where I have to force return of the new instance by dangling this solitary reference to 'aParrot' at the end of the method.

Utilizing #tap makes this method much better, from my point of view, in both respects.   Here the equivalent method:

```
  def self.new_from_array_tap(array)
    self.new.tap do |i|
      i.name = array[0]
      i.age = array[1]
    end
  end
```

First, although I still employ a variable, now its scoped to the block rather than to the method.  More narrow scope is always better. Secondly I no longer need the dangling reference to ensure return of the instance.

Here's the contract from the #tap methods perspective:  
> Call me on on any instance(i) and pass me a block.  I'll run that block and pass in the instance as a block variable.  Once the block completes I'll return i.
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

Its so simple and so elegant and so obvious!  I doubt I could ever I have invented it. 





