gallery-metabox
===============

Proper gallery metabox for WordPress. Uses the new WP 3.5 media uploader. Instead of selecting the images one at a time, you can also select multiple images. Images can be sorted by dragging the thumbnails.

![gallery-metabox](http://www.daanvosdewael.com/files/gallery-metabox-preview.jpg)

Usage
-----

>This is not a plugin! You need to include this in your theme folder and further customize it to your needs. If you are not comfortable doing this, don't use it...

Include the `gallery.php` in your `functions.php`:

```php
require_once 'gallery-metabox/gallery.php';
```

Specify where you want the gallery metabox to show on line 17 in `gallery.php`. You can pass an array to have it show up on multiple post types, custom post types are also allowed:

```php
$types = array('post', 'page', 'custom-post-type');
```

In your template inside a loop, grab the IDs of all the images with the following:

```php
$images = get_post_meta($post->ID, 'vdw_gallery_id', true);
```

Then you can loop through the IDs and call `wp_get_attachment_link` or `wp_get_attachment_image` to display the images with or without a link respectively:

```php
foreach ($images as $image) {
  echo wp_get_attachment_link($image, 'large');
  // echo wp_get_attachment_image($image, 'large');
}
```


I forked this repo and could not get the above code to work for me to output the images. Everything else worked fine except the images were stored in a serialized array  which I needed to unserialize to get it to work properly. 

Below is how I accessed the data for the images in my particular situation. 

```php
//Get all meta data on the page
$custom_meta = get_post_custom($post->ID);

//access the array for the data you want (vdw_gallery_id) and unserialize it
$images = unserialize($custom_meta['vdw_gallery_id'][0]);

//loop through and echo out your new unserialized array
foreach ($images as $image) {
    echo wp_get_attachment_image($image, 'large');
}

```
