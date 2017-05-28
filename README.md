# ReflectionClass

A basic reflection class for PHP. This class is designed to be a Common Class to be utilized as an aid for testing or getting access to private/protected/public/static access to functions/variables inside of PHP.

## Usage

To include the ReflectionClass in your composer file add the repo directory into your repositories section in the composer file and add the name of the module into the require section of the composer file.

```
"repositories": {
    ...
    { 
      "type": "vcs", 
      "url": "https://github.com/fufu70/ReflectionClass.git"
    }
    ...
}

...

"require": {
    ...
    "fufu70/reflectionclass": "dev-master",
    ...
}
```

The Reflection class has 3 Main functions:

* `Reflection::callMethod`
* `Reflection::getProperty`
* `Reflection::setProperty`

### `Reflection::callMethod`

The `callMethod` function uses the method name, class name, arguments, and object reference of the class name given. If the classs name is `null` then it will utilize the class name of the last class called.

```php
<?php
use Common\Reflection;

// call a function in the current class
$local_function_result = Reflection::callMethod('function_name', null, []);

// call a static function in the Curl class
$static_function_result = Reflection::callMethod(
    'post', 
    'Common\Curl', 
    [
        'http://example.com/endpoint'
        [
        'name' => 'value',
        'another_name' => 'another_value'
        ]
    ]
);

// call a function connected with an object
$imagick = new \Imagick(realpath('/path/to/file'));

Reflection::setProperty(
    'setImageOrientation', 
    'Imagick', 
    Imagick::ORIENTATION_LEFTBOTTOM, 
    $imagick
);
```

### `Reflection::getProperty`

The `getProperty` function uses the property name, class name, and object reference to get the property. Just like with the `callMethod` function, if the class name is empty it uses the last class called.

```php
<?php

// get the property value of the current class
$local_property_result = Reflection::getProperty('property_name');

// get the static property value of a class
$static_property_result = Reflection::getProperty('property_name', 'Class\Name');

// get the property value of a class objecty
$object = new stdClass();
$object->property_name = "property_value";
$object_property_result = Reflection::getProperty('property_name', 'stdClass', $object);
```

### `Reflection::setProperty`

The `setProperty` function uses the property name, class name, object reference, and new property value to set the property. Just like with the `getProperty` function, if the class name is empty it uses the last class called.

```php
<?php

// set the property value of the current class
$null = null;
Reflection::setProperty('property_name', null, $null, "new_property_value");

// set the static property value of a class
$null = null;
Reflection::setProperty('property_name', 'Class\Name', $null, $value);

// set the property value of a class objecty
$object = new stdClass();
$object->property_name = "property_value";
Reflection::setProperty('property_name', 'stdClass', $object, "new_property_value");
```