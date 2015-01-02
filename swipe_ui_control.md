# Swipe UI Control

### Overview

You can create a Swipe Control in two way

```php
<?php

// UI Controls Layout
$fields = array(
  array(
    array(
      'type'  => WPDKUIControlType::SWIPE,
      'id'    => 'swipe-control',
      'label' => 'Swipe me',
      'title' => 'Hello, I am a swipe',
      'value' => 'off' // init off
    ),
  ),
);

$layout = new WPDKUIControlsLayout( fields );
$layout->display();

```

Or directly

```php
<?php

// UI Controls Layout
$item =     array(
 'id'    => 'swipe-control',
 'label' => 'Swipe me',
 'title' => 'Hello, I am a swipe',
 'value' => 'off' // init off
);

$swipe_control = new WPDKUIControlSwipe( item );
$swipe_control->display();

```

#### Javascript Events

* swipe.wpdk
* change.wpdk.swipe
* changed.wpdk.swipe

The `swipe.wpdk` event is an alias of `click`. It is trigged before the state change, similar to `change`

```js
$( '#myswipe' ).on( WPDKUIComponentEvents.SWIPE, function(e, knob, status )
  {
    console.log( status );  // 'on' or 'off'
  }
);
```

> **NOTE** you can use the `wpdk_is_bool()` global function to improved any "bool" check, as `on`, `off`, `yes`, `no`, ...

```js
$( '#myswipe' ).on( WPDKUIComponentEvents.SWIPE_CHANGE, function(e, knob, status )
  {
    return confirm( 'Are you sure?' );
  }
);
```

> **NOTE** if you change the DOM dynamically, for example if you insert a swipe controls via Ajax or Javascript, **remember** that the `change` event **must be** refreshed because `$( document ).on( '#myswipe', 'onchange', ... )` alias of old `live` doesn't work. We suggest to use `$( '#myswipe' ).off( 'change' )` and then 're-bind' the event. However you can use `$( document ).trigger( WPDKUIComponents.REFRESH_SWIPE )` event to refresh swipe after DOM update.

After the changed

```js
$( '#myswipe' ).on( WPDKUIComponentEvents.SWIPE_CHANGED, function(e, knob, status )
  {
    console.log( 'Status changed in ' + status );
  }
);
```

#### Methods

You can read a swipe status by

```js
var status = $( swipe_control ).wpdkSwipe(); // return 'off' or 'on'
```

And you can set (with animate) a swipe by

```js
$( swipe_control ).wpdkSwipe( 'on' );    // or true
$( swipe_control ).wpdkSwipe( 'off' );   // or false 
```