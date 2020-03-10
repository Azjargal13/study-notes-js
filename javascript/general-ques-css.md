# General question CSS

Difference between CSS animation and Javascript animation?

resource used:
- https://developers.google.com/web/fundamentals/design-and-ux/animations/css-vs-javascript
- https://css-tricks.com/myth-busting-css-animations-vs-javascript/
## CSS animation

- Mostly used for simpler "one-shot" transitions, like toggling UI element states.
- It's ideal to use self-contained states for UI elements such as CSS transitions and animations.
- with CSS animations, the animation can be defined itself independently of the target element and use `animation-name` property to choose required animation.
- Lack of independent scale/rotation/position control. Because in CSS, they're all bundled into `transform` property.

## Javascript animation
  
- Mostly used for advanced effects such as bouncing, stop, pause, rewind or slow down.
- with JS, use the Web animations API.
- Web animations API is the standards-based approach. Provides real objects, ideal for complex object-oriented applications.
- using `requestAnimationFrame` directly when you want to orchestrate an entire scene by hand. (advanced JS approach, helpful for building game or drawing to an HTML canvas)
- gives more power to developer yet more complex than writing CSS transitions or animations.
- JS animations are not declarative its imperative, as it is written as inline part of the code.
- By default, we animations only modify the presentation of an element.