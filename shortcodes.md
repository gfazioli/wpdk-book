# Shortcodes

The WPDK makes available a very useful set of WordPress shortcodes.

* [wpdk_is_user_logged_in](#wpdk_is_user_logged_in)
* [wpdk_is_user_not_logged_in](#wpdk_is_user_not_logged_in)
* [wpdk_gist](#wpdk_gist)
* [wpdk_geo](#wpdk_geo)

### wpdk_is_user_logged_in

In your posts, pages or custom post type you can use these shortcode to display a part of content only when an user is or not logged in. For instance:

```
This content is visible to all user

[wpdk_is_user_logged_in]
This content is visibile for users logged in
[/wpdk_is_user_logged_in]
```

likewise...

### wpdk_is_user_not_logged_in

```
This content is visible to all user

[wpdk_is_user_not_logged_in]
This content is visibile for users NOT logged in
[/wpdk_is_user_not_logged_in]
```

Starting from v1.3.1 release, we addressed several improvements to `[wpdk_is_user_logged_in]` in order to filter a specific users type.
Now you can set some special attributes to limit the range of users logged.

#### Attributes supported since 1.3.1

* roles – A list of roles string, comma separated. Eg: administrator, subscriber
* caps – A list of capabilities string, comma separated. Eg. read, level_0
* emails – A list of emails string, comma separated. Eg. a.agima@commodore.com, c.sf@gmail.com
* ids – A list of user id, comma separated. Eg. 12,13,14

Let me show you some amazing examples:

```
[wpdk_is_user_logged_in roles='subscriber']
This content is visibile for users logged in with role subscriber
[/wpdk_is_user_logged_in]
```

```
[wpdk_is_user_logged_in roles='subscriber' caps="adv_perm, adv_read"]
This content is visibile for users logged in with role subscriber
and capabilities "adv_perm" and "adv_read"
[/wpdk_is_user_logged_in]
```

```
[wpdk_is_user_logged_in emails='a.agima@commodore.com']
This content is visibile for a single specified user (with email = a.agima@commodore.com)
[/wpdk_is_user_logged_in]
```

and finally...

```
[wpdk_is_user_logged_in ids='14,15']
This content is visibile for users with id 14 and 15
[/wpdk_is_user_logged_in]
```


### wpdk_gist

If you are a Githubber :) you’ll like also:

```
[wpdk_gist id="762771662"]

or

[wpdk_gist id="762771662" file="hello.php"]
```

### wpdk_geo

From release 1.7.0 you can make your content geo localization.
You can to display content based on geolocation information of the user who is viewing the page. The new shortcode `wpdk_geo` supports these attributes (all in case insesitive):

* city
  One or more city, eg: `city="Rome,paris"`

* region
  One or more region if supported, eg: `region="lazio,umbria"`

* country_code
  One or more standard country code, eg: `country_code="IT"`

* country
  One or more country name, eg: `country="italy,france"`

Some exmaple:

```
[wpdk_geo city="Rome"]
  Only for Rome
[/wpdk_geo]

[wpdk_geo city="rome"]
  Only for Rome
[/wpdk_geo]

[wpdk_geo city="rome,london"]
  Only for Rome and Landon
[/wpdk_geo]

[wpdk_geo region="lazio"]
  Only for region (Italy) Lazio
[/wpdk_geo]

[wpdk_geo country_code="IT"]
  Italian only
[/wpdk_geo]

[wpdk_geo country="italy"]
  Italian only
[/wpdk_geo]
```
```