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
fetch_json(data);

// $id = [1,2,3,4,5];
// echo fetch_json(["data" => $id]);
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

Available methods in this library:

#### - Set prefix for sessions:

```php
Session::set_prefix($prefix);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $prefix | Prefix for sessions. | object | Yes | |

**# Return** (boolean)

#### - Get sessions prefix:

```php
Session::get_prefix();
```

**# Return** (string) → sessions prefix

#### - Start session if session has not started:

```php
Session::init($lifeTime);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $lifeTime | Life time during session. | int | No | 0 |

**# Return** (boolean)

#### - Add value to a session:

```php
Session::set($key, $value);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $key | Session name. | string | Yes | |
| $value | The data to save. | mixed | No | false |

**# Return** (boolean true)

#### - Extract session item, delete session item and finally return the item:

```php
Session::pull($key);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $key | Item to extract. | string | Yes | |

**# Return** (mixed|null) → return item or null when key does not exists

#### - Get item from session:

```php
Session::get($key, $secondkey);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $key | Item to look for in session. | string | No | '' |
| $secondkey | If used then use as a second key. | string|boolean | No | false |

**# Return** (mixed|null) → return item or null when key does not exists

#### - Get session id:

```php
Session::id();
```

**# Return** (string) → the session id or empty

#### - Regenerate session_id:

```php
Session::regenerate();
```

**# Return** (string) → the new session id

#### - Empties and destroys the session:

```php
Session::destroy($key, $prefix);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $key | Session ID to destroy. | string | No | '' |
| $prefix | If true clear all sessions for current prefix. | boolean | No | false |

**# Return** (boolean)

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
Available methods in this library:

#### - Set cookie:

```php
Cookie::set($key, $value, $time);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $key | Cookie name. | string | Yes | |
| $value | The data to save. | string | Yes | |
| $time | Expiration time in days. | string | No | 365 |

**# Return** (boolean)

#### - Get item from cookie:

```php
Cookie::get($key);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $key | Cookie name. | string | No | '' |

**# Return** (mixed|false) → returns cookie value, cookies array or false

#### - Extract item from cookie and delete cookie:

```php
Cookie::pull($key);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $key | Cookie name. | string | Yes | |

**# Return** (string|false) → item or false when key does not exists

#### - Extract item from cookie and delete cookie:

```php
Cookie::destroy($key);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $key | Cookie name to destroy. Not set to delete all. | string | No | '' |

**# Return** (boolean)

#### - Set cookie prefix:

```php
Cookie::set_prefix($prefix);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $prefix | Cookie prefix. | string | Yes | |

**# Return** (boolean)

#### - Get cookie prefix:

```php
Cookie::get_prefix();
```

**# Return** (string) → cookie prefix

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

Resize
------

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

Crop
----

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

Loading and saving images from string
-------------------------------------

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

Displaying
----------

As seen above, you can call `$image->save('image.jpg');`

To render the image directly into the browser, you can call `$image->output()`;

Image Types
-----------

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

Interlacing
-----------

By default, [image interlacing](http://php.net/manual/en/function.imageinterlace.php) is turned on. It can be disabled by setting `$interlace` to `0`:

```php
$image = new ImageResize('image.jpg');
$image->scale(50);
$image->interlace = 0;
$image->save('image2.jpg');
```

Chaining
--------

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

Exceptions
--------

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

# String Library

Use this namespace in the controller :

```
use System\Libraries\Str;
```

## Available Methods

### - Check if the string starts with a certain value:

```php
Str::starts_with($search, $string);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $search | The string to search. | string | Yes | |
| $string | The string where search. | string | Yes | |

**# Return** (boolean)

### - Check if the string ends with a certain value:

```php
Str::ends_with($search, $string);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $search | The string to search. | string | Yes | |
| $string | The string where search. | string | Yes | |

**# Return** (boolean)

## Usage

Example of use for this library:

### - Check if the string starts with a certain value:

```php
Str::starts_with("Hello", "Hello world");
```

### - Check if the string ends with a certain value:

```php
Str::ends_with("world", "Hello World");
```

---

# LanguageCode Library

Use this namespace in the controller :

```
use System\Libraries\LanguageCode;
```

## Available Methods

Available methods in this library:

### - Get all language codes as array:

```php
LanguageCode::get();
```

**# Return** (array) → language codes and language names

### - Get language name from language code:

```php
LanguageCode::get_language_from_code($languageCode);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $languageCode | Language code, e.g. 'es'. | string | Yes | |

**# Return** (tring|false) → country name

