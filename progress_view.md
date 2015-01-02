# Progress View

### Overview

Useful UI class to display a progress bar bootstrap style.

#### PHP Class

```php
<?php

$bar             = new WPDKUIProgressBar( '', $percentage, WPDKUIProgressBarType::SUCCESS );
$bar->animated   = true;
$progress        = WPDKUIProgress::init( 'your-id', $bar );
$progress->width = '30%';
$progress->display();
```

#### Javascript

```js

// Chain list of bars
$( '#your-id' ).wpdkProgressBars();

// Change the percentage of first bar
$( '#your-id' ).wpdkProgressBars( 0 ).wpdkProgressBar( { percentage : 50 } );

// Arguments
var args =  {
  percentage         : {integer}|null,
  label              : {string},
  animated           : true|false|null,
  striped            : true|false|null,
  display_percentage : true|false
};

// Remove animation and striped from all childrend bars
$( '#your-id' )
  .wpdkProgressBars()
  .wpdkProgressBar( { animated : false, striped : false } );
```

### Note well

```js

// The following methods do the same thing

// Remove animation
$( '#your-id' )
  .wpdkProgressBars()
  .wpdkProgressBar().toggleClass( 'active', false );

// Remove animation (recommended)
$( '#your-id' )
  .wpdkProgressBars()
  .wpdkProgressBar( { animated : false } );
```
