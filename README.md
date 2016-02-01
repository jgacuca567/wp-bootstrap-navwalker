wp-bootstrap-navwalker
======================

**A custom WordPress nav walker class to fully implement the Bootstrap 4.0 Alpha navigation style in a custom theme using the WordPress built in menu manager.**

Bootstrap 4
------------


NOTE
----
This is a utility class that is intended to format your WordPress theme menu with the correct syntax and classes to utilize the Bootstrap dropdown navigation, and does not include the required Bootstrap JS files. You will have to include them manually. 

Installation
------------
Place **wp_bootstrap_navwalker.php** in your WordPress theme folder `/wp-content/your-theme/`

Open your WordPress themes **functions.php** file  `/wp-content/your-theme/functions.php` and add the following code:

```php
// Register Custom Navigation Walker
require_once('wp_bootstrap_navwalker.php');
```

Usage
------------
Update your `wp_nav_menu()` function in `header.php` to use the new walker by adding a "walker" item to the wp_nav_menu array.

```php
 <?php
/**
 * Displays a navigation menu
 * @param array $args Arguments
 */
$args = array(
    'theme_location' => '',
    'menu' => '',
    'container' => 'div',
    'container_class' => 'menu-{menu-slug}-container',
    'container_id' => '',
    'menu_class' => 'menu',
    'menu_id' => '',
    'echo' => true,
    'fallback_cb' => 'wp_bootstrap_navwalker::fallback',
    'before' => '',
    'after' => '',
    'link_before' => '',
    'link_after' => '',
    'items_wrap' => '<ul id = "%1$s" class = "%2$s">%3$s</ul>',
    'depth' => 0,
    'walker' => new wp_bootstrap_navwalker(),
);

wp_nav_menu($args);
?>
```

Your menu will now be formatted with the correct syntax and classes to implement Bootstrap dropdown navigation. 

You will also want to declare your new menu in your `functions.php` file.

```php
register_nav_menus( array(
	'primary' => __( 'Primary Menu', 'THEMENAME' ),
) );
```

Typically the menu is wrapped with additional markup, here is an example of a ` navbar-fixed-top` menu that collapse for responsive navigation.

```php
<nav class="navbar navbar-light bg-faded">
  <a class="navbar-brand" href="#">Navbar</a>
  <?php
/**
 * Displays a navigation menu
 * @param array $args Arguments
 */
$args = array(
    'theme_location' => '',
    'menu' => '',
    'container' => 'div',
    'container_class' => 'menu-{menu-slug}-container',
    'container_id' => '',
    'menu_class' => 'menu',
    'menu_id' => '',
    'echo' => true,
    'fallback_cb' => 'wp_bootstrap_navwalker::fallback',
    'before' => '',
    'after' => '',
    'link_before' => '',
    'link_after' => '',
    'items_wrap' => '<ul id = "%1$s" class = "%2$s">%3$s</ul>',
    'depth' => 0,
    'walker' => new wp_bootstrap_navwalker(),
);

wp_nav_menu($args);
?>
  <ul class="nav navbar-nav">
    <li class="nav-item active">
      <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Features</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Pricing</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">About</a>
    </li>
  </ul>
  
</nav>
```

To change your menu style add Bootstrap nav class names to the `menu_class` declaration.

Review options in the Bootstrap docs for more information on nav classes
http://getbootstrap.com/components/#nav

Displaying the Menu 
-------------------
To display the menu you must associate your menu with your theme location. You can do this by selecting your theme location in the *Theme Locations* list wile editing a menu in the WordPress menu manager.

Extras
------------

![Extras](http://edwardmcintyre.com/pub/github/navwalker-3-menu.jpg)

This script included the ability to add Bootstrap dividers, dropdown headers, glyphicons and disables links to your menus through the WordPress menu UI. 

Dividers
------------
Simply add a Link menu item with a **URL** of `#` and a **Link Text** or **Title Attribute** of `divider` (case-insensitive so ‘divider’ or ‘Divider’ will both work ) and the class will do the rest.

![Divider Example](http://edwardmcintyre.com/pub/github/navwalker-divider.jpg)

Glyphicons
------------
To add an Icon to your link simple place the Glyphicon class name in the links **Title Attribute** field and the class will do the rest. IE `glyphicon-bullhorn`

![Header Example](http://edwardmcintyre.com/pub/github/navwalker-3-glyphicons.jpg)

Dropdown Headers
------------
Adding a dropdown header is very similar, add a new link with a **URL** of `#` and a **Title Attribute** of `dropdown-header` (it matches the Bootstrap CSS class so it's easy to remember).  set the **Navigation Label** to your header text and the class will do the rest.

![Header Example](http://edwardmcintyre.com/pub/github/navwalker-3-header.jpg)

Disabled Links
------------
To set a disabled link simply set the **Title Attribute** to `disabled` and the class will do the rest. 

![Header Example](http://edwardmcintyre.com/pub/github/navwalker-3-disabled.jpg)

Changelog
------------
**2.0.4**
+ Updated fallback function to accept args array from wp_nav_menu

**2.0.3**
+ Included a fallback function that adds a link to the WordPress menu manager if no menu has been assigned to the theme location.

**2.0.2**
+ Small tweak to ensure carets are only displayed on top level dropdowns.

**2.0.1**
+ Added missing `active` class to active menu items.

**2.0**
+ Class was completly re-written using the latest Wordpress 3.6 walker class.
+ Now full supports Bootstrap 3.0+
+ Tested with wp_debug & the Theme Check plugin.

[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/twittem/wp-bootstrap-navwalker/trend.png)](https://bitdeli.com/free "Bitdeli Badge")
