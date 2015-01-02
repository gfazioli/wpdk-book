# Button Toggle UI Control

### Overview

The toggle button has two state string: `true` and `false`. To default `false`.

```html
<!-- Current state "false" -->
<button class="wpdk-ui-button-toggle"
        data-alternate_label="Start">
  Pause
</button>
```

When you click on the button, the state becomes `true` and the label becomes `Start`. If you click again, the state returns to `false` and the label return to `Pause`. And so on...

```html
<!-- Current state "true" -->
<button class="wpdk-ui-button-toggle"
        date-current_state="true"
        data-alternate_label="Start">
  Pause
</button>
```

In this way you can:

```php
<?php

// Your own state
$state = 'pause';

?>
<!-- Complete markup -->
<button class="wpdk-ui-button-toggle wpdk-ui-button-toggle-<?php echo ( 'pause' == $state ) ? 'true' : 'false' ?>"
        date-current_state="<?php echo ( 'pause' == $state ) ? 'true' : 'false' ?>"
        data-alternate_label="<?php echo ( 'pause' == $state ) ? 'Play' : 'Pause' ?>">
  <?php echo ( 'pause' == $state ) ? 'Pause' : 'Play' ?>
</button>
```

### CSS Classes

In addition you have to set the `wpdk-ui-button-toggle-true` and `wpdk-ui-button-toggle-false` classes in order to apply some custom own styles.

### Control

Also, you can use the `WPDKUIControlButton` class:

```php
<?php

// Prepare item
$item = array(
  'value'   => 'Pause',
  'toggle'  => array( 'true', 'Play' )
);

// Display the complete markup with `wpdk-ui-button-toggle-true` classes too.
WPDKUIControlButton::init( $item )->display();
```

### Javascript Events

```js
$( document ).on( WPDKUIComponentEvents.TOGGLE_BUTTON, function( e, $control, state) {

  // "true" or "false"
  console.log( state );
 }
);
```