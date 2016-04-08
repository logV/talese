Talese
======

An exploration into client side engagement instrumentation split into actions,
pathing and time spent datasets. 

User Actions
============

UserActions tries to instruments all clicks on the page. Whenever an HTML node
is clicked, a new sample is generated with information gleaned from the DOM
about that node and emitted. 

If jQuery is being used, UserActions is able to use the "delegate" feature to
capture all clicks, regardless of whether their propagation has been prevented.
Otherwise, if the click event propagation is stopped, there is a chance that
the click will be missed.


Schema
------

  * action (click, swipe, etc)
  * clicked node class+id
  * full path (class+id) to document body
  * closest parent ID
  * closest href
  * current page URL
  * width/height of the page
  * clientX/clientY and pageX/pageY of click

Pathing
=======

The page load tracker records when the URL in the address bar changes and updates
the current page context to reflect the change. This is basically a 'page load'
dataset that gives the frequency of different page loads as seen by the client.

Schema
------

  * page
  * prev page (for tracking URL changes made using HTML5 pushState)

Time Spent
==========

The TimeSpent tracker follows whether the browser is "active" or "idle". To
quantify this data, there are several possible states the browser can be in:
active, idle, unfocused, hidden and unknown. __active__ state is when there is
user input going on or during the first part of a page load. __idle__ state is
when the page is visible but hasn't been interacted with for a certain amount
of time. the __unfocused__ and __hidden__ state reflect whether the browser is
focused and whether the tab is visible. The __unknown__ state keeps track of
the rest of the time.

Packets are sent that account for 60 seconds of page time, with the time
divided up between the 5 categories. An avg of 60 for active would mean that
everyone using the site is active. An avg of 60 for idle would mean that
everyone using the site is idle.

TODO: figure out a better metric to express 'activity saturation'

Schema
------


* unfocused
* hidden
* active
* idle
* unknown time (when resuming from sleep or other unexpected clock changes)



Potential queries using these datasets
======================================

* What are the most popular pages and how much active user engagement they have
* How often different actions are taken by individuals and what order they are taken in
* How much click activity occurs on a given pages and where do clicks happen
* How many unique individuals are using a site (by IP or by session ID)
* What are the common dimensions of individuals browsers
* Compare activity and engagement by mobile vs. desktop

