# NSY SYSTEM GUIDE PART 1
NSY is a simple PHP Framework that works well on MVC or HMVC mode.

Site example :
<a href="https://nsy.kazuyamarino.com/" target="_blank">https://nsy.kazuyamarino.com/</a>

## Usefull Method

### Public directory path
Returns your site full path `public` directory, as specified in your config file.

```
echo public_path();

// for example
usr/share/../html/nsy/public/
```

### Images directory uri
Return img directory location on the `public` directory

```
echo img_url();

// for Example
// http://example.com/public/img
```

### Javascript directory uri
Return js directory location on the `public` directory

```
echo js_url();

// for Example
// http://example.com/public/js
```

### CSS directory uri
Return css directory location on the `public` directory

```
echo css_url();

// for Example
// http://example.com/public/css
```

### Get Version
Get `version` parameter value from config/Site.php.

```
echo get_version();

// 3.0.0
```

### Get Codename
Get `codename` parameter value from config/Site.php.

```
echo get_codename();

// Tifa
```

### Get Language Code
Get `locale` parameter value from config/App.php.

```
echo get_lang_code();

// en
```

### Open Graph Prefix
Get `prefix_attr` parameter value from config/App.php.

```
echo get_og_prefix();
```

### Get Site Title
Get `sitetitle` parameter value from config/Site.php.

```
echo get_title();
```

### Get Site Description
Get `sitedesc` parameter value from config/Site.php.

```
echo get_desc();
```

### Get Site Keywords
Get `sitekeywords` parameter value from config/Site.php.

```
echo get_keywords();
```

### Get Site Author
Get `siteauthor` parameter value from config/Site.php.

```
echo get_author();
```

### Get Session Prefix
Get `session_prefix` parameter value from config/App.php.

```
echo get_session_prefix();
```

### Get Site Email
Get `siteemail` parameter value from config/Site.php.

```
echo get_site_email();
```

---

### Base URL
Returns your site base URL, as specified in your config file.

```
echo base_url();

// http://example.com/
```

You can supply segments as a string. Here is a string example:

```
echo base_url("hmvc/action");
```

The above example would return something like: http://example.com/hmvc/action

You can supply a string to a file, such as an image or stylesheet. For example:

```
echo base_url("images/edit.png");
```

This would give you something like: http://example.com/images/edit.png

Redirect method is used to send a raw HTTP header. Here is the example:

```
redirect('hmvc/success');
```

The above example would return redirect url to: http://example.com/hmvc/success

```
redirect_back();
```

The above example would return redirect to previous page.

<hr>

### Array Flatten
PHP array_flatten() function. Convert a multi-dimensional array into a single-dimensional array :

```
array_flatten($items);

// $id = array_flatten([1, [2, [3], 4], 5]);
// print_r($id);
//
// Will return : [1, 2, 3, 4, 5]
```

### Fetch to JSON
If you want to display data values ​​in json form, you can do this method :

```
fetch_json($data, $http_response_code);

// $id = [1,2,3,4,5];
// echo fetch_json(["data" => $id], 200);
//
// Will return :
// {
//   "data": [
//    	1,
//    	2,
//    	3,
//    	4,
//    	5
//   ]
// }
```

<hr>

### Getting config value
If you want to take values ​​in the config file on the `system/config`, this is the way :

* Get value from `App.php` :

```
config_app('value_name');
// config_app('app_env');
```

* Get value from `Database.php` :

```
config_db('connection', 'value_name');
// config_db('mysql', 'DB_HOST');
```

* Get value from `Site.php` :

```
config_site('value_name');
// config_site('sitetitle');
```

<hr>

### Security helper
* For filtering input value :

```
secure_input('attr_name')
```

* Get CSRF Token on form :

```
echo form_csrf_token();
```

* Get CSRF Token/Only Token :

```
echo csrf_token();
```

* Filtering variable from XSS :

```
xss_filter('value');
```

* Allow http :

```
allow_http();
```

* Disallow http :

```
disallow_http();
```

* Remove get parameter :

```
remove_get_parameters('url');
```

---

### Get URI Segment
To help in retrieving data in URIs

```
get_uri_segment(segment number)
```

Example :

```
http://localhost/nsy/hmvc

echo get_uri_segment(1);
// Output is nsy

echo get_uri_segment(2);
// Output is hmvc
```

