# How to


Here you can find a set of examples and how-tos about WPDK in action into a WordPress environment.

Any example and/or how-to is available to anyone through GitHub interface. If you want to download and use these examples
in your environment, you naturally have to install WPDK first: please [follow these rules](Installing WPDK in your WordPress environment) to do that.

* [Hello World! WordPress plugin using WPDK - the basic](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#hello-world-wordpress-plugin-using-wpdk---the-basic)
* [Hello World! WordPress plugin using WPDK - intermediate](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#hello-world-wordpress-plugin-using-wpdk---intermediate)
* [Sample #1 of WordPress plugin using WPDK](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#sample-1-of-wordpress-plugin-using-wpdk) - two submenu item connected to simple view-controllers 
* [Sample #2 of WordPress plugin using WPDK](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#sample-2-of-wordpress-plugin-using-wpdk) - shows all available *WPDK graphic controls* 
* [Sample #3 of WordPress plugin using WPDK](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#sample-3-of-wordpress-plugin-using-wpdk) - two submenu item connected to specialized view-controllers - example of plugin configuration handling
* [Sample #4 of WordPress plugin using WPDK](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#sample-4-of-wordpress-plugin-using-wpdk) - full object oriented WordPress plugin with all features of sample #3
* [Sample #5 of WordPress plugin using WPDK](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#sample-5-of-wordpress-plugin-using-wpdk) - all features of sample #4, with *WPDK autoloading technology* enabled. The final sample.

### Hello World! WordPress plugin using WPDK - the basic

This how-to creates a simple WordPress plugin and generates, through WPDK object `WPDKMenu`, an `Hello World!` menu item
in the administration area of your WordPress environment. This code is very simple, and shows a basic, not *invasive* way
of using WPDK in developing a WordPress plugin.

Please follow these instructions to see this how-to in action in your WordPress environment.

1. If not already done, install WPDK in your environment - please [follow these rules](Installing WPDK in your WordPress environment) to do that.
2. Download the zip of this how-to from official GitHub repository [clicking here](https://github.com/wpXtreme/wpdk-sample-menu-1).
3. Unzip this how-to. You will have its root directory named `wpdk-sample-menu-1-master`
4. Copy the entire `wpdk-sample-menu-1-master` folder in the `wp-content/plugins` directory of your WordPress environment.
5. Activate the plugin in your WordPress administration area: a new `Hello World!` menu item will appear in the main navigation menu at the left side of the screen.
6. The source code of this plugin is well documented, and can be an easy starting point for your develop with WPDK.

### Hello World! WordPress plugin using WPDK - intermediate

This how-to creates a simple WordPress plugin and generates, through WPDK object `WPDKMenu`, an `Hello World!` menu item in the
administration area of your WordPress environment. This code is relatively more complex than first Hello World! example: the plugin
menu is made of two submenu items, each one with its own function called whenever the item is clicked; and the main menu item has an
attached icon, as other main menu item in WordPress menu of Administration Screen.

The plugin menu is built through another WPDK way of creating menu in Administration Screen: as an array, with specific array items,
processed by `renderByArray` static method of `WPDKMenu` class. It is another powerful, readable and easy way to accomplish this task with WPDK.

Please follow these instructions to see this how-to in action in your WordPress environment.

1. If not already done, install WPDK in your environment - please [follow these rules](Installing WPDK in your WordPress environment) to do that.
2. Download the zip of this how-to from official GitHub repository [clicking here](https://github.com/wpXtreme/wpdk-sample-menu-2).
3. Unzip this how-to. You will have its root directory named `wpdk-sample-menu-2-master`
4. Copy the entire `wpdk-sample-menu-2-master` folder in the `wp-content/plugins` directory of your WordPress environment.
5. Activate the plugin in your WordPress administration area: a new `Hello World!` menu item will appear in the main navigation
menu at the left side of the screen, with an icon at the left, and two related submenu items.
6. The source code of this plugin is well documented, and can be an easy starting point for your develop with WPDK.

### Sample #1 of WordPress plugin using WPDK

This how-to is the first basic sample of a WordPress plugin developed using WPDK: a little more complex sample than #1 and #2 above.

This is the structure:

* Create a main menu with two submenu items, through methods `addSubMenu` and `render` of `WPDKMenu` class.
* Connect each submenu item to a specific specialized `WPDKViewController` class instance. These specialized instances handle
the *HTML* output shown in the work area of WordPress Administration Screen, and their source code is in `plugin_root_dir/classes/wpdk-sample-vc.php` file.
* Customize method `display` of any specialized `WPDKViewController` class instance, in order to show my own content whenever
the related submenu item is clicked.

Please follow these instructions to see this how-to in action in your WordPress environment.

1. If not already done, install WPDK in your environment - please [follow these rules](Installing WPDK in your WordPress environment) to do that.
2. Download the zip of this how-to from official GitHub repository [clicking here](https://github.com/wpXtreme/wpdk-sample-plugin-1).
3. Unzip this how-to. You will have its root directory named `wpdk-sample-plugin-1-master`
4. Copy the entire `wpdk-sample-plugin-1-master` folder in the `wp-content/plugins` directory of your WordPress environment.
5. Activate the plugin in your WordPress administration area: a new `WPDK Plug#1` menu item will appear in the main navigation
menu at the left side of the screen, with an icon at the left, and two related submenu items. Click them to see result.
6. The source code of this plugin is well documented, and can be an easy starting point for your develop with WPDK.

### Sample #2 of WordPress plugin using WPDK

This how-to is the second sample of a WordPress plugin developed using WPDK. This is the structure:

* Create a main menu with two submenu items, through methods `addSubMenu` and `render` of `WPDKMenu` class.
* The first submenu item is connected to a specific specialized `WPDKViewController` class instance. This specialized instance
embeds a specific `WPDKView` class that shows all the available **WPDK graphic controls** you can easily use in your own code.
Following this simple use case, you can easily build and customize the views that control all aspects and parameters of your
WordPress creation. This sample doesn't store user choices in a custom configuration: it is only a container of all available *WPDK graphic controls*.
Next how-to will show you how to save and reload your own preferences using the same internal architecture.

Please follow these instructions to see this how-to in action in your WordPress environment.

1. If not already done, install WPDK in your environment - please [follow these rules](Installing WPDK in your WordPress environment) to do that.
2. Download the zip of this how-to from official GitHub repository [clicking here](https://github.com/wpXtreme/wpdk-sample-plugin-2).
3. Unzip this how-to. You will have its root directory named `wpdk-sample-plugin-2-master`
4. Copy the entire `wpdk-sample-plugin-2-master` folder in the `wp-content/plugins` directory of your WordPress environment.
5. Activate the plugin in your WordPress administration area: a new `WPDK Plug#2` menu item will appear in the main navigation menu
at the left side of the screen, with an icon at the left, and two related submenu items. Click them to see result.
6. The source code of this plugin is well documented, and can be an easy starting point for your develop with WPDK.

### Sample #3 of WordPress plugin using WPDK

This how-to is the third sample of a WordPress plugin developed using WPDK. This is the structure:

* Create a main menu with two submenu items, through methods `addSubMenu` and `render` of `WPDKMenu` class.
* The first submenu item is connected to a specific specialized `WPDKViewController` class instance. This specialized instance
embeds a specific `WPDKConfigurationView` class called `ControlsPreferencesView`, that shows a little subset of WPDK graphic
controls driving plugin configuration. You can set values and store them into DB, clicking the Update button; or you can
restore values to their default, clicking the Reset to default button. Following this simple use case, you can easily build
and customize your own plugin configuration, creating a property into `ControlsPreferencesSettingsBranch` model, and setting
its value with a specific WPDK graphic control defined into the `ControlsPreferencesView` specialized view.
* `updatePostData` method of `ControlsPreferencesView` class processes the Update request incoming from related button in the view.
* `resetToDefault` method of `ControlsPreferencesView` class processes the Reset to default request incoming from related button in the view.

Please follow these instructions to see this how-to in action in your WordPress environment.

1. If not already done, install WPDK in your environment - please [follow these rules](Installing WPDK in your WordPress environment) to do that.
2. Download the zip of this how-to from official GitHub repository [clicking here](https://github.com/wpXtreme/wpdk-sample-plugin-3).
3. Unzip this how-to. You will have its root directory named `wpdk-sample-plugin-3-master`
4. Copy the entire `wpdk-sample-plugin-3-master` folder in the `wp-content/plugins` directory of your WordPress environment.
5. Activate the plugin in your WordPress administration area: a new `WPDK Plug#3` menu item will appear in the main navigation
menu at the left side of the screen, with an icon at the left, and two related submenu items. Click them to see result.
6. The source code of this plugin is well documented, and can be an easy starting point for your develop with WPDK.

### Sample #4 of WordPress plugin using WPDK

This how-to is the fourth sample of a WordPress plugin developed using WPDK. 

The structure of this WordPress plugin is a little bit complex than all samples above. It is very close to the best way to develop a WordPress plugin with full *WPDK* support.

These are the main characteristics of this plugin sample:

* Full object oriented structure
* The plugin main skeleton is encapsulated into `WPDKSamplePlugin4` class, defined into `wpdk-sample-plugin-4.php`. This class
extends the basic *WPDK* class `WPDKWordPressPlugin`: please read [The step by step guide to writing a WordPress plugin with
full WPDK support](https://github.com/wpXtreme/wpdk/wiki/The-step-by-step-guide-to-writing-a-WordPress-plugin-with-full-WPDK-support) to
deepen the meaning and the scope of this fundamental *WPDK* class.
* The behaviour of this plugin is totally equal to sample #3. You can read [here](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#sample-3-of-wordpress-plugin-using-wpdk)
all the details. But the creation of plugin menu item in the main navigation menu is now embedded into `WPDKSamplePlugin4Admin` class,
defined into `classes/admin/wpdk-sample-admin.php`. This class extends the basic *WPDK* class `WPDKWordPressAdmin`, that prepares
some facilities and common action/filter hooks useful in all requests that involves administration area of WordPress. The creation
of plugin menu items in WordPress admin area is one of the facility this class prepares for us.

Please follow these instructions to see this how-to in action in your WordPress environment.

1. If not already done, install WPDK in your environment - please [follow these rules](Installing WPDK in your WordPress environment) to do that.
2. Download the zip of this how-to from official GitHub repository [clicking here](https://github.com/wpXtreme/wpdk-sample-plugin-4).
3. Unzip this how-to. You will have its root directory named `wpdk-sample-plugin-4-master`
4. Copy the entire `wpdk-sample-plugin-4-master` folder in the `wp-content/plugins` directory of your WordPress environment.
5. Activate the plugin in your WordPress administration area: a new `WPDK Plug#4` menu item will appear in the main navigation
menu at the left side of the screen, with an icon at the left, and two related submenu items. Click them to see result.
6. The source code of this plugin is well documented, and can be an easy starting point for your develop with WPDK.

### Sample #5 of WordPress plugin using WPDK

This how-to is the fifth, last sample of a WordPress plugin developed using WPDK. 

This sample represents the best way to develop a WordPress plugin with full *WPDK* support. Because it embeds, or it is compliant to, all the main *WPDK* features.

The behaviour of this plugin is totally equal to sample #4. You can read [here](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#sample-4-of-wordpress-plugin-using-wpdk)
all the details. The only sizable difference is the implementation of *WPDK autoloading technology* to the plugin source code,
that deserves some additional notes.

The entire *WPDK framework* uses *WPDK autoloading technology* described [here](https://github.com/wpXtreme/wpdk/wiki/WPDK-Features#wpdk-embeds-object-autoloading).
This technology is not restricted to *WPDK*; it can be used to any plugin that is developed with full *WPDK* support, and
extended to all your source code; thus, you can gain in your own source code the same *WPDK* advantages: **the speed of loading
and execution of your code can be up to 50% faster than normal file inclusion**.

In order to make full and better use of this technology in your plugin source code, these are the rules to follow:

* all source code must be written in object oriented paradigm, i.e. must be embedded in a dedicated class.
* one class - one file. Defining more classes in a single file is naturally possible, but in this way you can loose in performance.

This plugin sample follows these rules. The way to implement *WPDK autoloading technology* in your source code is basically like this:

* remove from your source code all `(require|include)(_once)` related to the internal classes of your project.
* create a private method in the main class of your plugin (the class that extends `WPDKWordPressPlugin`), in which you will
insert the autoloading code. In this sample, the method is called `_registerClasses`.
* inside this method, build a simple array like this:

```php
<?php

$includes = array(
      $this->classesPath . 'admin/wpdk-sample-admin.php'                         => 'WPDKSamplePluginAdmin',
      $this->classesPath . 'config/wpdk-sample-preferences-viewcontrollerc.php'  => 'PreferencesViewController',
      $this->classesPath . 'config/wpdk-sample-preferences.php'                  => 'PreferencesModel',
      $this->classesPath . 'config/about-viewcontroller.php'                     => 'AboutViewController',
      $this->classesPath . 'config/controls-preferences-view.php'                => 'ControlsPreferencesView',
      $this->classesPath . 'config/controls-settings.php'                        => 'ControlsSettings'
    );
```

The key of any element is a PHP file path related to internal files of project, and is always expressed in absolute value.
The related value for any key is the class name defined in the file. *If a file contains two or more classes, set them as an array*,
like this: `array( 'firstclass', 'secondclass' ... )`

* invoke the `registerAutoloadClass` method of `WPDKWordPressPlugin` class, passing the array just created: `$this->registerAutoloadClass( $includes );`.
This is the core method that physically enable autoloading of your code.
* call `_registerClasses` method in the constructor of your main class, and **ensure this calling is ALWAYS the first thing your
constructor does**, in order to avoid inconvenients.

Lo! From now on, *WPDK autoloading technology* is enabled also in your source code. **Server will load and execute the sole
source code related to the HTTP request incoming from client, ignoring all code not involved**.

In this sample, you can see these full settings in the constructor, and `_registerClasses` method, of `WPDKSamplePlugin5`
class (stored in file `wpdk-sample-plugin-5.php`). You can consider this as an easy track for your own develop.

Please follow these instructions to see this how-to in action in your WordPress environment.

1. If not already done, install WPDK in your environment - please [follow these rules](Installing WPDK in your WordPress environment) to do that.
2. Download the zip of this how-to from official GitHub repository [clicking here](https://github.com/wpXtreme/wpdk-sample-plugin-5).
3. Unzip this how-to. You will have its root directory named `wpdk-sample-plugin-5-master`
4. Copy the entire `wpdk-sample-plugin-5-master` folder in the `wp-content/plugins` directory of your WordPress environment.
5. Activate the plugin in your WordPress administration area: a new `WPDK Plug#5` menu item will appear in the main navigation menu at the left side of the screen, with an icon at the left, and two related submenu items. Click them to see result.
6. The source code of this plugin is well documented, and can be an easy starting point for your develop with WPDK.