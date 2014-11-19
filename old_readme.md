#LaravelXMLKit
Package for Laravel based on Eloquent to manage XML files with SimpleXMLElement and xpath.

##Usage
Install the package through Composer.

```js
{
    "require": {
        "laravel/framework": "4.2.*",
        "hugocabral/LaravelXMLKit": "dev-master" // or "hugocabral/LaravelXMLKit": "1.0.*"
    }
}
```


Edit 'app/config/app.php', and add a new item to the 'aliases' array:

```php
'LaravelXMLKit' => 'hugocabral\LaravelXMLKit\LaravelXMLKit'
```


Publish configuration file from package:

```bash
php artisan config:publish hugocabral/LaravelXMLKit
```

You may now edit these options at 'app/config/packages/hugcabral/LaravelXMLKit/config.php'. Or copy this file to 'app/config' folder with name 'LaravelXMLKit.php'.


Now, your XML models can simply extend 'LaravelXMLKit':

```php
<?php

class Breakfast extends LaravelXMLKit {

    /**
     * The file associated with the model
     *
     * @var string
     */
    protected $file = 'breakfast.xml';
   
    /**
     * Root element of the document
     *  
     * @var string
     */
    protected $root = 'breakfast';  
 
    /**
     * Child elements of the root
     * 
     * @var string 
     */
    protected $child = 'food';     
 
    /**
     * The primary key for the model
     *
     * @var string
     */
    protected $primaryKey = 'name';

}
```


See example of 'breakfast.xml' file on this link: 
https://github.com/hugocabral/LaravelXMLKit/blob/master/breakfast.xml


##Examples
```php
// Get all child nodes from XML root.
$foods = Breakfast::all();


// Count elements from selected childs $foods.
$foods->count();


// Get child from XML by $primaryKey or fail if not exists.
Breakfast::findOrFail('French Toast');


// Get child from XML with where condition.
$food = Breakfast::select()->where('name', '=', 'French Toast')->get();

// Update fields from selected child $food. 
$food->price = '3.25€';
$food->calories = 450;

// Save changes.
$food->save();


// Create new XML child.
$new = new Breakfast;

// Add data to child fields.
$new->name = 'French Toast';
$new->price = '4.50€';
$new->description = 'Thick slices made from our homemade sourdough bread';
$new->calories = 600;

// Save new child to XML file with tag attributes.
$new->save(array('id' => 26092014));
```

##Help
More help and reference soon...