### Generate Random Number
To generate a sequence of random numbers that correspond to the desired number or prefix.

```
generate_num(prefix, random_number_length, total_number/char_length);
```

Example :

```
echo generate_num();
// Default output NSY-617807

echo generate_num("VYLMA-", 4, 10);
// Output VYLMA-6906
```

---

### PHP SESSION

Use this namespace in the controller :

```
use System\Libraries\Session;
```

### Usage

Example of use for this library:

#### - Set prefix for sessions:

```php
Session::set_prefix('_prefix');
```

#### - Get sessions prefix:

```php
Session::get_prefix();
```

#### - Start session:

```php
Session::init();
```

#### - Start session by setting the session duration:

```php
Session::init(3600);
```

#### - Add value to a session:

```php
Session::set('name', 'Joseph');
```

#### - Add multiple value to sessions:

```php
$data = [
    'name'     => 'Joseph',
    'age'      => '28',
    'business' => ['name' => 'Company'],
];

Session::set($data);
```

#### - Extract session item, delete session item and finally return the item:

```php
Session::pull('age');
```

#### - Get item from session:

```php
Session::get('name');
```

#### - Get item from session entering two indexes:

```php
Session::get('business', 'name');
```

#### - Return the session array:

```php
Session::get();
```

#### - Get session id:

```php
Session::id();
```

#### - Regenerate session_id:

```php
Session::regenerate();
```

#### - Destroys one key session:

```php
Session::destroy('name');
```

#### - Destroys sessions by prefix:

```php
Session::destroy('ses_', true);
```

#### - Destroys all sessions:

```php
Session::destroy();
```

---

### Cookie Library

Use this namespace in the controller :

```
use System\Libraries\Cookie;
```

PHP library for handling cookies, NSY has supported the use of Cookie library class in the controller (mvc or hmvc).<br/>

### Usage

Example of use for this library:

#### - Set cookie:

```php
Cookie::set('cookie_name', 'value', 365);
```

#### - Get cookie:

```php
Cookie::get('cookie_name');
```

#### - Get all cookies:

```php
Cookie::get();
```

#### - Pull cookie:

```php
Cookie::pull('cookie_name');
```

#### - Destroy one cookie:

```php
Cookie::destroy('cookie_name');
```

#### - Destroy all cookies:

```php
Cookie::destroy();
```

#### - Set cookie prefix:

```php
Cookie::set_prefix('prefix_');
```

#### - Get cookie prefix:

```php
Cookie::get_prefix();
```

---

### Simple Ternary
Ternary operator logic is the process of using "`(condition) ? (true return value) : (false return value)`" statements to shorten your if/else structures.

```
ternary(condition, return true, return false)
```

Example :

```
/* most basic usage */
$var = 5;
$var_is_greater_than_two = ternary($var > 2, true, false);
// output returns true
```

---

### Specify an empty variable or not
In NSY, there is a function to make it easy for users to see whether a value is empty or not in a variable. i.e. only with 2 methods `not_filled()` and `is_filled()`.

`not_filled()`, s to determine a variable that has no value. Example :

```
$var = null;
not_filled($var); // output return true.
```

`is_filled()`, is to determine a variable has a value. Example :

```
$var = 5;
is_filled($var); // output return true.
```

Reference of the method :

```
$random = "";

$var1 = "";
$var2 = " ";
$var3 = false;
$var4 = true;
$var5 = array();
$var6 = null;
$var7 = "0";
$var8 = 0;
$var9 = 0.0;
$var10 = $random;
```

`not_filled()` :

```
$var1 = no value
$var2 = valued
$var3 = no value
$var4 = valued
$var5 = no value
$var6 = no value
$var7 = no value
$var8 = no value
$var9 = no value
$var10 = no value
```

`is_filled()` :

```
$var1 = no value
$var2 = valued
$var3 = no value
$var4 = valued
$var5 = no value
$var6 = no value
$var7 = no value
$var8 = no value
$var9 = no value
$var10 = no value
```

---

### Get User Agent
This is how to get user agent data with ease.

```
get_ua()
```

Example :

```
$d = get_ua();
print_r($d);

// output
Array
(
    [userAgent] => Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Ubuntu Chromium/77.0.3865.90 Chrome/77.0.3865.90 Safari/537.36
    [name] => Google Chrome
    [version] => 77.0.3865.90
    [platform] => Linux
    [pattern] => #(?Version|Chrome|other)[/ ]+(?[0-9.|a-zA-Z.]*)#
)
```