### - Get language code from language name:

```php
LanguageCode::get_code_from_language($languageName);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $languageName | Language name, e.g. 'Spanish'. | string | Yes | |

**# Return** (tring|false) → language code

## Usage

Example of use for this library:
```php
LanguageCode::get();
```

---

# LoadTime Library

Use this namespace in the controller :

```
use System\Libraries\LoadTime;
```

## Available Methods

Available methods in this library:

### - Set initial time:

```php
LoadTime::start();
```

**# Return** (float) → microtime

### - Set end time:

```php
LoadTime::end();
```

**# Return** (float) → seconds

### - Check if the timer has been started:

```php
LoadTime::is_active();
```

**# Return** (boolean)

## Usage

Example of use for this library:

```php
<?php
LoadTime::start();

for ($i=0; $i < 100000; $i++) {
    // print_r($i . ' ');
}

print_r('Script executed in: ' . LoadTime::end() . ' seconds.');

/* Script executed in: 0.0012 seconds. */
```

---

# Json Library

Use this namespace in the controller :

```
use System\Libraries\Json;
```

## Available Methods

Available methods in this library:

### - Creating JSON file from array:

```php
Json::array_to_file($array, $file);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $array | Array to be converted to JSON. | array | Yes | |
| $file | Path to the file. | string | Yes | |

**# Return** (boolean)

### - Save to array the JSON file content:

```php
Json::file_to_array($file);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $file | Path or external url to JSON file. | string | Yes | |

**# Return** (array|false)

### - Check for errors:

```php
JsonLastError::check();
```

**# Return** (array|null) → Null if there are no errors or array with state  code and error message.

### - Get collection of JSON errors:

```php
JsonLastError::get_collection();
```

**# Return** (array) → Collection of JSON errors.

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

Json::array_to_file($array, $pathfile);

```

### - Save to array the JSON file content:

```php
$pathfile = public_path('file.json');

$array = Json::file_to_array($pathfile);

```

### - Check for errors:

```php
$lastError = JsonLastError::check();

if (!is_null($lastError)) {
    var_dump($lastError);
}
```

### - Get collection of JSON errors:

```php
$jsonLastErrorCollection = JsonLastError::get_collection();
```

---

# Curl Library

Use this namespace in the controller :

```
use System\Libraries\Curl;
```

## Available Methods

Available methods in this library:

### - Make request and get response website:

```php
Curl::request($url, $params, $result);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $url | Url when get content. | string | Yes | |

| Attribute | Key | Description | Type | Required | Default
| --- | --- | --- | --- | --- | --- |
| $params | | Parameters. | array | No | array() |
| | 'referer' | The referrer URL. | string | No | |
| | 'timeout' | Timeout. | int | No | |
| | 'agent' | Useragent. | string | No | |
| | 'headers' | HTTP headers. | array | No | |
| | 'data' | Parameters to send. | array | No | |
| | 'type' | Type of request. | string | No | |

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $result | Returns result as array or object. | string | No | 'array' |

**# Return** (array|object) → response

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

## Available Methods

Available methods in this library:

### - Check if a file exists in a path or url:

```php
File::exists($file);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $file | Path or file url. | string | Yes | |

**# Return** (boolean)

### - Delete file if exists:

```php
File::delete($file);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $file | File path. | string | Yes | |

**# Return** (boolean)

### - Create directory if not exists:

```php
File::create_dir($path);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $path | Path where to create directory. | string | Yes | |

**# Return** (boolean)

### - Copy directory recursively:

```php
File::copy_dir_recursively($from, $to);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $from| Path from copy. | string | Yes | |
| $to| Path to copy. | string | Yes | |

**# Return** (boolean)

### - Delete empty directory:

```php
File::delete_empty_dir($path);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $path | Path to delete. | string | Yes | |

**# Return** (boolean)

### - Delete directory recursively:

```php
File::delete_dir_recursively($path);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $path | Path to delete. | string | Yes | |

**# Return** (boolean)

### - Get files from directory:

```php
File::get_files_from_dir($path);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $path | Path where get file paths. | string | Yes | |

**# Return** (boolean)

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
get_class(File::get_files_from_dir(__DIR__));
```

---

# IP Library

Use this namespace in the controller :

```
use System\Libraries\Ip;
```

## Available Methods

Available methods in this library:

### - Get user's IP:

```php
Ip::get();
```

**# Return** (string|false) → user IP or false

### - Validate IP:

```php
Ip::validate($ip);
```

| Attribute | Description | Type | Required | Default
| --- | --- | --- | --- | --- |
| $ip | IP address to be validated. | string | Yes | |

**# Return** (boolean)

## Usage

Example of use for this library:

### - Get user's IP:

```php
Ip::get();
```

### - Validate IP:

```php
$ip = Ip::get();

