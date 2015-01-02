# Preferences for users

> DRAFT

In order to store your preferences for each single users, the init of `WPDKPreferences` handle an user id param to perform a user store meta data. For example, if you wish create a preference for the current user just do it:

```php
<?php
// In your subclass
public static function init() {                                                      
  $user_id = get_current_user_id();                                                  
  return parent::init( self::PREFERENCES_NAME, __CLASS__, LAST_VERSION, $user_id );  
}                                                                                    
```

This preference is init with a specific user. In this case will be use `get_user_meta()` to retrive the stored preferences instead the `get_option()`