---

### Aurora File Export
Aurora is a library created to export data into several file formats supported by aurora such as txt, xls, ods, & etc.

```
aurora(file_extension, filename, separator, header, data, string_delimiter);
```

Variable explanation :
1. `file_extension` is a supported file extension by aurora. `(txt, csv, xls, xlsx, & ods)`.
2. `filename` is a filename defined by user.
3. `separator` is a delimiter of each data or table column `(tab, comma, semicolon, space, pipe, & dot)`.
4. `header` is the top or title of each column.
5. `data` is the contents of the table data or record.
6. `string_delimiter` is quote each string `("double" for double quote, & 'single' for singlequote)`.


Example :

```
// header data array structure must be like this
$header = [ 'Col1', 'Col2', 'Col3' ];

// columns data array structure must be like this
$data = Array
(
    [0] => Array
        (
            [name] => Vikry Yuansah
            [0] => Vikry Yuansah
            [user_name] => vikry
            [1] => vikry
            [user_code] => 1
            [2] => 1
        )

);

aurora('txt', 'nsy_aurora', 'pipe', $header, $data, 'single');

// Will generate nsy_aurora.txt, See output file at `public` folder.

// This is how it looks inside nsy_aurora.txt
'Col1'|'Col2'|'Col3'
'Vikry Yuansah'|'vikry'|'1'
```

---

# NSY FTP Client Library

