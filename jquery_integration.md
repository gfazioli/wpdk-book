# jQuery integration

### Overview

The jQuery is manage by `WPDKjQuery` class in `wpdk.js` core Javascript.

### Autocomplete

WPDK provides a several method to make an autocomplete input text.

#### Autocomplete users

```html
<input type="text"
       name="name_of_control"
       data-autocomplete="users"
       data-delay="500"                                         <!-- Optional -->
       data-min_length="2"                                      <!-- Optional -->
       data-query="['user_login','user_nicename','user_email']" <!-- Optional -->
       data-avatar="true"                                       <!-- Optional -->
       data-avatar_size="32"                                    <!-- Optional -->
       data-target="#my_control_id"
/>
<input type="hidden" id="my_control_id" />
```


## How to refresh components

### Autocomplete

```js
wpdk_do_action( WPDKUIComponents.REFRESH_JQUERY_AUTOCOMPLETE );
```


### Data (time) picker

```js
wpdk_do_action( WPDKUIComponents.REFRESH_JQUERY_DATAPICKER );
```


### Tabs

```js
wpdk_do_action( WPDKUIComponents.REFRESH_JQUERY_TABS );
```