animatedtimers
==============

Animated timers for Mudlet, using the geyser framework.

CHANGELOG
2.0 - added :stop(name) function. Also, when a timer expires or is stopped it will stop the stop watch. Added argument for whether to display the time on the timer or not.
2.1 - Added option to provide a caption for the timer, such that the text appears after the time (if showTime is true) or just as the text on the gauge (if showTime is false)
2.2 - Added :pause(name), :start(name) functions to allow pausing and restarting of timers. The difference between pause and stop is that pause will leave the timer visible on the screen, and stop will hide it.
3.0 - Added :pauseAll(), :stopAll(), :destroy(name), and :destroyAll() functions
      Constructor has changed as well, in order to make facilitating future options easier

###demonnic.anitimer:new(name, constructor, time, tableOfOptions)
This will create a new animated timer, named name. constructor should be a standard constructor for a Geyser.Gauge. time is the amount of time in seconds for the timer to run for. tableOfOptions has the following available options right now
- showTime: true or false boolean value. Defaults to true. This determines whether the amount of time left in the timer is shown on the timer or not
- timerCaption: string value. If you want some other text to show up on the timer, this is where you set it
- cssFront: string value. This should be a qt stylesheet, as you might normally pass to a Mudlet Label
- cssBack: string value. This should be a qt stylesheet, as you might normally pass to a Mudlet Label

it should be noted that if you specify cssFront, then cssBack will be the same as cssFront, but it will have a "background-color: black;" constraint added to the stylesheet in order to try and ensure some contrast between the two. One example would be:
```
local myCss1 = [[
border-width: 4px;
border-radius: 7;
border-color: red;
background-color: green;
]]
local myCss2 = [[
border-width: 4px;
border-radius: 7;
border-color: green;
background-color: red;
]]
demonnic.anitimer:new("Test2", {x = 0, y="50%", height = 20, width = "100%"}, 10, {container = demonnic.newContainer, showTime = true, timerCaption = "Test2", cssFront = myCss1, cssBack = myCss2})
```

This is one of the timers in the included "anitimer demo" alias. I set 4 timers up in this alias, it should provide you with some insight into how it looks.


###demonnic.anitimer:stop("myTimer") 
stops "myTimer" and removes it from the screen

###demonnic.anitimer:start("myTimer") 
restarts "myTimer" if there is any time left on it, and if so shows it on the screen

###demonnic.anitimer:pause("myTimer") 
stops "myTimer" but leaves it visible on the screen

###demonnic.anitimer:destory("myTimer")
stops "myTimer", removes it from the screen, and then nils out the timer, removing it from tracking. Use this is you want a timer to really go away and not be brought back by startAll()

###demonnic.anitimer:startAll()
will start every timer which is being tracked which is also not active (active timers are already started, after all)

###demonnic.anitimer:pauseAll() 
stops all timers, but leaves any timers which were visible on the screen

###demonnic.anitimer:stopAll()
stops all timers and removes them from the screen

###demonnic.anitimer:destroyAll()
destroys all animated timers

