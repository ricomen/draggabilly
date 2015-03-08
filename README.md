# Draggabilly

<div class="example-frame">
  <div class="example">
    <div id="basic" class="draggie">
      <div class="total-centered">Drag me</div>
    </div>
  </div>
</div>

<p class="tagline">Make that shiz draggable</p>

[github.com/desandro/draggabilly](http://github.com/desandro/draggabilly)

Rad because it supports IE8+ and multi-touch.

## Install

Grab a packaged source file:

+ [draggabilly.pkgd.min.js](http://draggabilly.desandro.com/draggabilly.pkgd.min.js) for production
+ [draggabilly.pkgd.js](http://draggabilly.desandro.com/draggabilly.pkgd.js) for development

Install with [Bower](http://bower.io): `bower install draggabilly`

Install with [npm](https://www.npmjs.com/package/draggabilly): `npm install draggabilly`

## Usage

Initialize Draggabilly as a jQuery plugin

``` js
var $draggable = $('.draggable').draggabilly({
  // options...
})
```

Initialize Draggabilly with vanilla JS

``` js
var elem = document.querySelector('.draggable');
var draggie = new Draggabilly( elem, {
  // options...
});

// or pass in selector string as first argument
var draggie = new Draggabilly( '.draggie', {
  // options...
});
```

When the user first presses down, Draggabillly will add the class `.is-pointer-down` to the element. When dragging, Draggabillly will add the class `.is-dragging` to the element.

## Options

### axis

<div class="example-frame">
  <div id="axised" class="example">
    <div class="draggie draggie--squat">
      <div class="total-centered">axis: 'x'</div>
    </div>
  </div>
</div>

**Type:** _String_

**Values:** `'x'` or `'y'`

``` js
axis: 'x'
```

Constrains movement to horizontal or vertical axis.

### containment

<div class="example-frame">
  <div id="container" class="example">
    <div class="draggie"></div>
    <div class="draggie"></div>
    <div class="draggie"></div>
  </div>
</div>

**Type:** _Element_, Selector _String_, or _Boolean_

``` js
containment: '.container'
```

Contains movement to the bounds of the element. If `true`, the container will be the parent element.

### grid

<div class="example-frame">
  <div id="gridded" class="example">
    <div class="draggie draggie--squat">
      <div class="total-centered">grid: [ 20, 20 ]</div>
    </div>
  </div>
</div>

**Type:** _Array_

**Values:** `[ x, y ]`

``` js
grid: [ 20, 20 ]
```

Snaps the element to a grid, every x and y pixels.

### handle

<div class="example-frame">
  <div class="example">
    <div id="has-handle" class="draggie">
      <div class="handle"></div>
    </div>
  </div>
</div>

**Type:** Selector _String_

``` js
handle: '.handle'
```

Specifies on what element the drag interaction starts.

`handle` is useful for when you do not want all inner elements to be used for dragging, like inputs and forms. See [back handle example on CodePen](http://codepen.io/desandro/pen/znAuH).

## Events

Bind events with jQuery with standard jQuery event methods `.on()`, `.off()`, and `.one()`.

<div class="example-frame">
  <div id="evented" class="example">
    <pre><code>


</code></pre>
    <div class="draggie"></div>
  </div>
</div>

``` js
// jQuery
function listener(/* parameters */) {
  console.log('eventName happened');
}
// bind event listener
$draggable.on( 'eventName', listener );
// unbind event listener
$draggable.off( 'eventName', listener );
// bind event listener to trigger once. note ONE not ON
$draggable.one( 'eventName', function() {
  console.log('eventName happened just once');
});
```

Bind events with vanilla JS with `.on()`, `.off()`, and `.once()` methods.

Draggabilly is an Event Emitter. You can bind event listeners to events.

``` js
// vanilla JS
function listener(/* parameters */) {
  console.log('eventName happened');
}
// bind event listener
draggie.on( 'eventName', listener );
// unbind event listener
draggie.off( 'eventName', listener );
// bind event listener to trigger once. note ONCE not ONE or ON
draggie.once( 'eventName', function() {
  console.log('eventName happened just once');
});
```

### dragStart

Triggered when dragging starts and the element starts moving.

```js
// jQuery
$draggable.on( 'dragStart', function( event, pointer ) {...})
// vanilla JS
draggie.on( 'dragStart', function( event, pointer ) {...})
```

+ `event` - **Type:** _Event_ - the original `mousedown` or `touchstart` event
+ `pointer` - **Type:** _MouseEvent_ or _Touch_ - the event object that has `.pageX` and `.pageY`

### dragMove

Triggered when dragging moves.

```js
// jQuery
$draggable.on( 'dragMove', function( event, pointer, moveVector ) {...})
// vanilla JS
draggie.on( 'dragMove', function( event, pointer, moveVector ) {...})
```

+ `event` - **Type:** _Event_ - the original `mousemove` or `touchmove` event
+ `pointer` - **Type:** _MouseEvent_ or _Touch_ - the event object that has `.pageX` and `.pageY`
+ `moveVector` **Type:** _Object_ - How far the pointer has moved from its start position `{ x: 20, y: -30 }`

### dragEnd

Triggered when dragging ends.

```js
// jQuery
$draggable.on( 'dragEnd', function( event, pointer ) {...})
// vanilla JS
draggie.on( 'dragEnd', function( event, pointer ) {...})
```

+ `event` - **Type:** _Event_ - the original `mouseup` or `touchend` event
+ `pointer` - **Type:** _MouseEvent_ or _Touch_ - the event object that has `.pageX` and `.pageY`

### pointerStart

Triggered when the user's pointer (mouse, touch, pointer) presses down.

```js
// jQuery
$draggable.on( 'pointerStart', function( event, pointer ) {...})
// vanilla JS
draggie.on( 'pointerStart', function( event, pointer ) {...})
```

+ `event` - **Type:** _Event_ - the original `mousedown` or `touchstart` event
+ `pointer` - **Type:** _MouseEvent_ or _Touch_ - the event object that has `.pageX` and `.pageY`

### pointerMove

Triggered when the user's pointer moves.

```js
// jQuery
$draggable.on( 'pointerMove', function( event, pointer, moveVector ) {...})
// vanilla JS
draggie.on( 'pointerMove', function( event, pointer, moveVector ) {...})
```

+ `event` - **Type:** _Event_ - the original `mousemove` or `touchmove` event
+ `pointer` - **Type:** _MouseEvent_ or _Touch_ - the event object that has `.pageX` and `.pageY`
+ `moveVector` **Type:** _Object_ - How far the pointer has moved from its start position `{ x: 20, y: -30 }`

### pointerUp

Triggered when the user's pointer unpresses.

```js
// jQuery
$draggable.on( 'pointerUp', function( event, pointer ) {...})
// vanilla JS
draggie.on( 'pointerUp', function( event, pointer ) {...})
```

+ `event` - **Type:** _Event_ - the original `mouseup` or `touchend` event
+ `pointer` - **Type:** _MouseEvent_ or _Touch_ - the event object that has `.pageX` and `.pageY`

### staticClick

Triggered when the user's pointer is pressed and unpressed and has not moved enough to start dragging.

`click` events are hard to detect with draggable UI, as they are triggered whenever a user drags. Draggabilly's staticClick event resolves this, as it is triggered when the user has not dragged.

```js
// jQuery
$draggable.on( 'staticClick', function( event, pointer ) {...})
// vanilla JS
draggie.on( 'staticClick', function( event, pointer ) {...})
```

+ `event` - **Type:** _Event_ - the original `mouseup` or `touchend` event
+ `pointer` - **Type:** _MouseEvent_ or _Touch_ - the event object that has `.pageX` and `.pageY`

## Methods

### disable

``` js
// jQuery
$draggable.draggabilly('disable')
// vanilla JS
draggie.disable()
```

### enable

``` js
// jQuery
$draggable.draggabilly('enable')
// vanilla JS
draggie.enable()
```

### destroy

``` js
// jQuery
$draggable.draggabilly('destroy')
// vanilla JS
draggie.destroy()
```

### jQuery.fn.data('draggabilly')

Get the Draggabilly instance from a jQuery object. Draggabilly instances are useful to access Draggabilly properties.

``` js
var draggie = $('.draggie').data('draggabilly')
// access Draggabilly properties
console.log( 'draggie at ' + draggie.position.x + ', ' + draggie.position.y )
```

## Properties

### position

`{ x: 20, y: -30 }`

+ `x` _Integer_
+ `y` _Integer_

## RequireJS

Draggabilly works with [RequireJS](http://requirejs.org).

You can require [draggabilly.pkgd.js](http://draggabilly.desandro.io/draggabilly.pkgd.js).

``` js
requirejs( [
  'path/to/draggabilly.pkgd.js',
], function( Draggabilly ) {
  new Draggabilly( ... );
});
```

Or, you can manage dependencies with [Bower](http://bower.io). Set `baseUrl` to `bower_components` and set a path config for all your application code.

``` js
requirejs.config({
  baseUrl: 'bower_components/',
  paths: { // path your your app
    app: '../'
  }
});

requirejs( [
  'draggabilly/draggabilly',
  'app/my-component.js'
], function( Draggabilly, myComp ) {
  new Draggabilly( ... );
});
```

## License

Draggabilly is released under the [MIT License](http://desandro.mit-license.org/). Have at it.
