# wpdk_geo

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