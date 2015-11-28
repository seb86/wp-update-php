# WP Update Php library
Library to be bundled with WordPress plugins to enforce users to upgrade their PHP versions _or_ switch to a decent host.

## Installation
We recommend installing the library using [Composer](https://getcomposer.org/), as follows.

```
composer require seb86/wp-update-php
```

Another option is to download the [class file](https://github.com/seb86/wp-update-php/blob/master/src/wp-update-php.php) manually.

## Usage
Usage of this library depends on how you start your plugin. The core `does_it_meet_required_php_version` method does all the checking for you and adds an admin notice in case the version requirement is not met.

For example, when you start your plugin by instantiating a new object, you should wrap a conditional check around it. 

_Example:_

```php
$updatePhp = new WP_Update_Php();

if ( $updatePhp->does_it_meet_required_php_version()) {
  // Instantiate new object here
}

// The version check has failed, a admin notice has been thrown
```

### The Defaults
Without passing through any plugin details or php requirement, the class library reverts to it's default settings.

* Plugin name: null
* Textdomain: null
* Minimum Version of Php: 5.3.0
* Recommended Version of Php: null

To change these settings, simply apply like so:

_Example:_

```php
$updatePhp = new WP_Update_Php(
	array(
		'name' => 'Auto Load Next Post',
		'textdomain' => 'auto-load-next-post'
	),
	array(
		'minimum_version' => '5.3.0',
		'recommended_version' => '5.4.7'
	)
);
```
All variables are in an array of their own.

When adding the name of the plugin, the notices no longer referr as "this plugin" but by the plugin name. It helps acknowledge which plugin the user is activating at the time.

Adding the textdomain allows you to include the strings in your POT file allowing the the notices to be translated.

If you need to specify the the minimum and recommeded version of the Php for your plugin to work, make sure you have the versions applied to the correct variable.

## Including the library file
Adding the library via Composer has preference. The Composer autoloader will automatically take care of preventing including two classes with the same name.

In case you want to include the file manually, please wrap the include or require call in a [`class_exists`](http://php.net/class_exists) conditional, like so:

```php
if ( ! class_exists('WP_Update_Php')) {
	require_once('wp-update-php/wp-update-php.php');
}
```

## License
(GPLv2 license or later)

WP Update PHP Library forked from [https://github.com/WPupdatePHP/wp-update-php](https://github.com/WPupdatePHP/wp-update-php) and modified.
Copyright (C) 2015  Coen Jacobs, Sébastien Dumont

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
