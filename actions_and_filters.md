# Actions and Filters

WPDK replicate the php actions and filters. You can use:

* `wpdk_add_action()`
* `wpdk_add_filter()`
* `wpdk_do_action()`
* `wpdk_apply_filters()`

This function are similar to php with the only difference on accepets parameters number. This arguments is not necessary.

### Actions

```js

// Add action
wpdk_add_action( 'test_action', test_action );

// Action function
function test_action()
{
  console.log( 'Fires test_action' );
}

wpdk_do_action( 'test_action' );
```

### Filters


```js

// Add filter
wpdk_add_filter( 'test_filter', test_filter );

// Filter function
function test_filter( value )
{
  value = 'Hello';

  return value;
}

var value = wpdk_apply_filters( 'test_filter', 'none' );
// value = 'Hello'
```