Ip::validate($ip);
```

<hr>

## The Controllers

### Passing variable to view
If you want to passing variable to view, you can use example below :

```
$arr = [
	'my_name' => $this->m_welcome->welcome(),
	'mvc_page' => $this->m_hello->mvc_page(),
	'date' => Carbon::now()
];

$this->load_template('header', $arr);
```

The above example will generate variable `$my_name`, `$date` and `$mvc_page` in view.

### Load MVC or HMVC view file
#### Load MVC view file :

```
$this->load_view(null, 'filename');
```

#### Load HMVC view file :

```
$this->load_view('module-name', 'filename');
```

The PHP superglobals `post()` and `get()` are used to collect form-data.

```
post('hello');

// Same as $_POST['hello'];
```

```
get('hello');

// Same as $_GET['hello'];
```

### Sequence variable
Create a sequence of the named placeholders, e.g. `:id0`, `:id1`, `:id2`. So the code would be:

```
$this->bind('placeholders')->vars('variable')->sequence()

// $ids = [2,3,4];
// $this->bind(":id")->vars($ids)->sequence()
//
// Will return `print_r()` result
//
// Array
// (
//    [0] => :id0,:id1,:id2
//    [1] => Array
//        (
//            [:id0] => 2
//            [:id1] => 3
//            [:id2] => 4
//        )
// )
```

### Instantiate Model class in the controller
Instantiate the Model class in the controller is useful to make it easier for us to give variables to it.
So there is no need to rewrite the instantiate class in another method.

Just have to write it in the contruct method, like this:

```
public function __construct() {
	// Instantiate Model Crud
	$this->m_crud = new m_crud;
}
```

then `$this->m_crud` is the variable.

<hr>


## The Models

### Primary & Secondary Database Connections
NSY has supported 2 database connections in one running application.

You can see the env in root. There seems to be a configuration like this :

```
# Define Primary Connection
DB_CONNECTION=
DB_HOST=
DB_PORT=
DB_NAME=
DB_USER=
DB_PASS=

# Define Secondary Connection
DB_CONNECTION_SEC=
DB_HOST_SEC=
DB_PORT_SEC=
DB_NAME_SEC=
DB_USER_SEC=
DB_PASS_SEC=
```

Example for define Connection :

```
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_NAME=dev_example
DB_USER=root
DB_PASS=password
```

For example, in the model you want to run an sql query on the first database connection :

```
$q = 'SELECT * FROM blabla';
$this->connect()->query($q);
```

Then, if you want to run an sql query on the second database connection :

```
$q = 'SELECT * FROM blabla';
$this->connect_sec()->query($q);
```

### Getting data out of statement in dozens different formats. fetch_all()
That's most interesting function, with most astonishing features. Mostly thanks to its existence one can call PDO a wrapper, as this function can automate many operations otherwise performed manually.

`fetch_all()` returns an array that consists of all the rows returned by the query. From this fact we can make two conclusions:

This function should not be used, if many rows has been selected. In such a case conventional while loop ave to be used, fetching rows one by one instead of getting them all into array at once. "Many" means more than it is suitable to be shown on the average web page.

This function is mostly useful in a modern web application that never outputs data right away during fetching, but rather passes it to template.
You'd be amazed, in how many different formats this function can return data in (and how little an average PHP user knows of them), all controlled by `FETCH...` variables. Some of them are: `FETCH_NUM, FETCH_ASSOC, FETCH_BOTH, FETCH_CLASS, FETCH_KEY_PAIR, FETCH_UNIQUE, FETCH_GROUP, and FETCH_FUNC`.

#### Getting a plain array.
By default, this function will return just simple enumerated array consists of all the returned rows. Row formatting constants, such as `FETCH_NUM, FETCH_ASSOC, FETCH_COLUMN` etc can change the row format.

```
$q = 'SELECT id, name, username FROM users';
$d = $this->connect()->query($q)->style(FETCH_ASSOC)->fetch_all();

print_r($d);

// output
Array
(
    [0] => Array
        (
            [id] => 1
            [name] => Vikry Yuansah
            [user_name] => vikry
        )
)
```

#### Getting a column number.
It is often very handy to get plain one-dimensional array right out of the query, if only one column out of many rows being fetched. Here you go:

```
$q = 'SELECT name FROM users';
$d = $this->connect()->query($q)->style(FETCH_COLUMN)->fetch_all();

