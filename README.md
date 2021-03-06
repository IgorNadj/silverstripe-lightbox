# Lightboxes

Provides an interface to create modal/popup boxes with customisable content within.

## Requirements

To get the lightbox working on your page, you'll need to include this javascript file.
```
Requirements::javascript('lightbox/javascript/lightbox.js');
```

We've provided some default styling for the lightbox, you can use that by including this css file.
```
Requirements::css('lightbox/css/lightbox.css');
```

## Extending more DataObjects
If you want to be able to use Lightbox on other DataObjects that are not extended from SiteTree, you can do that by following these steps:
Create a LightboxItemExtension, Item could be any DataObject class
```
class LightboxItemExtension extends DataExtension {
	private static $many_many = array(
		'Items' => 'Item',
	);
}
```

Extend both that Item class and the Lightbox class, we've done this using a config.yml file
```
---
Name: mysitelightboxextensions
---
Lightbox:
  extensions:
    - LightboxExtension
Item:
  extensions:
    - DataObjectLightboxExtension
```

DataObjectLightboxExtension contains a standard `onAfterWrite()` event that handling creating a link between the DataObject and Lightbox.

## Adding more Lightbox layouts/types

Create a new class which extends from the Lightbox class, for example this CustomLightbox class
```
<?php

class CustomLightbox extends Lightbox {

	public static $singular_name = 'Custom Lightbox';
	public static $plural_name = 'Custom Lightboxes';

	private static $db = array(
		'Content2' => 'HTMLText',
		'Button2Text' => 'Varchar(255)',
		'Button2Link' => 'Varchar(255)',
	);
}
```