# Cron

### Overview

Cron is how WordPress handles scheduled events. The term cron comes from the time - based job scheduler in UNIX. WordPress uses cron for various core functionality. These scheduled jobs include checking for new versions of WordPress, checking for plugin and theme updates, and publishing scheduled posts.

#### How Is Cron Executed?

One of the common misconceptions about cron in WordPress is that cron is always running, looking for tasks to execute. This actually isn't true. Cron is run when a frontend or admin page is loaded on your web site. Every time a page is requested, WordPress checks if there are any cron jobs to run. Any visit to your Web site can trigger cron, whether from a visitor or a search engine bot.

This is also one of the caveats of cron. Because cron runs on page load, it is not 100% precise. If you
have a scheduled cron job to run at midnight, but your Web site lacks adequate traffic, the scheduled
job may not run until 12:30 a.m. or later because no one is on your Web site that late.

### Scheduling cron events

Two types of cron events can be scheduled in WordPress: single and recurring. A recurring event is
a cron job that runs on a schedule and has a set recurring time in which it will run again. A single
event runs once and never runs again until it is rescheduled.

### The WPDK Cron

WPDK provides a several class to manage WordPress cron

* [WPDKCron](#wpdkcron)
* [WPDKCronController](#wpdkcroncontroller)
* [WPDKCronSchedules](#wpdkcronschedules)
* [WPDKRecurringCron](#wpdkrecurringcron)
* [WPDKSingleCron](#wpdksinglecron)

### WPDKCron

This is the most important and useful class. You can subclass `WPDKCron` to create any single or recurring cron.

#### Single or One-Time

```php
<?php

class MySingleCron extends WPDKCron {

  // Construct
  public function __construct() 
  {
    parent::__construct( 'name_of_event', time()+60 );
  }

  // Event
  public function cron()
  {
    // Hello
  }
}
```

#### Recurring

```php
<?php

class MyRecurringCron extends WPDKCron {

  // Construct
  public function __construct() 
  {
    parent::__construct( 'name_of_event', false, 'hourly' );
  }

  // Event
  public function cron()
  {
    // Hello, next start in 60 minutes
  }
}
```


### Utility class

`WPDKSingleCron` and `WPDKRecurringCron` are an alias of `WPDKCron`. These classes are useful to create single or recurring cron in easy way

#### WPDKSingleCron

```php
<?php

class MySingleCron extends WPDKSingleCron {

  // Construct
  public function __construct() 
  {
    parent::__construct( 'name_of_event', time()+60 );
  }

  // Event
  public function cron()
  {
    // Hello
  }
}
```

#### WPDKRecurringCron

```php
<?php

class MyRecurringCron extends WPDKRecurringCron {

  // Construct
  public function __construct() 
  {
    parent::__construct( 'name_of_event', 'hourly' );
  }

  // Event
  public function cron()
  {
    // Hello, next start in 60 minutes
  }
}
```

### WPDKCronSchedules

This class add some recurring time to standard WordPress schedules defines

```php
<?php

const HALF_HOUR   = 'wpdk_half_hour';
const TWO_MINUTES = 'wpdk_two_minutes';
```

You can use these new schedules by `WPDKCronSchedules::HALF_HOUR`, for example

```php
<?php

class MyRecurringCron extends WPDKRecurringCron {

  // Construct
  public function __construct() 
  {
    parent::__construct( 'name_of_event', WPDKCronSchedules::HALF_HOUR );
  }

  // Event
  public function cron()
  {
    // Hello, next start in 30 minutes (1/2 hour)
  }
}
```


### WPDKCronController

This class provides two utility methods to remove single or all cron jobs.


## Where ?

A cron can be added during the activation of a plugin. We must also remember to delete it when the plugin is disabled. For example:

```php
<?php
/**
 * Catch for activation. This method is called one shot.
 *
 * @brief Activation
 */
public function activation()
{
  // Init cron
  WPXSSCouponDeleteExpiredRecurringCron::init();
}
/**
 * Catch for deactivation. This method is called when the plugin is deactivate.
 *
 * @brief Deactivation
 */
public function deactivation()
{
  WPXSSCouponDeleteExpiredRecurringCron::init()->remove();
}
```