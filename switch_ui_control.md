### Overview

The Switch UI Control button replace the old deprecated Swipe button.
This control is similar to a input checkbox.

![image](https://cloud.githubusercontent.com/assets/432181/5614329/5820e48c-94f0-11e4-9dc5-70cca8e17846.png)

```php
<?php

// UI Controls Layout
$fields = array(
  array(
    array(
      'type'  => WPDKUIControlType::SWITCH_BUTTON,
      'id'    => 'swipe-control',
      'label' => 'Swipe me',
      'title' => 'Hello, I am a swipe',
      'value' => true
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
 'value' => false
);

$swipe_control = new WPDKUIControlSwitch( item );
$swipe_control->display();
```

### Ajax integration

You can fire an Ajax action automatically

```php
<?php

// UI Controls Layout
$fields = array(
  array(
    array(
      'type'      => WPDKUIControlType::SWITCH_BUTTON,
      'id'        => 'swipe-control',
      'on_switch' => 'my_action',
      'label'     => 'Swipe me',
      'title'     => 'Hello, I am a swipe',
      'value'     => true
    ),
  ),
);

$layout = new WPDKUIControlsLayout( fields );
$layout->display();
```

When switch the control will fire an action `wp_ajax_{$on_switch}`.

### Javascript

You can get one or more switch ui controls by:

```js

var $switches = wpdkSwitches();

var $switches = $( document ).wpdkSwitches();

var $switches = $( '#my.form' ).wpdkSwitches();

var $switch = $( '#switch-control' );

```

#### Actions and Filters



When you switch the control will be fire a filter and an action:

```js

/**
 * Filter the switch state before change.
 *
 * @param {boolean} state The switch state.
 * @param {*} control The switch control.
 */
wpdk_apply_filters( 'wpdk_ui_switch_state', options, $this );

/**
 * Fires when a swipe is changed.
 *
 * @param {object} $control The swipe control.
 * @param {string} status The swipe status 'on'.
 */
wpdk_do_action( 'wpdk_ui_switch_changed', options, $this );
```

You can use the filter in order to change the state before switch control changed the state.
You can use the action to catch the state changed. See also events below.

#### Events

To check "on" or "off" state use `$( this ).is( ':checked' )`

```js
$( '#swipe-control' ).on( 'change', function()
  {
    console.log( $( this ).is( ':checked' ) );  // true/false
  }
);
```

#### Methods

You can read a switch state by

```js
var status = $( '#switch-control' ).wpdkSwitch( 'state' ); // return true or false
```

And you can set (with animate) a switch by

```js
$( '#switch-control' ).wpdkSwitch( 'state', true );  
$( '#switch-control' ).wpdkSwitch( 'state', false ); 
```

> NOTE: if you change the state the `change` event will be fire

And you can toggle (with animate) a switch by

```js
$( '#switch-control' ).wpdkSwitch( 'toggle' );  
```