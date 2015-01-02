# List Table

### Overview

The `WPDKListTableViewController` is an extension of WordPress `WP_List_Table`. In the WPDK environment the view is separated by the data model. In WordPress `WP_List_Table` combine view and data.

![Graph](https://cloud.githubusercontent.com/assets/432181/2539227/129ab122-b5c6-11e3-8770-6de77d1eef51.png)

### Subclass WP_List_Table

So, the `WPDKListTableViewController` starts subclassing the `WP_List_Table` WordPress class. A simple skeleton for your own List Table view controller is

```php
<?php

class MyListTableViewController extends WPDKListTableViewController {

   // Used to store the items per page
   const OPTION = 'my_list_per_page';

  /**
   * Override the model property with your model
   *
   * @brief Model
   *
   * @var MyListTableModel $model
   */
  public $model;

  /**
   * Create an instance of WPXShortcodesManagerShortcodesViewController class
   *
   * @brief Construct
   *
   * @return WPXShortcodesManagerShortcodesViewController
   */
  public function __construct()
  {
    // Get your model
    $this->model = MyListTableModel::init();

    // Standard List Table args
    $args = array(
      'singular' => MyListTableModel::COLUMN_ID,
      'plural'   => 'my_items',
      'ajax'     => false,
      
      // @since 1.5.16 - WPDK extra
      'wpdk_request_status' => 'status',
      'wpdk_default_status' => WPDKDBTableRowStatuses::ALL,
      'wpdk_default_action' => WPDKDBListTableModel::ACTION_EDIT,
    );
    parent::__construct( 'my-id', __( 'My Title' ), $args );
  }

  // TODO implement a static init method to improve instance performance
}
```

Your `WPDKListTableViewController` provides all view/output method. All logic and model data are in the `WPDKListTableModel`.

The `WPDKListTableViewController` class also provides

```php
<?php

  // Load and admin head
  public function load() {}
  public function admin_head() {}

  // Extra table nav, inherith by WP_List_Table
  public function extra_tablenav() {}

  // Column contain
  public function column_default() {}

  // Actions view - this method is called after process_bulk_action() in model
  public function process_bulk_action() {}

```

#### Custom Rows

You can customize your row by override this method

```php
<?php
/**
 * Generates content for a single row of the table.
 *
 * @brief Row
 * @note  This method override the parent
 *
 * @param object $item The current item
 */
public function single_row( $item )
{
  // Custom row
  echo '<tr class="my-class">';

  // Parent
  $this->single_row_columns( $item );
  echo '</tr>';
}
```

Also, you can avoid the checkbox columns by using this method

```php
<?php
/**
 * Return TRUE to display the checkbox, FALSE otherwise
 *
 * @brief Standard checkbox for group actions
 * @since 1.5.5
 * @note  You can override this method for your custom view. This method is called only there is a column named "cb"
 *
 * @param array $item The single item from items
 *
 * @return bool
 */
public function column_checkbox( $item )
{
  return true;
}
```

or directly

```php
<?php
/**
 * Return the HTML markup for the checkbox element used for multiple selections.
 *
 * @brief Standard checkbox for group actions
 * @note  Please, do not override this method directly, but use `column_checbox` instead
 *
 * @param array $item The single item from items
 *
 * @return string
 */
public function column_cb( $item )
{
  if( ! $this->column_checkbox( $item ) ) {
    return;
  }
  $name  = $this->args['singular'];
  $value = $item[ $name ];
  return sprintf( '<input type="checkbox" name="%s[]" value="%s" />', $name, $value );
}
```
4. Class `BookEditView` - file `book-edit-view.php`