print_r($d);

// output
Array
(
    [0] => Vikry Yuansah
)
```

#### Getting key-value pairs.
Also extremely useful format, when we need to get the same column, but indexed not by numbers in order but by another field. Here goes `FETCH_KEY_PAIR` constant:

```
$q = 'SELECT name FROM users';
$d = $this->connect()->query($q)->style(FETCH_KEY_PAIR)->fetch_all();

print_r($d);

// output
Array
(
    [1] => Vikry Yuansah
    [2] => Nayla Syifa
)
```

and many other modes in fetch_all.

### Getting data out of statement. fetch()
It fetches a single row from database, and moves the internal pointer in the result set, so consequent calls to this function will return all the resulting rows one by one.

```
$q = 'SELECT id, name FROM users';
$d = $this->connect()->query($q)->style(FETCH_NUM)->fetch();

print_r($d);

// output
Array
(
    [0] => 1
    [1] => Vikry Yuansah
)
```

Another way would be to bind these variables explicitly while setting the proper param type:

Binds a PHP variable to a corresponding named or question mark placeholder in the SQL statement that was used to prepare the statement.

BindValue with PARAM_INT (Defines variable type as integer/number) :

```
$id = [ ':id' => [3, PAR_INT] ];

$q = "SELECT id, name, user_name FROM tbl_users WHERE id = :id";
$d = $this->connect()->query($q)->vars($id)->bind(BINDVAL)->fetch();

print_r($d);

// output
Array
(
    [id] => 3
    [0] => 3
    [name] => Tialuna
    [1] => Tialuna
    [user_name] => tia
    [2] => tia
)
```

BindParam with PARAM_STR (Defines the variable type as a text string) :

```
$string = [ ':name' => ['%yuan%', PAR_STR] ];

$q = "SELECT id, name, user_name FROM tbl_users WHERE name LIKE :name";
$d = $this->connect()->query($q)->vars($string)->bind(BINDPAR)->fetch();

print_r($d);

// output
Array
(
    [id] => 1
    [0] => 1
    [name] => Vikry Yuansah
    [1] => Vikry Yuansah
    [user_name] => vikry
    [2] => vikry
)
```

Unlike `BINDVAL`, the variable is bound as a reference and will only be evaluated at the time that `exec()` is called.

`BINDPAR` to bind PHP variables to the parameter markers: bound variables pass their value as input and receive the output value, if any, of their associated parameter markers

### Getting data out of statement. fetch_column()
A neat helper function that returns value of the single field of returned row. Very handy when we are selecting only one field:

```
// Getting the name based on id
$id = [ ':id' => 2 ];

$q = "SELECT name FROM tbl_users WHERE id = :id";
$d = $this->connect()->query($q)->vars($id)->fetch_column();

return $d;

// output
Nayla Syifa
```

```
// getting number of rows in the table utilizing method chaining
$q = "SELECT count(*) FROM tbl_users";
$d = $this->connect()->query($q)->fetch_column();

return $d;

// output
3 => number of row data
```

### Getting row count
NSY uses PDO. PDO offers a function for returning the number of rows found by the query, `row_count()`, for example:

```
$q = "SELECT * FROM tbl_users";
$d = $this->connect()->query($q)->row_count();

return $d->result;

// output
3 => number of row data
```

However, if you want to get the number of affected rows, here is an example:

```
$id = [ ':id' => 2 ];

$q = "DELETE FROM tbl_users WHERE id = :id";
$deleted_data = $this->connect()->vars($id)->query($q)->row_count();

return deleted_data->result;

// output
1 => number of row data that was deleted
```

### Executes a prepared statement. exec()

#### Update data :

```
$id = [ ':id' => 2 ];

$q = "UPDATE tbl_users SET name = :name WHERE id = :id";
$this->connect()->query($q)->vars($id)->exec();

// Update field name from tbl_users where id is 2
```

#### Multi Update data :

```
$id = [ 11025, 11026 ];
foreach ( $id as $key => $ids ) {
  $params = [
    ':id' => $ids,
    ':user_name' => 'nsy_for_kids'
  ];
  $q = "UPDATE tbl_users SET user_name = :user_name WHERE id = :id";
  $this->connect()->query($q)->vars($params)->exec();
}

// Update field user_name to 'nsy_for_kids' from tbl_users where id is 11025 & 11026
```

#### Delete data :

```
$id = [ ':id' => 2 ];

