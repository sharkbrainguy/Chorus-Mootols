Chorus
======

The easiest way to start using `Chorus` is the function `Chorus.view`.

`Chorus.view` takes any number of `Timelines` or timeline shorthands and returns a `Chorus.View`.

A `Chorus.View` implements `toElement` so it can be grabbed, adopted, etc.

This example demonstrates alot of the shorthands for various types of `Timeline`.

    $('ChorusContainer').adopt(
        Chorus.view(
            "@sharkbrain", // Follow the twitter user sharkbrain
            "@sharkbrain/friends-i-dont-like", // follow the list  'friends-i-dont-like'
            "@+sharkbrain", // Follow the conversation with sharkbrain
            "#sharks", // Follow the hashtag sharks
            "FB:BarackObama", // Follow Barack Obama on Facebook
            "FF:paul", // Follow Paul on Friendfeed
            "BZ:anybody" // Is anyone on Buzz?
        ));

Basic Concepts
-------------

Chorus provides three base classes Status, Timeline, and View.

Statuses represent a single status message on a service.

Timelines publish Statuses.

Views subscribe to Timelines and display any Statuses that it receives as HTML. 

A Chorus module may provide subclasses of these base classes for use with a particular service.

Chorus.Twitter
-------------

Chorus.Twitter provides TwitterUserTimeline (a Timeline subclass) and Tweet (a subclass of Status).

The following creates a View and a Timeline, and the View subscribes to the Timeline.

Then the Element TwitterDisplay adopts the view.

    var view = new Chorus.View(); 
    var sharktwitter = new Chorus.TwitterUserTimeline("sharkbrain") // follows the user sharkbrain on twitter
    view.subscribe(sharkbrainTwitter); 
    
    $("TwitterDisplay").adopt(view);

this could also be initialized with the 'feeds' and 'container' options for the same effect:

    new Chorus.View({
        'feeds': new Chorus.TwitterUserTimeline("sharkbrain"),
        'container': "TwitterDisplay"
    });

The Chorus.Twitter module installs the shorthand "@username" for TwitterUserTimelines so the same thing could also be achieved with the shorthand.

    new Chorus.View({'feeds': "@sharkbrain", 'container': "TwitterDisplay"});

Chorus.Twitter also provides the following Timeline subclasses with the associated shorthands:

    TwitterListTimeline(username, listname, options) "@username/listname"
    TwitterAboutTimeline(username, options) "@+username"
    TwitterSearchTimeline(searchstring, options) this is the default if no other patterns match. 

TwitterAboutTimeline follows a user and all tweets addressed to that user.