NSY supports a flexible FTP and SSL-FTP client for PHP. This library provides helpers easy to use to manage the remote files. [nicolab/php-ftp-client](https://github.com/Nicolab/php-ftp-client).

You only need to instantiate the class in the construct method `__contruct`.
[See Instantiate Model class in the controller](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE.md#instantiate-model-class-in-the-controller).

#### Login to FTP

```
$this->ftp = new \FtpClient\FtpClient();
$this->ftp->connect('website.com');
$this->ftp->login('admin@website.com', 'password');

// Turns passive mode on (true) or off (false)
$this->ftp->pasv(true);
```

#### Returns the last modified time of the given file

```
$this->ftp->modifiedTime('path/of/file');
```

#### Changes to the parent directory

```
$this->ftp->up();
```

#### Returns a list of files in the given directory

```
$this->ftp->nlist('path/of/directory', true);
```

#### Removes a directory

```
$this->ftp->rmdir('path/of/directory/to/remove');
```

#### Removes a directory (recursive)

```
$this->ftp->rmdir('path/of/directory/to/remove', true);
```

#### Creates a directory

```
$this->ftp->mkdir('path/of/directory/to/create');
```

#### Creates a directory (recursive), creates automaticaly the sub directory if not exist

```
$this->ftp->mkdir('path/of/directory/to/create', true);
```

#### Check if a directory exist

```
$this->ftp->isDir('path/of/directory');
```

#### Check if a directory is empty

```
$this->ftp->isEmpty('path/of/directory');
```

#### Scan a directory and returns the details of each item

```
$this->ftp->scanDir('path/of/directory');
```

#### Returns the total size of the given directory in bytes

```
$this->ftp->dirSize('path/of/directory');
```

### Count method
* count in the current directory

```
$total = $this->ftp->count();
```

* count in a given directory

```
$total = $this->ftp->count('/path/of/directory');
```

* count only the "files" in the current directory

```
$total_file = $this->ftp->count('.', 'file');
```

* count only the "files" in a given directory

```
$total_file = $this->ftp->count('/path/of/directory', 'file');
```

* count only the "directories" in a given directory

```
$total_dir = $this->ftp->count('/path/of/directory', 'directory');
```

* count only the "symbolic links" in a given directory

```
$total_link = $this->ftp->count('/path/of/directory', 'link');
```

#### Downloads a file from the FTP server into a string

```
$this->ftp->getContent('path/of/file');
```

### Upload method
* Uploads a file to the server from a string

```
$this->ftp->putFromString('path/of/file', 'string');
```

* Uploads a file to the server

```
$this->ftp->putFromPath('path/of/file');
```

* upload with the BINARY mode

```
$this->ftp->putAll('source_directory', 'target_directory');
```

* Is equal to

```
$this->ftp->putAll('source_directory', 'target_directory', FTP_BINARY);
```

* or upload with the ASCII mode

```
$this->ftp->putAll('source_directory', 'target_directory', FTP_ASCII);
```

#### Downloads all files from remote FTP directory

```
$this->ftp->getAll('source_directory', 'target_directory', FTP_BINARY);
```

#### Returns a detailed list of files in the given directory

```
$this->ftp->rawlist('path/of/directory');
```

#### Parse raw list

```
$d = $this->ftp->rawlist('path/of/directory');
$e = $this->ftp->parseRawList($d);
```

#### Convert raw info (drwx---r-x ...) to type (file, directory, link, unknown)

```
$this->ftp->rawToType('drwx---r-x');
```

#### Set permissions on a file via FTP

```
$this->ftp->chmod('0775', 'path/of/file');
```

---

# ImageResize Library

Use this namespace in the controller :

```
use System\Libraries\ImageResize;
```

### Resize

To scale an image, in this case to half it's size (scaling is percentage based):

```php
$image = new ImageResize('image.jpg');
$image->scale(50);
$image->save('image2.jpg');
```

To resize an image according to one dimension (keeping aspect ratio):

```php
$image = new ImageResize('image.jpg');
$image->resize_to_height(500);
$image->save('image2.jpg');

$image = new ImageResize('image.jpg');
$image->resize_to_width(300);
$image->save('image2.jpg');
```

To resize an image according to a given measure regardingless its orientation (keeping aspect ratio):

```php
$image = new ImageResize('image.jpg');
$image->resize_to_long_side(500);
$image->save('image2.jpg');

$image = new ImageResize('image.jpg');
$image->resize_to_short_side(300);
$image->save('image2.jpg');
```

To resize an image to best fit a given set of dimensions (keeping aspet ratio):

```php
$image = new ImageResize('image.jpg');
$image->resize_to_best_fit(500, 300);
$image->save('image2.jpg');
```

All resize functions have ```$allow_enlarge``` option which is set to false by default.
You can enable by passing ```true``` to any resize function:

```php
$image = new ImageResize('image.jpg');
$image->resize(500, 300, $allow_enlarge = True);
$image->save('image2.jpg');
```

If you are happy to handle aspect ratios yourself, you can resize directly:

```php
$image = new ImageResize('image.jpg');
$image->resize(800, 600);
$image->save('image2.jpg');
```

This will cause your image to skew if you do not use the same width/height ratio as the source image.

### Crop

To to crop an image:

```php
$image = new ImageResize('image.jpg');
$image->crop(200, 200);
$image->save('image2.jpg');
```

This will scale the image to as close as it can to the passed dimensions, and then crop and center the rest.

In the case of the example above, an image of 400px &times; 600px will be resized down to 200px &times; 300px, and then 50px will be taken off the top and bottom, leaving you with 200px &times; 200px.

Crop modes:

Few crop mode options are available in order for you to choose how you want to handle the eventual exceeding width or height after resizing down your image.
The default crop mode used is the `CROPCENTER`.
As a result those pieces of code are equivalent:

```php
$image = new ImageResize('image.jpg');
$image->crop(200, 200);
$image->save('image2.jpg');
```

```php
$image = new ImageResize('image.jpg');
$image->crop(200, 200, true, ImageResize::CROPCENTER);
$image->save('image2.jpg');
```

In the case you have an image of 400px &times; 600px and you want to crop it to 200px &times; 200px the image will be resized down to 200px &times; 300px, then you can indicate how you want to handle those 100px exceeding passing the value of the crop mode you want to use.

For instance passing the crop mode `CROPTOP` will result as 100px taken off the bottom leaving you with 200px &times; 200px.


```php
$image = new ImageResize('image.jpg');
$image->crop(200, 200, true, ImageResize::CROPTOP);
$image->save('image2.jpg');
```

On the contrary passing the crop mode `CROPBOTTOM` will result as 100px taken off the top leaving you with 200px &times; 200px.

```php
$image = new ImageResize('image.jpg');
$image->crop(200, 200, true, ImageResize::CROPBOTTOM);
$image->save('image2.jpg');
```

Freecrop:

There is also a way to define custom crop position.
You can define $x and $y in ```freecrop``` method:

```php
$image = new ImageResize('image.jpg');
$image->freecrop(200, 200, $x =  20, $y = 20);
$image->save('image2.jpg');
```

### Loading and saving images from string

To load an image from a string:

```php
$image = ImageResize::create_from_string(base64_decode('R0lGODlhAQABAIAAAAQCBP///yH5BAEAAAEALAAAAAABAAEAAAICRAEAOw=='));
$image->scale(50);
$image->save('image.jpg');
```

You can also return the result as a string:

```php
$image = ImageResize::create_from_string(base64_decode('R0lGODlhAQABAIAAAAQCBP///yH5BAEAAAEALAAAAAABAAEAAAICRAEAOw=='));
$image->scale(50);
echo $image->();
```

Magic `__toString()` is also supported:

```php
$image = ImageResize::create_from_string(base64_decode('R0lGODlhAQABAIAAAAQCBP///yH5BAEAAAEALAAAAAABAAEAAAICRAEAOw=='));
$image->resize(10, 10);
echo (string)$image;
```

### Displaying

As seen above, you can call `$image->save('image.jpg');`

To render the image directly into the browser, you can call `$image->output()`;

### Image Types

When saving to disk or outputting into the browser, the script assumes the same output type as input.

If you would like to save/output in a different image type, you need to pass a (supported) PHP [`IMAGETYPE_`* constant](http://www.php.net/manual/en/image.constants.php):

- `IMAGETYPE_GIF`
- `IMAGETYPE_JPEG`
- `IMAGETYPE_PNG`

This allows you to save in a different type to the source:

```php
$image = new ImageResize('image.jpg');
$image->resize(800, 600);
$image->save('image.png', IMAGETYPE_PNG);
```

Quality
-------

The properties `$quality_jpg` and `$quality_png` are available for you to configure:

```php
$image = new ImageResize('image.jpg');
$image->quality_jpg = 100;
$image->resize(800, 600);
$image->save('image2.jpg');
```

By default they are set to 85 and 6 respectively. See the manual entries for [`imagejpeg()`](http://www.php.net/manual/en/function.imagejpeg.php) and [`imagepng()`](http://www.php.net/manual/en/function.imagepng.php) for more info.

You can also pass the quality directly to the `save()`, `output()` and `()` methods:

```php
$image = new ImageResize('image.jpg');
$image->crop(200, 200);
$image->save('image2.jpg', null, 100);

$image = new ImageResize('image.jpg');
$image->resize_to_width(300);
$image->output(IMAGETYPE_PNG, 4);

$image = new ImageResize('image.jpg');
$image->scale(50);
$result = $image->get_image_as_string(IMAGETYPE_PNG, 4);
```

We're passing `null` for the image type in the example above to skip over it and provide the quality. In this case, the image type is assumed to be the same as the input.

### Interlacing

By default, [image interlacing](http://php.net/manual/en/function.imageinterlace.php) is turned on. It can be disabled by setting `$interlace` to `0`:

```php
$image = new ImageResize('image.jpg');
$image->scale(50);
$image->interlace = 0;
$image->save('image2.jpg');
```

### Chaining

When performing operations, the original image is retained, so that you can chain operations without excessive destruction.

This is useful for creating multiple sizes:

```php
$image = new ImageResize('image.jpg');
$image
    ->scale(50)
    ->save('image2.jpg')

    ->resize_to_width(300)
    ->save('image3.jpg')

    ->crop(100, 100)
    ->save('image4.jpg')
;
```

### Exceptions

ImageResize throws ImageResizeException for it's own for errors. You can catch that or catch the general \Exception which it's extending.

It is not to be expected, but should anything go horribly wrong mid way then notice or warning Errors could be shown from the PHP GD and Image Functions (http://php.net/manual/en/ref.image.php)

```php
try{
    $image = new ImageResize(null);
    echo "This line will not be printed";
} catch (ImageResizeException $e) {
    echo "Something went wrong" . $e->getMessage();
}
```

---

# Carbon Library

Use this namespace in the controller :

```
use Carbon\Carbon;
```
Carbon DateTime, [Carbon Documentation](https://carbon.nesbot.com/docs/)

---

# String Method

### - Check if the string starts with a certain value:

```php
str_starts_with($search, $string);
```

```php
str_starts_with("Hello", "Hello world");
```

**# Return** (boolean)

### - Check if the string ends with a certain value:

```php
str_ends_with($search, $string);
```

```php
str_ends_with("world", "Hello World");
```

**# Return** (boolean)

---

# LanguageCode Method

### - Get all language codes as array:

```php
parse_language();
```

```php
print_r( parse_language() );
```

**# Return** (array) → language codes and language names

### - Get language name from language code:

```php
get_language_name($languageCode);
```

```php
get_language_name('id');
```

**# Return** (tring|false) → country name

### - Get language code from language name:

```php
get_language_code($languageName);
```

```php
get_language_code('Indonesian');
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $languageName | Language name, e.g. 'Spanish'. | string | Yes | |

**# Return** (tring|false) → language code

---

# LoadTime Method

### - Set initial time:

```php
load_time();
```

**# Return** (float) → microtime

### - Set end time:

```php
end_time();
```

**# Return** (float) → seconds

### - Check if the timer has been started:

```php
is_active_time();
```

**# Return** (boolean)

## Usage

Example of use for this library:

```php
<?php
load_time();

for ($i=0; $i < 100000; $i++) {
    // print_r($i . ' ');
}

print_r('Script executed in: ' . end_time() . ' seconds.');

/* Script executed in: 0.0012 seconds. */
```

---

# Json Method

## Usage

Example of use for this library:

### - Creating JSON file from array:

```php

$array = [
	'name'  => 'Josantonius',
    'email' => 'info@josantonius.com',
    'url'   => 'https://github.com/josantonius/PHP-Json'
];

$pathfile = public_path('file.json');

json_array_to_file($array, $pathfile);

```

### - Save to array the JSON file content:

```php
$pathfile = public_path('file.json');

$array = json_file_to_array($pathfile);

```

### - Check for errors:

```php
$lastError = json_last_error();

if (!is_null($lastError)) {
    var_dump($lastError);
}
```

### - Get collection of JSON errors:

```php
$jsonLastErrorCollection = json_collection_error();
```

---

# Curl Library

Use this namespace in the controller :

```
use System\Libraries\Curl;
```

## Usage

Example of use for this library:

### - Send GET request and obtain response as array:

```php
Curl::request('https://graph.facebook.com/zuck');
```

### - Send GET request and obtain response as object:

```php
Curl::request('https://graph.facebook.com/zuck', false, 'object');
```

### - Send GET request with params and obtain response as array:

```php
$data = [
    'timeout' => 10,
    'referer' => 'http://site.com',
];

Curl::request('https://graph.facebook.com/zuck', $data);
```

### - Send GET request with params and obtain response as object:

```php
$data = [
    'timeout' => 10,
    'referer' => 'http://site.com',
];

Curl::request('https://graph.facebook.com/zuck', $data, 'object');
```

### - Send POST request and obtain response as array:

```php
$data = [
    'type'    => 'post',
    'data'    => array('user' => '123456', 'password' => 'xxxxx'),
    'timeout' => 10,
    'referer' => 'http://' . $_SERVER['HTTP_HOST'],
    'headers' => [
        'Content-Type:application/json',
        'Authorization:0kdm3hzmb4h3cf',
    ],
];

Curl::request('https://graph.facebook.com/zuck', $data);
```

### - Send POST request and obtain response as object:

```php
$data = [
    'type'    => 'post',
    'data'    => array('user' => '123456', 'password' => 'xxxxx'),
    'timeout' => 10,
    'referer' => 'http://' . $_SERVER['HTTP_HOST'],
    'headers' => [
        'Content-Type:application/json',
        'Authorization:0kdm3hzmb4h3cf',
    ],
];

Curl::request('https://graph.facebook.com/zuck', $data, 'object');
```

### - Send PUT request and obtain response as array:

```php
$data = [
    'type'    => 'put',
    'data'    => array('email' => 'new@email.com'),
    'timeout' => 30,
    'referer' => 'http://' . $_SERVER['HTTP_HOST'],
    'headers' => [
        'Content-Type:application/json',
        'Authorization:0kdm3hzmb4h3cf',
    ],
];

Curl::request('https://graph.facebook.com/zuck', $data);
```

### - Send PUT request and obtain response as object:

```php
$data = [
    'type'    => 'put',
    'data'    => array('email' => 'new@email.com'),
    'timeout' => 30,
    'referer' => 'http://' . $_SERVER['HTTP_HOST'],
    'headers' => [
        'Content-Type:application/json',
        'Authorization:0kdm3hzmb4h3cf',
    ],
];

Curl::request('https://graph.facebook.com/zuck', $data, 'object');
```

### - Send DELETE request and obtain response as array:

```php
$data = [

    'type'    => 'delete',
    'data'    => ['userId' => 10],
    'timeout' => 30,
    'referer' => 'http://' . $_SERVER['HTTP_HOST'],
    'headers' => [
        'Content-Type:application/json',
        'Authorization:0kdm3hzmb4h3cf',
    ],
];

Curl::request('https://graph.facebook.com/zuck', $data);
```

### - Send DELETE request and obtain response as object:

```php
$data = [
    'type'    => 'delete',
    'data'    => ['userId' => 10],
    'timeout' => 30,
    'referer' => 'http://' . $_SERVER['HTTP_HOST'],
    'headers' => [
        'Content-Type:application/json',
        'Authorization:0kdm3hzmb4h3cf',
    ],
];

Curl::request('https://graph.facebook.com/zuck', $data, 'object');
```

---

# File Library

Use this namespace in the controller :

```
use System\Libraries\File;
```

## Usage

Example of use for this library:

### - Check if a local file exists:

```php
<?php
File::exists('path/to/file.php');
```

### - Check if a external file exists:

```php
<?php
File::exists('https://raw.githubusercontent.com/Josantonius/PHP-File/master/composer.json');
```

### - Delete a local file:

```php
<?php
File::delete(public_path('file.txt'));
```

### - Create directory:

```php
<?php
File::create_dir(public_path('/test/'));
```

### - Delete empty directory:

```php
<?php
File::delete_empty_dir(public_path('/test/'));
```

### - Delete directory recursively:

```php
<?php
File::delete_dir_recursively(public_path('/test/'));
```

### - Copy directory recursively:

```php
<?php
File::copy_dir_recursively(public_path('/test/'), public_path('/copy/'));
```

### - Get file paths from directory:

```php
<?php
File::get_files_from_dir(__DIR__);
```

### - Writes data to the file specified in the path.

```php
<?php
File::write_file($path, $data, $mode = 'wb');
```

### - Get Filenames

```php
<?php
File::get_filenames($source_dir, $include_path = false, $_recursion = false);
```

### - Get Directory File Information

```php
<?php
File::get_dir_file_info($source_dir, $top_level_only = true, $_recursion = false);
```

### - Get File Info

```php
<?php
File::get_file_info($file, $returned_values = array('name', 'server_path', 'size', 'date'));
```

### - Get Mime by Extension

```php
<?php
File::get_mime_by_extension($filename);
```

### - Returns the MIME types array from config/Mimes.php

```php
<?php
File::get_mimes();
```

### - Generates headers that force a download to happen

```php
<?php
File::force_download($filename = '', $data = '', $set_mime = false);
```

---

# IP Method

## Usage

Example of use for this library:

### - Get user's IP:

```php
get_ip();
```

### - Validate IP:

```php
$ip = get_ip();

validate_ip($ip);
```

---

# Validate Library

Use this namespace in the controller :

```
use System\Libraries\Validate;
```

## Usage

Example of use for this library:

### - ARRAY:

#### - When an array is passed:

```php
var_dump(Validate::as_array(['foo', 'bar'])); // ['foo', 'bar']
```

#### - When an JSON array is passed:

```php
var_dump(Validate::as_array('["foo", "bar"]')); // ['foo', 'bar']
```

#### - When an object is passed:

```php
$data = new \StdClass;

$data->foo = 'bar';

var_dump(Validate::as_array($data)); // ['foo' => 'bar']
```

#### - When an JSON object is passed:

```php
var_dump(Validate::as_array('{"foo": "bar"}')); // ['foo' => 'bar']
```

#### - Parameter return default value when there's no a correct array:

```php
var_dump(Validate::as_array(false)); // null

var_dump(Validate::as_array(false, ['foo', 'bar'])); // ['foo', 'bar']
```

### - OBJECT:

#### - When an object is passed:

```php
$data = new \StdClass;

$data->foo = 'bar';

$object = Validate::as_object($data);

echo $object->foo; // 'bar'
```

#### - When an JSON object is passed:

```php
$object = Validate::as_object('{"foo": "bar"}');

echo $object->foo; // 'bar'
```

#### - When an array is passed:

```php
$object = Validate::as_object(['foo' => 'bar']));

echo $object->foo; // 'bar'
```

#### - Parameter return default value when there's no a correct object:

```php
var_dump(Validate::as_object(false)); // null

$object = Validate::as_object(false, ['foo' => 'bar']);

echo $object->foo; // 'bar'
```

### - JSON:

#### - When an JSON object is passed:

```php
echo Validate::as_json('{"foo": "bar"}'); // '{"foo": "bar"}'
```

#### - When an array is passed:

```php
echo Validate::as_json(['foo' => 'bar']); // '{"foo":"bar"}'
```

#### - When an object is passed:

```php
$data = new \StdClass;

$data->foo = 'bar';

echo Validate::as_json($data); // '{"foo":"bar"}'
```

#### - Parameter return default value when there's no a correct JSON:

```php
var_dump(Validate::as_json(false)); // null

echo Validate::as_json(false, '["foo", "bar"]'); // '["foo", "bar"]'
```

### - STRING:

#### - When an string is passed:

```php
echo Validate::as_string('foo'); // 'foo'
```

#### - When an integer is passed:

```php
echo Validate::as_string(221104); // '221104'
```

#### - Parameter return default value when there's no a correct string:

```php
var_dump(Validate::as_string(false)); // null

echo Validate::as_string(false, 'foo'); // 'foo'
```

### - INTEGER:

#### - When an integer is passed:

```php
echo Validate::as_integer(8); // 8
```

#### - When an string is passed:

```php
echo Validate::as_integer('8'); // 8
```

#### - Parameter return default value when there's no a correct integer:

```php
var_dump(Validate::as_integer(false)); // null

echo Validate::as_integer(false, 8); // 8
```

### - FLOAT:

#### - When an float is passed:

```php
echo Validate::as_float(8.8); // 8.8
```

#### - When an string is passed:

```php
echo Validate::as_float('8.8'); // 8.8
```

#### - Parameter return default value when there's no a correct float:

```php
var_dump(Validate::as_float(false)); // null

echo Validate::as_float(false, 8.8); // 8.8
```

### - BOOLEAN:

#### - When an boolean true is passed:

```php
var_dump(Validate::as_boolean(true)); // true
```

#### - When an string true is passed:

```php
var_dump(Validate::as_boolean('true')); // true
```

#### - When an integer one is passed:

```php
var_dump(Validate::as_boolean(1)); // true
```

#### - When an string one is passed:

```php
var_dump(Validate::as_boolean('1')); // true
```

#### - When an boolean false is passed:

```php
var_dump(Validate::as_boolean(false)); // false
```

#### - When an string false is passed:

```php
var_dump(Validate::as_boolean('false')); // false
```

#### - When an integer zero is passed:

```php
var_dump(Validate::as_boolean(0)); // false
```

#### - When an string zero is passed:

```php
var_dump(Validate::as_boolean('0')); // false
```

#### - Parameter return default value when there's no a correct boolean:

```php
var_dump(Validate::as_boolean(null)); // null

echo Validate::as_boolean(null, true); // true
```

### - IP:

#### - When an IP is passed:

```php
echo Validate::as_ip('255.255.255.0'); // '255.255.255.0'
```

#### - Parameter return default value when there's no a correct IP:

```php
var_dump(Validate::as_ip(null)); // null

echo Validate::as_ip(null, '255.255.255.0'); // '255.255.255.0'
```

### - URL:

#### - When an URL is passed:

```php
echo Validate::as_url('https://josantonius.com'); // 'https://josantonius.com'
```

#### - Parameter return default value when there's no a correct URL:

```php
var_dump(Validate::as_url(null)); // null

echo Validate::as_url(null, 'https://josantonius.com'); // 'https://josantonius.com'
```

### - Email:

#### - When an email is passed:

```php
echo Validate::as_email('hello@josantonius.com'); // 'hello@josantonius.com'
```

#### - Parameter return default value when there's no a correct email:

```php
var_dump(Validate::as_email(null)); // null

echo Validate::as_email(null, 'hello@josantonius.com'); // 'hello@josantonius.com'
```

<hr>

**Go to [SYSGUIDE Part 2](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md)**

<hr>

## License
The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt)