$q = "DELETE FROM tbl_users WHERE id = :id";
$this->connect()->query($q)->vars($id)->exec();

// Delete data from tbl_users where id is 2
```

#### Multi Delete data :

```
$id = [ 11025, 11026 ];
foreach ( $id as $key => $ids ) {
  $params = [
    ':id' => $ids
  ];
  $q = "DELETE FROM tbl_users WHERE id = :id";
  $this->connect()->query($q)->vars($params)->exec();
}

// Delete data from tbl_users where id is 11025 & 11026
```

#### Insert data :

```
$param = [ ':user_name' => 'Harmoni' ];

$q = "INSERT INTO tbl_users (user_name) VALUES (:user_name)";
$this->connect()->query($q)->vars($param)->exec();

// Insert data to field user_name from tbl_users where user_name is 'Harmoni'
```

### Multi Insert. multi_insert()
To input multiple data into the database at once in one command.

```
$arr = [
    [0] => [
        [0] => 11043 // for column id on tbl_users
        [1] => Vikry Yuansah // for column name on tbl_user
        [2] => vikry // for column user_name on tbl_user
    ],
    [1] => [
        [0] => 11042 // for column id on tbl_users
        [1] => Tialuna // for column name on tbl_user
        [2] => tia // for column user_name on tbl_user
    ]
];
$q = "INSERT INTO tbl_users (id, name, user_name)";
$this->connect()->query($q)->vars($arr)->multi_insert();
```

### NSY Transaction
Database transactions ensure that a set of data changes will only be made permanent if every statement is successful. Any query or code failure during a transaction can be caught and you then have the option to roll back the attempted changes.

NSY provides simple methods for beginning, committing, and rollbacking back transactions.

#### Begin transaction :

```
$this->begin_trans();
```

#### Commit transaction :

```
$this->end_trans();
```

#### Rollback transaction :

```
$this->null_trans();
```

#### First example of transaction in `multi_insert()`.

```
$arr = [
    [0] => [
        [0] => 11043 // for column id on tbl_users
        [1] => Vikry Yuansah // for column name on tbl_user
        [2] => vikry // for column user_name on tbl_user
    ],
    [1] => [
        [0] => 11042 // for column id on tbl_users
        [1] => Tialuna // for column name on tbl_user
        [2] => tia // for column user_name on tbl_user
    ]
];
$q = "INSERT INTO tbl_users (id, name, user_name)";
$this->connect()->begin_trans()->query($q)->vars($arr)->multi_insert()->end_trans();
```

#### Second example of transaction in `multi_insert()`.

```
$arr = [
    [0] => [
        [0] => 11043 // for column id on tbl_users
        [1] => Vikry Yuansah // for column name on tbl_user
        [2] => vikry // for column user_name on tbl_user
    ],
    [1] => [
        [0] => 11042 // for column id on tbl_users
        [1] => Tialuna // for column name on tbl_user
        [2] => tia // for column user_name on tbl_user
    ]
];
$q = "INSERT INTO tbl_users (id, name, user_name)";
$conn = $this->connect();
$conn->begin_trans();
$conn->query($q);
$conn->vars($arr);
$conn->multi_insert();
$conn->end_trans();
```

`begin_trans()` must be located in each code after we define the connection `$this->connect()`.

And before using a transaction, you must turn on the transaction mode in `config/app.php` => `transaction` to `on` (default is `off`), to turn on the rollback function (The rollback function is enabled by default when `transaction = on`, so there's no need to call the `null_trans()`).

### Emulation mode, set ATTR_EMULATE_PREPARES to FALSE
For more information about this, go to the following URL [Emulation mode](https://phpdelusions.net/pdo#emulation).

```
$this->emulate_prepares_false();
```

### Mysqlnd and buffered queries. Huge datasets.
For more information about this, go to the following URL [Mysqlnd and buffered queries](https://phpdelusions.net/pdo#mysqlnd).

#### set MYSQL_ATTR_USE_BUFFERED_QUERY to FALSE

```
$this->use_buffer_query_false();
```

#### set MYSQL_ATTR_USE_BUFFERED_QUERY to TRUE

```
$this->use_buffer_query_true();
```

### Return type, set ATTR_STRINGIFY_FETCHES to TRUE
For more information about this, go to the following URL [Return type](https://phpdelusions.net/pdo#returntypes).

```
$this->stringify_fetches_true();
```

<br/>

**Go to [SYSGUIDE Part 2](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md)**

<hr>

## License
The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt)
