# Javascript question #3

resources used:
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events
- https://davidwalsh.name/event-delegate
- https://stackoverflow.com/questions/7614317/what-is-the-difference-between-native-objects-and-host-objects
  

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

 but it causes the `<div>` to also be hidden at the same time. This is because the video is inside the `<div>` — it is part of it — so clicking on the video actually runs both the above event handlers.

When an event is fired on an element that has parent elements (in this case, the `<video>` has the `<div>` as a parent), modern browsers run two different phases — the capturing phase and the bubbling phase.

**In the capturing phase:**

The browser checks to see if the element's outer-most ancestor (`<html>`) has an onclick event handler registered on it for the capturing phase, and runs it if so.
Then it moves on to the next element inside `<html>` and does the same thing, then the next one, and so on until it reaches the element that was actually clicked on.

**In the bubbling phase, the exact opposite occurs:**

The browser checks to see if the element that was actually clicked on has an onclick event handler registered on it for the bubbling phase, and runs it if so.
Then it moves on to the next immediate ancestor element and does the same thing, then the next one, and so on until it reaches the `<html>` element.

Note: In cases where both types of event handlers are present, bubbling and capturing, the capturing phase will run first, followed by the bubbling phase.

To fix the issue:

The standard Event object has a function available on it called stopPropagation() which, when invoked on a handler's event object, makes it so that first handler is run but the event doesn't bubble any further up the chain, so no more handlers will be run.

# Event delegation

Bubbling also allows us to take advantage of event delegation — this concept relies on the fact that if you want some code to run when you click on any one of a large number of child elements, you can set the event listener on their parent and have events that happen on them bubble up to their parent rather than having to set the event listener on every child individually. Remember earlier that we said bubbling involves checking the element the event is fired on for an event handler first, then moving up to the element's parent, etc.?

A good example is a series of list items — if you want each one of them to pop up a message when clicked, you can set the click event listener on the parent `<ul>`, and events will bubble from the list items to the `<ul>`.

**Q: Host objects vs Native (BuiltIn) objects?**

# Host objects

Objects like window, XmlHttpRequest, DOM nodes and so on, which is provided by the browser environment. They are distinct from the built-in objects because not all environment will have the same host objects. If JavaScript runs outside of the browser, for example as server side scripting language like in Node.js, different host objects will be available.

Host objects (assuming browser environment): window, document, location, history, XMLHttpRequest, setTimeout, getElementsByTagName, querySelectorAll, ...

# Native (BuiltIn) objects

Built-in objects: String, Math, RegExp, Object, Function etc. - core predefined objects always available in JavaScript. Defined in the ECMAScript spec.

object in an ECMAScript implementation whose semantics are fully defined by this specification rather than by the host environment.

NOTE Standard native objects are defined in this specification. Some native objects are built-in; others may be constructed during the course of execution of an ECMAScript program.

Native objects: Object (constructor), Date, Math, parseInt, eval, string methods like indexOf and replace, array methods, ...

# User defined objects

User objects: objects defined in JavaScript code. So 'Bird' in your example would be a user object

The JavaScript spec groups built-in objects and user objects together as native objects. This is an unorthodox use of the term "native", since user objects are obviously implemented in JavaScript while the built-ins is most likely implemented in a different language under the hood, just as the host objects would be. But from the perspective of the JavaScript spec, both builtins and user objects are native to JavaScript because they are defined in the JavaScript spec, while host objects are not.

**Q: What is UA?*

# User Agent

to check your own UA, you can visit here and check.https://www.whoishostingthis.com/tools/user-agent/

Good to read:

https://lucybain.com/blog/2014/feature-detection-vs-inference/