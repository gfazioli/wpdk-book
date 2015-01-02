# WPDK Features

### WPDK is completely object oriented

Any element of WPDK has been developed following **object oriented paradigm**, according to the current *PHP* model.

This choice ensures an easier maintenance of source code, and allows you to easily extend the basic features of this framework to create solid and stable custom results. For example, see the internal [Class Hierarchy](http://wpxtreme.github.io/wpdk/documentation/html/hierarchy.html) page: you can see that all WPDK elements are always encapsulated in a specific dedicated object. So you can instantiate the object you need, or extend it to create a custom behaviour: object oriented paradigm helps you to do that in a cleaner and solid way.

### WPDK follows MVC pattern


In any context this approach is possible and reasonable, WPDK follows **MVC pattern**, described and introduced <a href="http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller">in this document</a>.

As this document remind us, this developing pattern, well known to *Objective-C* developers, ensures clarity and solidity of source code, because *phisically separates the representation of information from the user's interaction with it*.

For example, WPDK implements a generic `WPDKViewController` object, that handles display of data in the large area in the middle of *WordPress Administration Screen*, formerly called **the work area**. A standard content in this area is like this:

* header with icon and title - optional button add
* one or more views implemented through `WPDKView` object instances.

Two specializations of this basic object are `WPDKAboutViewController`, that handles display of credits/info about a plugin, and `WPDKjQueryTabsViewController`, that handles display of jQuery tabs.

Following *MVC* approach, you can easily build complex and powerful views, separating from them the model that phisically contains data to be shown. Maybe you can have, at the end, more source code that you really need. But you gain clarity, solidity, ease in readability and maintenance of your source code.

This approach is not embedded at all in WordPress source code. WPDK aims to fill this gap.

### Full Doxygen compatibility of WPDK documentation

All WPDK documentation is embedded in source code, and is written in *PHPDoc* format compatible to <a href="http://www.stack.nl/~dimitri/doxygen/index.html">Doxygen</a> syntax.

The use of this standard format means that using your preferred IDE ( *PHPStorm, Netbeans, Eclipse, Aptana, ecc.* ), you will always have help inline during develop with WPDK. This help is constantly enriched from WPDK developers with examples, better explanation of methods and properties, better description of classes, ecc. whenever this framework is updated. No need to search on the net: all documentation about stable WPDK objects is always available, and aligned to a well known and popular format.

### WPDK has all graphic controls you need


In your WordPress creations, one of the most important aspect is the user interface.

Instead of creating by yourself everytime a brand new user interface, with forms, data saving and restoring, HTML code, CSS, and so on, you can use the numerous, ever growing, and powerful **WPDK graphic controls**, immediately available for your develop.

With a simple syntax, you can use and customize input text, buttons, checkbox, radio buttons, single and multiple combo, textarea, file selector, simple label, swipe buttons. But that's not all. You can also insert *TwitterBootstrap Alert* in your own code, following a specific operation that your code executes, and leaving to WPDK the internal handling.

This is a key point. Because using this approach, *you can create a standard and pleasant user interface for all your WordPress creations*, leaving to WPDK all the internal stuff. You don't have to worry about how to put a swipe button into your WordPress administrative page: WPDK can make this task for you in a while.

The entire [wpXtreme ecosystem](https://wpxtre.me/) uses this WPDK feature to standardize user interface, and to create efficient and powerful results in all its WordPress creations.

Go to the [[WPDK How-Tos]] section, see how easy is creating and using a graphic control in your own code, get the source code that use this pattern, and customize it to your own needs.

### WPDK useful classes and helpers

In addition to specific targeted objects, WPDK makes available a set of objects that embed some specific features that can enhance and simplify your WordPress develop. These evergrowing available objects are called *helpers*, and include:

* array manipulation - `WPDKArray`
* crypting data - `WPDKCrypt`
* colors - `WPDKColors`
* local filesystem navigation - `WPDKFilesystem`
* math functions - `WPDKMath`
* basic WordPress screen content manipulation - `WPDKScreenHelp`

### WPDK embeds object autoloading

WPDK natively implements <a href="http://www.php.net/manual/en/language.oop5.autoload.php">PHP autoloading classes</a> feature. This is a key point, in WPDK technology, that deserves additional information.

As you have seen, WPDK is totally object oriented: that is, all WPDK elements are always objects, defined as *PHP classes*. Thanks to *PHP autoloading feature*, whenever a client sends an *HTTP request* that involves one or more WPDK objects, **WPDK loads and execute the sole source code involved in the HTTP transaction**.

Consider this: in any *HTTP transaction*, WordPress loads always itself entirely, even if the transaction does not need the 80-90% of the source code loaded and executed. WPDK does not behave in this way: if your *HTTP request* is directed to a web page that uses, for example, `WPDKMenu` and `WPDKArray` objects, *only those two WPDK objects are loaded and parsed*. The entire remaining WPDK source code is not considered at all.

This is made possible through the embedded *WPDK autoloading technology*, based on *PHP autoloading classes* above.

But that's not all. If you develop your WordPress creation following some simple rules ( that include a full object oriented approach to your develop ), the *WPDK autoloading technology* becomes available also to your creation, even it is totally external to WPDK. This is another key point, that can dramatically increasing the speed of loading and execution of your code, *up to 50% faster than normal file inclusion*.

[Click here](https://github.com/wpXtreme/wpdk/wiki/WPDK-How-tos#sample-5-of-wordpress-plugin-using-wpdk) to see how easy is developing your WordPress creation using WPDK for automatically gaining *WPDK autoloading technology* in your own code.
