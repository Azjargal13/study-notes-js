# Javascript question #3

resources used:

**Q: Explain event delegation?**

# Event delegation

# What is event?

Events are actions or occurrences which system responds. For example, user clicks a btn, then it shows the info etc.

System produces a signal when an event occurs, provides mechanism by some action can be taken automatically. 

Each event has an event handler (listener), that will run when the event fires.

Note: Web events are not part of the core JavaScript language — they are defined as part of the APIs built into the browser.

### Event objects

Automatically passed to event handlers to provide extra features and information.

`e.target` useful when setting the same event handler on multiple events.

## Event bubbling and capture

Event bubbling and capture are two mechanisms that describe what happens when two handlers of the same event type are activated on one element. 