# ![ripplet.js](https://luncheon.github.io/ripplet.js/logo.gif)

Fully controllable vanilla-js material design ripple effect generator.

[Demo](https://luncheon.github.io/ripplet.js/demo/)  


## Installation

### via npm

```bash
$ npm install ripplet.js
```

```javascript
import ripplet from 'ripplet.js';

element.addEventListener('mousedown', ripplet);
```

### via CDN

```html
<script src="https://cdn.jsdelivr.net/npm/ripplet.js"></script>
<script>
  element.addEventListener('mousedown', ripplet);
</script>
```


## API

### ripplet(targetSuchAsMouseEvent[, options]) => HTMLElement

Generate a ripplet immediately.  
In particular, create two elements (one is a circular enlarging element representing ripplet, and the other is a container element to restrict visible area) and remove them when the animation ends. Do nothing else.

#### Parameters

* targetSuchAsMouseEvent: Object (required) (in most cases, pass the received MouseEvent object)

| Property name           | Description                              |
| ----------------------- | ---------------------------------------- |
| currentTarget           | Target element                           |
| clientX                 | Client x-coordinate of center of ripplet |
| clientY                 | Client y-coordinate of center of ripplet |

* options: Object (optional)

| Property name           | Default             | Description           |
| ----------------------- | ------------------- | --------------------- |
| className               | ""                  | Class name to be set for the ripplet element (not for this library to use, but for user to style that element) |
| color                   | "rgba(0, 0, 0, .1)" | Ripplet color         |
| opacity                 | null                | Ripplet opacity (used when alpha channel of color property above is shared and difficult to change) |
| spreadingDuration       | ".4s"               | As its name suggests  |
| spreadingDelay          | "0s"                | As its name suggests  |
| spreadingTimingFunction | "linear"            | As its name suggests  |
| clearingDuration        | "1s"                | As its name suggests  |
| clearingDelay           | "0s"                | As its name suggests  |
| clearingTimingFunction  | "ease-in-out"       | As its name suggests  |

#### Return value

Generated container element (having one child element representing ripplet)


### defaultOptions

You can change the default ripplet options for your app.  
For example:

```javascript
import { defaultOptions } from 'ripplet';

defaultOptions.color = 'rgba(64, 128, 255, .2)';
```

or

```html
<script src="https://cdn.jsdelivr.net/npm/ripplet.js"></script>
<script>
  ripplet.defaultOptions.color = 'rgba(64, 128, 255, .2)';
</script>
```


## Declarative HTML example with vanilla-js (dynamically appended elements ready!)

```html
<div data-ripplet-color="rgba(255, 64, 192, .2)">Click me!</div>
<div data-ripplet-color="rgba(64, 255, 192, .2)">Click me!</div>
<div data-ripplet-color="rgba(64, 192, 255, .2)">Click me!</div>
```

```javascript
window.addEventListener('mousedown', function (event) {
  var currentTarget = event.target.closest('[data-ripplet-color]');
  if (currentTarget) {
    ripplet(
      {
        currentTarget: currentTarget,
        clientX: event.clientX,
        clientY: event.clientY,
      },
      {
        color: currentTarget.getAttribute('data-ripplet-color'),
      }
    );
  }
}, true);
```


## License

WTFPL
