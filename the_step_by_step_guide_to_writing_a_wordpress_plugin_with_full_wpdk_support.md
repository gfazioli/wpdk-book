# The step by step guide to writing a WordPress plugin with full WPDK support

Writing a WordPress plugin with full WPDK support means using all the WPDK features in your code to create a solid product, that is fast to execute, and easy to maintain and evolve.

For reaching this goal, you have to follow some simple rules and you have to use some simple tricks in your source code. All of them are described in this page, step by step. If you don't follow them, you can anyway use WPDK for specific tasks; but you loose all the major gains WPDK is ready to give you.

First of all, you have to completely develop your plugin in an object oriented approach, extending some basic WPDK object. This is necessary not only for a better encapsulation of data, but also to make a full use of [WPDK autoloading technology](https://github.com/wpXtreme/wpdk/wiki/How-to-write-a-WordPress-plugin-with-full-WPDK-support#wpdk-autoloading-technology).

Let's assume that you are creating a new WordPress plugin, named `Test Plugin`.

Your first step is defining the main class of your WordPress plugin, your *plugin* from now on. You can define it directly in the plugin main file, the one that contains *the comment header* used by WordPress to recognize and extract informations about any plugin.

In the root directory of your plugin, create a file named `testplugin.php`. Inside this file, insert the WordPress standard comment for recognize this plugin, and the definition of the main class:

```php
<?php

/**
 * Plugin Name: Test Plugin
 * Plugin URI: http://your-domain.com
 * Description: my WordPress plugin with full WPDK support
 * Version: 1.0.0
 * Author: You
 * Author URI: http://your-domain.com
 */

// Include WPDK framework - the root directory name of WPDK may be different.
// Please change the line below according to your environment.
require_once( trailingslashit( dirname( __FILE__ ) ) . 'wpdk-production/wpdk.php' );

// Define of include your main plugin class
if( !class_exists( 'TestPlugin' ) ) 
{
  class TestPlugin extends WPDKWordPressPlugin {
  }
}
```

Please note the declaration of a class named `TestPlugin`, that extends `WPDKWordPressPlugin` class. We have to deepen the behaviour of the `WPDKWordPressPlugin` class, because your main class inherits all things it needs directly from it.

The `WPDKWordPressPlugin` class is one of the most important class of the whole *WPDK framework*. It encapsulates all init procedures for a plugin, and provides the fundamental startup of a plugin in order to make it full compatible with the WPDK standard. You rarely (never) instantiate `WPDKWordPressPlugin` object directly. Instead, you instantiate subclasses of the `WPDKWordPressPlugin` class.

In WPDK environment, this class **must** be used to extend the main class of a plugin: its goal is to initialize the environment in which the plugin itself operates.

In addition to initializing, `WPDKWordPressPlugin` class performs automatically for you a large series of standard procedures needed in normal coding of a WordPress standard Plugin, and gives access to a lot of properties and methods really useful for your develop:

* Gets directly from WordPress comments, and stores in its properties, information about your plugin : plugin name, version, the text and the text domain path.
* Prepares a set of standard properties with most commonly used paths and urls.
* Provides a lot of hooks to wrap (filters and actions) among the most used in WordPress environment.
* Prepares an instance of `WPDKWatchDog` object for your own log.

All properties and methods of this class are documented in **PHPDoc** format compatible with *Doxygen* tool, so you can extract all detailed info and help through your PHP IDE.

The class `TestPlugin`, extending `WPDKWordPressPlugin`, is the main class of your plugin. Through it, you can control every aspect of your plugin and manage what to do
exactly where you want ( in WordPress front end, in WordPress admin area, in both worlds, and so on ). Using this class as a manager, you can write all code you need to fulfil the scope of your plugin.

When WordPress loads your plugin through this file, this class have also to be engaged, through the line:

```php
<?php
    $GLOBALS['TestPlugin'] = new TestPlugin();
```

that you have to put at the end of the class definition. In this way, your plugin becomes up and running, obviously if it was previously activated. Now our test code becomes this:

```php
<?php
    /**
      * Plugin Name: Test Plugin
      * Plugin URI: http://your-domain.com
      * Description: my WordPress plugin with full WPDK support
      * Version: 1.0.0
      * Author: You
      * Author URI: http://your-domain.com
      */

    // Include WPDK framework - the root directory name of WPDK may be different.
    // Please change the line below according to your environment.
    require_once( trailingslashit( dirname( __FILE__ ) ) . 'wpdk-production/wpdk.php' );

    // Define of include your main plugin class
    if( !class_exists( 'TestPlugin' ) ) {
      class TestPlugin extends WPDKWordPressPlugin {
 
        /**
          * Create an instance of TestPlugin class
          */
        public function __construct( $file ) {

          parent::__construct( $file );

        }

      }
    }

    $GLOBALS['TestPlugin'] = new TestPlugin();
```

Please note that creating an instance of `TestPlugin` class *does not mean activating the whole plugin into the WordPress environment*. The physical activation of plugin is as usual demanded to normal WordPress flow.

### Filesystem guideline

In order to get all benefits from *WPDK framework* we suggest you to use a standard organization for your plugin filesystem. The *WPDK framework* prepares for you a set of standard folder reference properties accessible from `TestPlugin` main class instance. The standard plugin filesystem recognised from WPDK has this form:

* **Your Plugin main folder**
  * assets/
    * css/
      * images
    * js/
  * classes/
  * localization/

#### Useful assets

In addition, *WPDK framework* also provides a `database` folder reference:

* **Your Plugin folder**
  * assets/
    * css/
      * images
    * js/
  * classes/
  * localization/
  * database/

This filesystem tree is mapped into the following properties of the `TestPlugin` main class:

```php
<?php
    $this->path
    $this->classesPath
    $this->databasePath
```

In addition, you have also the following `http` URL properties:

```php
<?php
    $this->url
    $this->assetsURL
    $this->cssURL
    $this->imagesURL
    $this->javascriptURL
```

All of these properties are accessible through the instance of `TestPlugin` class you defined above.

> **Remember that mapping is not dynamic!** Paths are not dynamically extracted from your own folder tree; for obvious reasons, all filesystem properties have a constant init. `$this->cssURL`, for example, is always equal to `trailingslashit( plugin_dir_url( $main_file ) ) . "css/";`.

### Plugin activation

The method `activation` of your `TestPlugin` class is invoked every time your plugin is activated. Please note that **activation is not loading**: the activation of a WordPress plugin happens just once, normally through `plugin` page of WordPress admin area, when a user choose to activate a plugin. From that moment on, the plugin becomes *active*, and this method is not invoked anymore.

To override this method and put all the code you need to execute whenever your plugin is activated, you have to declare it into `TestPlugin` class definition, in this way:

```php
<?php

/**
  * Plugin Name: Test Plugin
  * Plugin URI: http://your-domain.com
  * Description: my WordPress plugin with full WPDK support
  * Version: 1.0.0
  * Author: You
  * Author URI: http://your-domain.com
  */

// Include WPDK framework - the root directory name of WPDK may be different.
// Please change the line below according to your environment.
require_once( trailingslashit( dirname( __FILE__ ) ) . 'wpdk-production/wpdk.php' );

// Define of include your main plugin class
if( !class_exists( 'TestPlugin' ) ) {
  class TestPlugin extends WPDKWordPressPlugin {

    /**
      * Create an instance of TestPlugin class
      */
    public function __construct( $file ) {

      parent::__construct( $file );

    }

    // Called when the plugin is activate - only first time
    public function activation() {
      // To override
    }

  }
}

$GLOBALS['TestPlugin'] = new TestPlugin();
```

In `activation` method you can insert the code your plugin eventually needs to execute in plugin activation phase.

### Plugin deactivation

The method `deactivation` of your `TestPlugin` class is invoked every time your plugin is deactivated. The deactivation of a WordPress plugin happens just once, normally through `plugin` page of WordPress admin area, when a user choose to deactivate a plugin. From that moment on, the plugin becomes *inactive*, and this method is not invoked anymore.

To override this method and put all the code you need to execute whenever your plugin is deactivated, you have to declare it into `TestPlugin` class definition, in this way:

```php
<?php
/**
  * Plugin Name: Test Plugin
  * Plugin URI: http://your-domain.com
  * Description: my WordPress plugin with full WPDK support
  * Version: 1.0.0
  * Author: You
  * Author URI: http://your-domain.com
  */

// Include WPDK framework - the root directory name of WPDK may be different.
// Please change the line below according to your environment.
require_once( trailingslashit( dirname( __FILE__ ) ) . 'wpdk-production/wpdk.php' );

// Define of include your main plugin class
if( !class_exists( 'TestPlugin' ) ) {
  class TestPlugin extends WPDKWordPressPlugin {

    /**
      * Create an instance of TestPlugin class
      */
    public function __construct( $file ) {

      parent::__construct( $file );

    }

    // Called when the plugin is activate - only first time
    public function activation() {
      // To override
    }

    // Called when the plugin is deactivated
    public function deactivation() {
      // To override
    }

  }
}

$GLOBALS['TestPlugin'] = new TestPlugin();
```

In `deactivation` method you can insert the code your plugin eventually needs to execute in plugin deactivation phase.

### Plugin loaded

The method `loaded` of your `TestPlugin` class is invoked every time your plugin is loaded. Please note that **loading is not activation**: every single time this plugin is loaded by WordPress environment, this method will be invoked.

To override this method and put all the code you need to execute whenever your plugin is loaded, you have to declare it into `TestPlugin` class definition, in this way:

```php
<?php

/**
  * Plugin Name: Test Plugin
  * Plugin URI: http://your-domain.com
  * Description: my WordPress plugin with full WPDK support
  * Version: 1.0.0
  * Author: You
  * Author URI: http://your-domain.com
  */

// Include WPDK framework - the root directory name of WPDK may be different.
// Please change the line below according to your environment.
require_once( trailingslashit( dirname( __FILE__ ) ) . 'wpdk-production/wpdk.php' );

// Define of include your main plugin class
if( !class_exists( 'TestPlugin' ) ) {
  class TestPlugin extends WPDKWordPressPlugin {

    /**
      * Create an instance of TestPlugin class
      */
    public function __construct( $file ) {

      parent::__construct( $file );

    }

    // Called when the plugin is activate - only first time
    public function activation() {
      // To override
    }

    // Called when the plugin is deactivated
    public function deactivation() {
      // To override
    }

    // Called when the plugin is loaded
    public function loaded() {
      // To override
    }

  }
}

$GLOBALS['TestPlugin'] = new TestPlugin();
```

In `loaded` method you can insert the code your plugin eventually needs to execute in plugin loading.

### Plugin configuration

The method `configuration` of your `TestPlugin` class is invoked every time your plugin is loaded. Please note that **loading is not activation**: every single time this plugin is loaded from WordPress environment, this method will be invoked.

Here you can put all stuffs about the configuration of your plugin: for example, the load of current plugin configuration from WordPress DB; it is a commodity: you can perform the same task in another way. Nevertheless, it can be really useful for you to use this hook, because this method is always executed **AFTER the plugin has been fully loaded from WordPress environment**.

To override this method and put all the code you need to execute whenever your plugin is loaded, you have to declare it into `TestPlugin` class definition, in this way:

```php
<?php

/**
  * Plugin Name: Test Plugin
  * Plugin URI: http://your-domain.com
  * Description: my WordPress plugin with full WPDK support
  * Version: 1.0.0
  * Author: You
  * Author URI: http://your-domain.com
  */

// Include WPDK framework - the root directory name of WPDK may be different.
// Please change the line below according to your environment.
require_once( trailingslashit( dirname( __FILE__ ) ) . 'wpdk-production/wpdk.php' );

// Define of include your main plugin class
if( !class_exists( 'TestPlugin' ) ) {
  class TestPlugin extends WPDKWordPressPlugin {

    /**
      * Create an instance of TestPlugin class
      */
    public function __construct( $file ) {

      parent::__construct( $file );

    }

    // Called when the plugin is activate - only first time
    public function activation() {
      // To override
    }

    // Called when the plugin is deactivated
    public function deactivation() {
      // To override
    }

    // Called when the plugin is loaded
    public function loaded() {
      // To override
    }

    // Called when the plugin is fully loaded
    public function preferences() {
      // To override
    }

  }
}

$GLOBALS['TestPlugin'] = new TestPlugin();
```

In `configuration` method you can insert the code your plugin eventually needs to execute about its configuration.

### Commodity

Your `TestPlugin` main class has also some commodity methods, useful to group together some similar tasks.

For example, with `_defines` method, you can insert the definition of all *PHP* `define` used by your class. You can write your own *PHP* `define` directly in this method, or you can also put your `define` in file `defines.php`, stored whatever in your plugin folders tree, and included by this method.

`_defines()` internal method has to be invoked in the `TestPlugin` constructor. It is not attached to any WordPress action.

Your code, now:

```php
<?php

/**
  * Plugin Name: Test Plugin
  * Plugin URI: http://your-domain.com
  * Description: my WordPress plugin with full WPDK support
  * Version: 1.0.0
  * Author: You
  * Author URI: http://your-domain.com
  */

// Include WPDK framework - the root directory name of WPDK may be different.
// Please change the line below according to your environment.
require_once( trailingslashit( dirname( __FILE__ ) ) . 'wpdk-production/wpdk.php' );

// Define of include your main plugin class
if( !class_exists( 'TestPlugin' ) ) {
  class TestPlugin extends WPDKWordPressPlugin {

    /**
      * Create an instance of TestPlugin class
      */
    public function __construct( $file ) {

      parent::__construct( $file );

      $this->defines();

    }

    /**
      * Include the external file with my own defines
      */
    private function defines() {
      include_once( 'defines.php' );
    }

    /* Called when the plugin is activate - only first time. */
    public function activation() {
      /* To override. */
    }

    /* Called when the plugin is deactivated. */
    public function deactivation() {
      /* To override. */
    }

    /* Called when the plugin is loaded. */
    public function loaded() {
      /* To override. */
    }

    /* Called when the plugin is fully loaded. */
    public function preferences() {
      /* To override. */
    }

  }
}

$GLOBALS['TestPlugin'] = new TestPlugin( __FILE__ );
```

### Writing code in your plugin specifically related to WordPress frontend

The method `theme` of your `TestPlugin` class is called every time your plugin is loaded, after the invocation of `loaded` and `configuration` methods; but this calling happens **if, and only if, the web request is related to the front-end side of WordPress**: that is to say, not related in any way to the admin side of WordPress. Loading is not activation: every single time this plugin is loaded from WordPress environment, this method will be invoked.

To override this method and put all the code you need to execute whenever your plugin is loaded, you have to declare it into `TestPlugin` class definition, in this way:

```php
<?php

/**
  * Plugin Name: Test Plugin
  * Plugin URI: http://your-domain.com
  * Description: my WordPress plugin with full WPDK support
  * Version: 1.0.0
  * Author: You
  * Author URI: http://your-domain.com
  */

// Include WPDK framework - the root directory name of WPDK may be different.
// Please change the line below according to your environment.
require_once( trailingslashit( dirname( __FILE__ ) ) . 'wpdk-production/wpdk.php' );

// Define of include your main plugin class
if( !class_exists( 'TestPlugin' ) ) {
  class TestPlugin extends WPDKWordPressPlugin {

    /**
      * Create an instance of TestPlugin class
      */
    public function __construct( $file ) {

      parent::__construct( $file );

      $this->defines();

    }

    /**
      * Include the external file with my own defines
      */
    private function defines() {
      include_once( 'defines.php' );
    }

    /* Called when the plugin is activate - only first time. */
    public function activation() {
      /* To override. */
    }

    /* Called when the plugin is deactivated. */
    public function deactivation() {
      /* To override. */
    }

    /* Called when the plugin is loaded. */
    public function loaded() {
      /* To override. */
    }

    /* Called when the plugin is fully loaded. */
    public function preferences() {
      /* To override. */
    }

    /* Called only if the web request is related to the front-end side of WordPress */
    public function theme() {
      /* To override. */
    }

  }
}

$GLOBALS['TestPlugin'] = new TestPlugin( __FILE__ );
```

In `theme` method, you can insert all code your plugin needs to execute in the front-end area of your WordPress environment. For example, you can insert here the declaration of a specific class instance that handles all stuffs about front-end area. Or you can directly add here some specific hooks related to front-end WordPress filters, like `the_title` or `the_content`. This gives your plugin more readability and flow comprehension.


### Writing code in your plugin specifically related to WordPress admin area

The method `admin` of your `TestPlugin` class is called every time your plugin is loaded, after the invocation of methods `loaded` and `configuration`; but this calling happens **if, and only if, the web request is related to the admin side of WordPress**. Loading is not activation: every single time this plugin is loaded from WordPress
environment, this method will be invoked.

To override this method and put all the code you need to execute whenever your plugin is loaded, you have to declare it into `TestPlugin` class definition, in this way:

```php
<?php

/**
  * Plugin Name: Test Plugin
  * Plugin URI: http://your-domain.com
  * Description: my WordPress plugin with full WPDK support
  * Version: 1.0.0
  * Author: You
  * Author URI: http://your-domain.com
  */

// Include WPDK framework - the root directory name of WPDK may be different.
// Please change the line below according to your environment.
require_once( trailingslashit( dirname( __FILE__ ) ) . 'wpdk-production/wpdk.php' );

// Define of include your main plugin class
if( !class_exists( 'TestPlugin' ) ) {
  class TestPlugin extends WPDKWordPressPlugin {

    /**
      * Create an instance of TestPlugin class
      */
    public function __construct( $file ) {

      parent::__construct( $file );

      $this->defines();

    }

    /**
      * Include the external file with my own defines
      */
    private function defines() {
      include_once( 'defines.php' );
    }

    /* Called when the plugin is activate - only first time. */
    public function activation() {
      /* To override. */
    }

    /* Called when the plugin is deactivated. */
   public  function deactivation() {
      /* To override. */
    }

    /* Called when the plugin is loaded. */
    public function loaded() {
      /* To override. */
    }

    /* Called when the plugin is fully loaded. */
    public function preferences() {
      /* To override. */
    }

    /* Called only if the web request is related to the front-end side of WordPress */
    public function theme() {
      /* To override. */
    }

    /* Called only if the web request is related to the admin side of WordPress */
    public function admin() {
      /* To override. */
    }

  }
}

$GLOBALS['TestPlugin'] = new TestPlugin( __FILE__ );
```

In `admin` method, you can insert all code your plugin needs to execute in the admin area of your WordPress environment. For example, you can insert here the declaration of a specific class instance that handles all stuffs about admin area ( plugin main menu item creation, css and javascript enqueuing, ecc. ) . Or you can directly add here some specific hooks related to administration WordPress filters, like `menu_order` or `admin_head`.  This gives your plugin more readability and flow comprehension.

### Introduction to available plugin enhancements 

#### WPDKWordPressAdmin class

WPDK has another most important class that encapsulates tasks to perform in the admin side of WordPress: `WPDKWordPressAdmin`. See related documentation or [the How-To section](WPDK How-tos) for all details.

#### WPDK autoloading technology

This guide shows you the basic how-to for developing your plugin in order to make it full compatible with all WPDK features. To make use of powerful *WPDK autoloading technology*, see [the How-To section](WPDK How-tos) for examples of use of this technology integrated in this plugin model.
