# Preferences

The `WPDKPreferences` class replace the old `WPDKConfiguration` model. The new architecture contains:

#### Models

* `WPDKPreferences`
* `WPDKPreferencesBrach`

#### UI
* `WPDKPreferencesViewController`
* `WPDKPreferencesView`

> The above classes will be available from 1.1.3 WPDK release.

This new architecture make easy to manage the plugin preferences and its UI.

### Models
To make the whole structure clearer and easier to built classes upon, a branch utility class `WPDKPreferencesBranch` has been added. This class is not mandatory, but is could be pretty useful.

![Model](https://f.cloud.github.com/assets/432181/993803/89663abe-09a1-11e3-819e-50d0863bfa34.png)



As said before, the current `WPDKConfiguration` class has an issue related to reset and updated values. It's not possible to patch it in simple way, so I replaced it with a new class structure:

* `WPDKPreferences`
* `WPDKPreferencesBranch`
* `WPDKPreferencesViewController`
* `WPDKPreferencesView`

The new **Preferences** architecture will be introduced with the 1.1.3 WPDK release. For **backward compatibility** the old **Configuration** architecture will still be supported but it's deprecated..

The following classes will be deprecated with WPDK v1.1.3:

* `WPDKConfiguration`
* `WPDKConfigurationView`

## Introducing WPDKPreferences

The new `WPDKPreferences` architecture is easier and more flexible than the old configuration. In addition I added a preferences view controller to make easily manage the standard common view.
The main difference with the old configuration class model is the post data process: the preferences' main class and its branch now handle the process related to the post data (reset and update). This action is performed at the init of the plugin. This way any changes would be available at the plugin startup phase.

In addition I make easier the subclass process. For instance see below this Maintenance Pro implementation (test):

```php
<?php
/**
 * Maintenace Pro preferences model
 *
 * @class           WPXMaintenanceProPreferences
 * @author          =undo= <info@wpxtre.me>
 * @copyright       Copyright (C) 2012-2013 wpXtreme Inc. All Rights Reserved.
 * @date            2013-08-20
 * @version         1.0.0
 *
 */
class WPXMaintenanceProPreferences extends WPDKPreferences {

  /**
   * The preferences name used on database
   *
   * @brief Preferences name
   *
   * @var string
   */
  const PREFERENCES_NAME = 'wpx-maintenance-pro-preferences';

  /**
   * Your own configuration property
   *
   * @brief Configuration version
   *
   * @var string $version
   */
  public $version = WPXMAINTENANCEPRO_VERSION;

  /**
   * Scheduling
   *
   * @brief Scheduling
   *
   * @var WPXMaintenaceProPreferencesScheduling $scheduling
   */
  public $scheduling;

  /**
   * Template Configuration
   *
   * @brief Template
   *
   * @var WPXMaintenaceProPreferencesTemplate $template
   */
  public $template;

  /**
   * Rules
   *
   * @brief Rules
   *
   * @var WPXMaintenaceProPreferencesRules $rules
   */
  public $rules;

  /**
   * Messages
   *
   * @brief Messages
   *
   * @var WPXMaintenaceProPreferencesMessages $messages
   */
  public $messages;

  /**
   * Return an instance of WPXMaintenanceProPreferences class from the database or onfly.
   *
   * @brief Get the preferences
   *
   * @return WPXMaintenanceProPreferences
   */
  public static function init()
  {
    return parent::init( self::PREFERENCES_NAME, __CLASS__, WPXMAINTENANCEPRO_VERSION );
  }

  /**
   * Set the default
   *
   * @brief Default
   */
  public function defaults()
  {
    $this->scheduling = new WPXMaintenaceProPreferencesScheduling( $this );
    //    $this->template   = new WPXMaintenaceProConfigurationTemplate();
    //    $this->rules      = new WPXMaintenaceProConfigurationRules();
    //    $this->messages   = new WPXMaintenaceProConfigurationMessages();
  }

}


/**
 * Scheduling preferences branch model
 *
 * @class           WPXMaintenaceProPreferencesScheduling
 * @author          =undo= <info@wpxtre.me>
 * @copyright       Copyright (C) 2012-2013 wpXtreme Inc. All Rights Reserved.
 * @date            2013-08-20
 * @version         1.0.0
 *
 */
class WPXMaintenaceProPreferencesScheduling extends WPDKPreferencesBranch {

  const ENABLED     = 'enabled';
  const DATE_START  = 'date_start';
  const DATE_EXPIRE = 'date_expire';

  public $enabled;
  public $date_start;
  public $date_expire;

  /**
   * Set the default configuration
   *
   * @brief Default configuration
   */
  public function defaults()
  {
    $this->enabled     = 'n';
    $this->date_start  = '';
    $this->date_expire = '';
  }

  /**
   * Update this branch
   *
   * @brief Update
   */
  public function update()
  {
    $this->enabled     = isset( $_POST[self::ENABLED] ) ? $_POST[self::ENABLED] : 'n';
    $this->date_start  = WPDKDateTime::format( $_POST[self::DATE_START], 'YmdHi' );
    $this->date_expire = WPDKDateTime::format( $_POST[self::DATE_EXPIRE], 'YmdHi' );

    parent::update();
  }

}
```

As you see above, the `init` method is more simple:

```php
<?php
  public static function init()
  {
    return parent::init( self::PREFERENCES_NAME, __CLASS__, WPXMAINTENANCEPRO_VERSION );
  }
```

To make the whole structure clearer and easier to built classes upon, a branch utility class `WPDKPreferencesBranch` has been added. This class is not mandatory, but it could be pretty helpful.
Remember that any **branch** must follow a strict interface. For example you need to implement the new `update()` and `defaults()` methods.

### View and view controller

A new preferences view controller has been added as well. See below for example:

```php
<?php
/**
 * Maintenance Pro preferences view controller
 *
 * @class           WPXMaintenanceProPreferencesViewController
 * @author          =undo= <info@wpxtre.me>
 * @copyright       Copyright (C) 2012-2013 wpXtreme Inc. All Rights Reserved.
 * @date            2013-08-20
 * @version         1.0.0
 *
 */
class WPXMaintenanceProPreferencesViewController extends WPDKPreferencesViewController {

  const ID = 'wpx-maintenance-tabs';

  /**
   * Create an instance of WPXMaintenanceProPreferencesViewController class
   *
   * @brief Construct
   *
   * @return WPXMaintenanceProPreferencesViewController
   */
  public function __construct()
  {
    $scheduling = new WPXMaintenanceProPreferencesSchedulingView();

    /* Create each single tab. */
    $tabs = array(
      new WPDKjQueryTab( $scheduling->id, __( 'Scheduling', WPXMAINTENANCEPRO_TEXTDOMAIN ), $scheduling->html() ),
      //      new WPDKjQueryTab( 'wpx-maintenance-pro-template', __( 'Template', WPXMAINTENANCEPRO_TEXTDOMAIN ), $template->html() ),
      //      new WPDKjQueryTab( 'wpx-maintenance-pro-rules', __( 'Rules', WPXMAINTENANCEPRO_TEXTDOMAIN ), $rules->html() ),
      //      new WPDKjQueryTab( 'wpx-maintenance-pro-messages', __( 'Messages', WPXMAINTENANCEPRO_TEXTDOMAIN ), $messages->html() ),
    );

    parent::__construct( self::ID, __( 'Maintenance settings', WPXMAINTENANCEPRO_TEXTDOMAIN ), $tabs );

  }

  /**
   * Used to load Javascript or styles
   *
   * @brief Before load the view
   */
  public static function didHeadLoad()
  {
    wp_enqueue_script( 'wpx-maintenance-pro-preferences', WPXMAINTENANCEPRO_URL_JAVASCRIPT .
      'wpx-maintenance-pro-configuration.js', array( 'jquery' ), WPXMAINTENANCEPRO_VERSION, true );
  }

}
```

This view controller makes it easier to build tabbed view that feature reset and update buttons.
Also, the new `WPDKPreferencesView` is more light:

```php
<?php
/**
 * Maintenance Pro scheduling view preferences
 *
 * @class           WPXMaintenanceProPreferencesSchedulingView
 * @author          =undo= <info@wpxtre.me>
 * @copyright       Copyright (C) 2012-2013 wpXtreme Inc. All Rights Reserved.
 * @date            2013-08-20
 * @version         1.0.0
 *
 */
class WPXMaintenanceProPreferencesSchedulingView extends WPDKPreferencesView {

  /**
   * Create an instance of WPXMaintenanceProPreferencesSchedulingView class
   *
   * @brief Construct
   *
   * @return WPXMaintenanceProPreferencesSchedulingView
   */
  public function __construct()
  {
    $preferences = WPXMaintenanceProPreferences::init();
    parent::__construct( $preferences, 'scheduling' );
  }

  /**
   * Return fields array
   *
   * @brief Fields
   *
   * @return array
   */
  public function fields()
  {
    /**
     * @var WPXMaintenaceProPreferencesScheduling $scheduling
     */
    $scheduling = $this->branch;

    $fields = array(
      __( 'Maintenance mode', WPXMAINTENANCEPRO_TEXTDOMAIN ) => array(
        array(
          array(
            'type'  => WPDKUIControlType::SWIPE,
            'name'  => WPXMaintenaceProPreferencesScheduling::ENABLED,
            'label' => __( 'Enable Now', WPXMAINTENANCEPRO_TEXTDOMAIN ),
            'title' => __( 'If you enable this option the starting and ending dates below will be ignored.', WPXMAINTENANCEPRO_TEXTDOMAIN ),
            'value' => $scheduling->enabled
          )
        ),
        array(
          array(
            'type'  => WPDKUIControlType::DATETIME,
            'name'  => WPXMaintenaceProPreferencesScheduling::DATE_START,
            'label' => __( 'Starting date', WPXMAINTENANCEPRO_TEXTDOMAIN ),
            'value' => WPDKDateTime::format( $scheduling->date_start )
          )
        ),
        array(
          array(
            'type'   => WPDKUIControlType::DATETIME,
            'name'   => WPXMaintenaceProPreferencesScheduling::DATE_EXPIRE,
            'label'  => __( 'Ending date', WPXMAINTENANCEPRO_TEXTDOMAIN ),
            'value'  => WPDKDateTime::format( $scheduling->date_expire ),
            'append' => sprintf( ' <strong>%s</strong>: %s', __( 'Date on server', WPXMAINTENANCEPRO_TEXTDOMAIN ), date( __( 'm/d/Y H:i', WPXMAINTENANCEPRO_TEXTDOMAIN ) ) )
          )
        ),
      )
    );

    return $fields;
  }

}
```
