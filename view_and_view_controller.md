# View and View Controller

In MVC pattern, there is a separation between model and its views. In pure pattern, a model interacts with its views through a controller(s).

WPDK implements this pattern by the use of two fundamental classes, that a developer can (have to) specialize extending them with its own needs: `WPDKView`, and `WPDKViewController` classes.

`WPDKViewController` class exposes methods and properties to manage the whole HTML display into the work area of WordPress Administration Screen. Upon request, it provides a view that can be displayed or interacted with. Often, this view is the root view for a more complex hierarchy of views, implemented by specialized instances of `WPDKView` class. The view controller acts as the central coordinating agent for the view hierarchy, handling exchanges between the views and any relevant controller or data objects.

![View Controller Schema](http://wpxtreme.github.io/wpdk/documentation/images/view-controller.png)

This is the typical hierarchy handled by a specialized instance of `WPDKViewController` class:

 * header with icon and title + optional button add = an instance of `WPDKHeaderView` class.
 * one or more views, that can be specialized instances of `WPDKView` class.

To display your HTML markup content you can choose several methods:

### 1. Overriding `WPDKViewController` `display()` method

Overriding `display` method in specialized `WPDKViewController` class allows a developer to set a custom content for its instances. The same for `WPDKView` class.

```php
<?php
class FirstViewController extends WPDKViewController {
  
  public function __construct()
  {
    parent::__construct( 'first-view-controller', 'Title of First view controller' );
  }
  
  public function display() {
    parent::display();

    echo 'Your content';
  }
}
```

In this way you get the following HTML markup:

```html
<div class="wpdk-view wrap clearfix" id="first-view-controller-view-root" data-type="wpdk-view">
  <div class="wpdk-view clearfix wpdk-header-view clearfix" id="first-view-controller-header-view" data-type="wpdk-view">
    <div class="wpdk-vc-header-icon" id="first-view-controller-header-view" data-type="wpdk-header-view"></div>
  <h2><button class="wpdk-fullscreen"></button>Title of First view controller</h2>
  <div class="wpdk-vc-header-after-title"></div>
  </div>
</div>
Your content
```

As you see from above example, _Your content_, set into `display` method, is out of any `div` container.

### 2. Create your custom `WPDKView`

The best way to manage your custom content is create your custom (and reusable) `WPDKView`

```php
<?php
class SecondViewController extends WPDKViewController {

  public function __construct()
  {
    parent::__construct( 'second-view-controller', 'Title of Second view controller' );

    $view = new CustomView();
    $this->viewHead->addSubview( $view );
  }
}

class CustomView extends WPDKView {

  public function __construct()
  {
    parent::__construct( 'custom-view' );
  }

  public function draw()
  {
    ?>
    <h3>I'm a TAG h4 for second view controller in a custom view</h3>
  <?php
  }
}
```

In this way, instead, your HTML markup will be:

```html
<div class="wpdk-view clearfix wpdk-header-view clearfix" id="second-view-controller-header-view" data-type="wpdk-view">
  <div class="wpdk-vc-header-icon" id="second-view-controller-header-view" data-type="wpdk-header-view"></div>
  <h2><button class="wpdk-fullscreen"></button>Title of Second view controller</h2>
  <div class="wpdk-vc-header-after-title"></div>
  <div class="wpdk-view clearfix" id="custom-view" data-type="wpdk-view">
    <h3>I'm a TAG h4 for second view controller in a custom view</h3>
  </div>
</div>
```

Your custom content is now *wrap into a `<div>`*, or into your view, if you prefer.

Why using this complexity? For `WPDKView` class, to encapsulate specialized behaviours *that can be reusable anywhere*, simply creating a new instance of the specialized `WPDKView` class that implements them.
For `WPDKViewController` class, to centralize handling of low-level HTML into the whole work area of WordPress Administration Screen; you don't need to create everytime by hand all the `<div></div>` parts of your HTML view into the work area: simply set your own specific HTML content overriding `display` method, and then call it, if necessary.

Moreover, the `WPDKView` exposes several useful methods as:

```php
<?php

// Get HTML markup from a view
$html = $view->html();

// Display HTML markup from a view
$view->display();

// Add a sub view; manage hierarchy of views
$view->addSubview( $second_view );

```

To see how all this theory turns to action, go to [WPDK How-To](WPDK How-tos) and get the source code that use this pattern.