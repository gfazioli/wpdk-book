# Table View

### Overview

The class `WPDKUITableView` is useful to create a subclass to display a table data.

#### Components

In order to display the table view with right style, you have to use:

```php
<?php
WPDKUIComponents::init()->enqueue( WPDKUIComponents::TABLE );
```

#### Typical subclass

Typically you will subclass `WPDKUITableView`.

```php
<?php

class MyTable extends WPDKUITableView {

  private $_model;

  public function init( $model ) 
  {
    static $instance = null;
    if ( is_null( $instance ) ) {
      $instance = new self( $model );
    }

    return $instance;
  }

public function __construct( $model = null )
  {
    parent::__construct( 'your-id' );

    // Save the model
    $this->_model = $model;
  }  

public function columns()
  {
    $columns = array(
      'column-id'  => __( 'Column Label Name' ),
    );

    return $columns;
  }

  public function items()
  {
    $items = array();

    // Process your model to generate the rows

    $items[] = array(
      'column-id' => 'value',
    );
  }

  public function column( $item, $column_key )
  {
    switch ( $column_key ) {
      case 'column-id':
        // Simple or custom format
        return $item[ $column_key ]
        break;
    }
  }

}

```