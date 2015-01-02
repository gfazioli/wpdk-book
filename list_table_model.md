# List Table Model

A list table model describe the data show by view controller. Your class have to subclass a generic `WPDKListTableModel` class and provides a set of method to descrive your data. A typical model is

```php
<?php

class MyModel extends WPDKListTableModel {

  // Columns
  const COLUMN_ID = 'id';

  // Actions
  const ACTION_NEW = 'new';

  // Statuses
  const STATUS_PENDING = 'pending';

  // Your custom

  /**
   * Create an instance of MyModel class
   *
   * @brief Construct
   *
   * @return MyModel
   */
  public function __construct()
  {
    // Your init

    // Init the model and process action before wp is loaded
    parent::__construct();
  }
}
```

The model provides several method for data as interface

![image](https://cloud.githubusercontent.com/assets/432181/2547753/3665668e-b656-11e3-831d-ab1e2220c577.png)

As shown in the diagram above, some methods are not present in the interface as it is not required or necessary. For example

* `get_filters()`
* `get_sortable_columns()`
* `current_action()`

### Process data

You'll use the `process_bulk_action` method to process the post data. The process result can be handle by `action_result` property as show below

```php
<?php
...
$this->action_result = WPXSmartShopStats::init()->insert( $_REQUEST );
```

After this, in `process_bulk_action` of view controller, you can check the `action_result` property and display the right alert (success or error). For example

```php
<?php
...
  // Insert
  case WPXSmartShopStats::ACTION_INSERT:

    // Successfully
    if( false === WPXSmartShopStats::init()->action_result ) {
      ...
    }
...
```
4. Class `BookEditView` - file `book-edit-view.php`