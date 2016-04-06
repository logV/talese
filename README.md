Talese
======

An exploration into client side engagement instrumentation split into actions,
pathing and time spent datasets. 

User Actions
------------

UserActions tries to instruments all clicks on the page. Whenever an HTML node
is clicked, a new sample is generated with information gleaned from the DOM
about that node and emitted. 

If jQuery is being used, UserActions is able to use the "delegate" feature to
capture all clicks, regardless of whether their propagation has been prevented.
Otherwise, if the click event propagation is stopped, there is a chance that
the click will be missed.

Pathing
-------

The pathing tracker records when the URL in the address bar changes and updates
the current page context to reflect the change. This is basically a 'page load'
dataset that gives the frequency of different page loads as seen by the client.

Time Spent
----------

The TimeSpent tracker follows whether the browser is "active" or "idle". To quantify this data, there are several possible states the browser can be in: active, idle, unfocused, hidden and unknown. __active__ state is when there is user input going on or during the first part of a page load. __idle__ state is when the page is visible but hasn't been interacted with for a certain amount of time. the __unfocused__ and __hidden__ state reflect whether the browser is focused and whether the tab is visible. The __unknown__ state keeps track of the rest of the time.

The data is quantified in 60 second chunks and can be seen as a measure of 'saturation' of each of the above states. 
