# Chivins Codeigniter Wordpress Like Shortcodes
 This is standalone wordpress like codeigniter shortcode library. With this library you can implement wordpress shortcode wizard into your codeigniter project in order to build snippets for your project


## Example Usage:

## Loading the class
You can auto load the shortcode helper by going to `application => config => autoload.php `

```php
# autoload.php

$autoload['helper'] = array('shortcode');
```

You can still load it with 
```php 
	
	$this->load->helper('shortcode');

```

Here's a pure code we want to parse shortcodes in it:

```php
print ($welcome = 'Welcome to my world! click [chivins]here[/chivins] to visit chivins homepage!');

# Welcome to my world! click [chivins]here[/chivins] to visit chivins homepage!
```

Now we want to add the shortcode `chivins` and use `do_shortcode` to make it listen for shortcodes:

```php
add_shortcode('chivins', function($atts, $content){
    return sprintf(
        '<a href="%s">%s</a>',
        $login_url = 'https://chivins.com',
        $content
    ); 
});

print ($welcome = do_shortcode('Welcome to my world! click [chivins]here[/chivins] to visit chivins homepage!'));

#Welcome to my world! click <a href="https://chivins.com">here</a> to visit chivins homepage!
```

## Shortcode with attributes:

You can also pass attributes to the shortcodes which you can use later in the shortcode callback. Here are couple example shortcodes with attributes:

`[link rel="nofollow" /]`
`[image src="pixel.gif" alt=image lazyload='true' /]`

Now if you debug the `$atts` in the shortcode callback, you'll find all of the shortcode attributes as an array:

```php
add_shortcode('image', function($atts, $content){
    print_r($atts);
});

echo do_shortcode('[image src="pixel.gif" alt=image lazyload=\'true\' /]');

# > ['src' => 'pixel.gif', 'alt' => 'image', 'lazyload' => 'true']
```
