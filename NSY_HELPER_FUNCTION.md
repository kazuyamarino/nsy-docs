# NSY Helper Function

## Standard Helper Function

### The PHP superglobals `post`, `deposer` and `get` are used to collect form-data

```php
post('hello');

// Same as $_POST['hello'];
```

```php
get('hello');

// Same as $_GET['hello'];
```

```php
deposer(array(some_array));

// Same as $_FILE[ array(some_array) ];
```

### Public Directory Path

Returns your site full path `public` directory, as specified in your config file.

```php
echo public_path();

// for example
usr/share/../html/nsy/public/
```

### Images Directory Url

Return img directory location on the `public` directory.

```php
echo img_url();

// for Example
// http://example.com/public/img
```

### Javascript Directory Url

Return js directory location on the `public` directory.

```php
echo js_url();

// for Example
// http://example.com/public/js
```

### CSS Directory Url

Return css directory location on the `public` directory.

```php
echo css_url();

// for Example
// http://example.com/public/css
```

### Get Version

Get `version` parameter value from `Config/Site.php`.

```php
echo get_version();

// 3.0.0
```

### Get Codename

Get `codename` parameter value from `Config/Site.php`.

```php
echo get_codename();

// Tifa
```

### Get Language Code

Get `locale` parameter value from `Config/App.php`.

```php
echo get_lang_code();

// en
```

### Open Graph Prefix

Get `prefix_attr` parameter value from `Config/App.php`.

```php
echo get_og_prefix();
```

### Get Site Title

Get `sitetitle` parameter value from `Config/Site.php`.

```php
echo get_title();
```

### Get Site Description

Get `sitedesc` parameter value from `Config/Site.php`.

```php
echo get_desc();
```

### Get Site Keywords

Get `sitekeywords` parameter value from `Config/Site.php`.

```php
echo get_keywords();
```

### Get Site Author

Get `siteauthor` parameter value from `Config/Site.php`.

```php
echo get_author();
```

### Get Session Prefix

Get `session_prefix` parameter value from `Config/App.php`.

```php
echo get_session_prefix();
```

### Get Site Email

Get `siteemail` parameter value from `Config/Site.php`.

```php
echo get_site_email();
```

---

## Getting Config Value

If you want to take values ​​in the config file on the `System/Config`, this is the way :

**Get value from `App.php`**

```php
config_app('value_name');
// config_app('app_env');
```

**Get value from `Site.php`**

```php
config_site('value_name');
// config_site('sitetitle');
```

---

## Define an empty variable or a non-empty variable

In NSY, there is a function to make it easier for users to see whether a value is empty or not in a variable. i.e. with only 2 methods `not_filled()` and `is_filled()`.

`not_filled()`, is to determine a variable that has no value.
`is_filled()`, is to determine a variable has a value.

**Example :**

```php
$var = null;
not_filled($var); // output return true.
```

```php
$var = 5;
is_filled($var); // output return true.
```

**Reference of the method :**

For example, we have several variables with their respective values ​​that have been determined.

```php
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

then, if the variables above are used with the `is_filled` and `not_filled` methods, they will produce variable values ​​like the following :

Result of `not_filled()` :

```php
$var1 = empty
$var2 = not empty
$var3 = empty
$var4 = not empty
$var5 = empty
$var6 = empty
$var7 = empty
$var8 = empty
$var9 = empty
$var10 = empty
```

Result of `is_filled()` :

```php
$var1 = empty
$var2 = not empty
$var3 = empty
$var4 = not empty
$var5 = empty
$var6 = empty
$var7 = empty
$var8 = empty
$var9 = empty
$var10 = empty
```

---

## Base URL

Returns your site base URL, as specified in your config file.

```php
echo base_url();

// http://example.com/
```

You can supply segments as a string. Here is a string example:

```php
echo base_url("hmvc/action");
```

The above example would return something like: <http://example.com/hmvc/action>

You can supply a string to a file, such as an image or stylesheet. For example:

```php
echo base_url("images/edit.png");
```

This would give you something like: <http://example.com/images/edit.png>

---

## Redirect URL

Redirect method is used to send a raw HTTP header. Here is the example:
>
>```php
>redirect('hmvc/success');
>```
>
>The above example would return redirect url to: ><http://example.com/hmvc/success>

Another function is `redirect_url()`, serves to redirect to a web page with a more complete and specific address.
>
>```php
>redirect_url('http://example.com/hmvc/blog/page');
>```
>
>The above example would return : <http://example.com/hmvc/blog/page>
>
>```php
>redirect_back();
>```
>
>The above example would return redirect to previous page.

---

## Simple Ternary

Ternary operator logic is the process of using "`(condition) ? (true return value) : (false return value)`" statements to shorten your if/else structures.

```php
terner(condition, return true, return false)
```

**Example :**

```php
/* most basic usage */

$var = 5;
$var_is_greater_than_two = terner($var > 2, true, false);

// output returns true
```

---

## Aurora File Export

Aurora is a library created to export data into several file formats supported by aurora such as `txt`, `xls`, `ods`, & etc.

```php
aurora(file_extension, filename, separator, header, data, string_delimiter);
```

### Variable explanation

1. `file_extension` is a supported file extension by aurora. `(txt, csv, xls, xlsx, & ods)`.
2. `filename` is a filename defined by user.
3. `separator` is a delimiter of each data or table column `(tab, comma, semicolon, space, pipe, & dot)`.
4. `header` is the top or title of each column.
5. `data` is the contents of the table data or record.
6. `string_delimiter` is quote each string `("double" for double quote, & 'single' for singlequote)`.

**Example :**

```php
// header data array structure should be like this
$header = [ 'Col1', 'Col2', 'Col3' ];

// columns data array structure should be like this
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

## Get User Agent

This is how to get user agent data with ease.

```php
get_ua()
```

**Example :**

```php
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

## Generate Random Number

To generate a sequence of random numbers that correspond to the desired number or prefix.

```php
generate_num(prefix, random_number_length, total_number/char_length);
```

**Example :**

```php
echo generate_num();
// Default output NSY-617807

echo generate_num("VYLMA-", 4, 10);
// Output VYLMA-6906
```

---

## Get URI Segment

To help in retrieving data in URIs

```php
get_uri_segment(segment number)
```

**Example :**

```php
http://localhost/nsy/hmvc

echo get_uri_segment(1);
// Output is nsy

echo get_uri_segment(2);
// Output is hmvc
```

**Get last URI Segment on any route condition :**

```php
get_last_uri_segment()
```

if there is a web url like the following `localhost/platforma/wa/sendblast-pc`, then with `get_last_uri_segment()` it will get the last url segment `sendblast-pc`.

**Get complete URI :**

```php
get_uri()
```

---

## Simple string encryption/decryption function

**To encrypt string :**

```php
string_encrypt($action = 'encrypt', $string = '')
```

**To decrypt string :**

```php
string_encrypt($action = 'decrypt', $string = '')
```

---

## Convert image file to base64

```php
image_to_base64($files = '')
```

---

## Convert image string to base64

```php
string_to_base64($string = '')
```

---

## Convert large positive numbers in to short form

Use to convert large positive numbers in to short form like 1K+, 100K+, 199K+, 1M+, 10M+, 1B+ etc

```php
number_format_short($value = 0)
```

---

## Array Flatten

PHP array_flatten() function. Convert a multi-dimensional array into a single-dimensional array :

```php
array_flatten($items);

// $id = array_flatten([1, [2, [3], 4], 5]);
// print_r($id);
//
// Will return : [1, 2, 3, 4, 5]
```

---

## Fetch to JSON

If you want to display data values ​​in json form, you can do this method :

```php
json_fetch($data, $http_response_code);

// $id = [1,2,3,4,5];
// echo json_fetch(["data" => $id], 200);
//
// Will return :
// {
//   "data": [
//     1,
//     2,
//     3,
//     4,
//     5
//   ]
// }
```

---

## PHP Session Library

Use this namespace in the controller :

```php
use System\Libraries\Facades\Session;

Session::start();
```

Or

```php
use System\Libraries\Session

$Session = new Session();
$Session->start();
```

**Usage :**

Go to the PHP Session Library documentation page, [HERE](https://github.com/josantonius/php-session).

---

## Cookie Library

Use this namespace in the controller :

```php
use System\Libraries\Facades\Cookie;
```

**Usage :**

Go to the Cookie Library documentation page, [HERE](https://github.com/josantonius/php-cookie)

---

## NSY FTP Client Library

Use this namespace in the controller :

```php
use System\Vendor\Ftp;
```

NSY supports a flexible FTP and SSL-FTP client for PHP. This library provides helpers easy to use to manage the remote files. [nicolab/php-ftp-client](https://github.com/Nicolab/php-ftp-client).

You only need to instantiate the class in the construct method `__contruct`.
[See Instantiate Model class in the controller](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE.md#instantiate-model-class-in-the-controller).

### Login to FTP

```php
$this->ftp = new Ftp();
$this->ftp->connect('website.com');
$this->ftp->login('admin@website.com', 'password');

// Turns passive mode on (true) or off (false)
$this->ftp->pasv(true);
```

### Returns the last modified time of the given file

```php
$this->ftp->modifiedTime('path/of/file');
```

### Changes to the parent directory

```php
$this->ftp->up();
```

### Returns a list of files in the given directory

```php
$this->ftp->nlist('path/of/directory', true);
```

### Removes a directory

```php
$this->ftp->rmdir('path/of/directory/to/remove');
```

### Removes a directory (recursive)

```php
$this->ftp->rmdir('path/of/directory/to/remove', true);
```

### Creates a directory

```php
$this->ftp->mkdir('path/of/directory/to/create');
```

### Creates a directory (recursive), creates automaticaly the sub directory if not exist

```php
$this->ftp->mkdir('path/of/directory/to/create', true);
```

### Check if a directory exist

```php
$this->ftp->isDir('path/of/directory');
```

### Check if a directory is empty

```php
$this->ftp->isEmpty('path/of/directory');
```

### Scan a directory and returns the details of each item

```php
$this->ftp->scanDir('path/of/directory');
```

### Returns the total size of the given directory in bytes

```php
$this->ftp->dirSize('path/of/directory');
```

## Count method

### Count in the current directory

```php
$total = $this->ftp->count();
```

### Count in a given directory

```php
$total = $this->ftp->count('/path/of/directory');
```

### Count only the "files" in the current directory

```php
$total_file = $this->ftp->count('.', 'file');
```

### Count only the "files" in a given directory

```php
$total_file = $this->ftp->count('/path/of/directory', 'file');
```

### Count only the "directories" in a given directory

```php
$total_dir = $this->ftp->count('/path/of/directory', 'directory');
```

### Count only the "symbolic links" in a given directory

```php
$total_link = $this->ftp->count('/path/of/directory', 'link');
```

### Downloads a file from the FTP server into a string

```php
$this->ftp->getContent('path/of/file');
```

## Upload method

### Uploads a file to the server from a string

```php
$this->ftp->putFromString('path/of/file', 'string');
```

### Uploads a file to the server

```php
$this->ftp->putFromPath('path/of/file');
```

### upload with the BINARY mode

```php
$this->ftp->putAll('source_directory', 'target_directory');
```

### Is equal to

```php
$this->ftp->putAll('source_directory', 'target_directory', FTP_BINARY);
```

### Or upload with the ASCII mode

```php
$this->ftp->putAll('source_directory', 'target_directory', FTP_ASCII);
```

### Downloads all files from remote FTP directory

```php
$this->ftp->getAll('source_directory', 'target_directory', FTP_BINARY);
```

### Returns a detailed list of files in the given directory

```php
$this->ftp->rawlist('path/of/directory');
```

### Parse raw list

```php
$d = $this->ftp->rawlist('path/of/directory');
$e = $this->ftp->parseRawList($d);
```

### Convert raw info (drwx---r-x ...) to type (file, directory, link, unknown)

```php
$this->ftp->rawToType('drwx---r-x');
```

### Set permissions on a file via FTP

```php
$this->ftp->chmod('0775', 'path/of/file');
```

---

## Carbon Library

Use this namespace in the controller :

```php
use System\Vendor\Carbon;
```

Go to the Carbon Library documentation page, [HERE](https://carbon.nesbot.com/docs/)

---

## Validate Library

Example of use for this library:

### ARRAY

**When an array is passed :**

```php
var_dump(validate_array(['foo', 'bar'])); // ['foo', 'bar']
```

**When an JSON array is passed :**

```php
var_dump(validate_array('["foo", "bar"]')); // ['foo', 'bar']
```

**When an object is passed :**

```php
$data = new \StdClass;

$data->foo = 'bar';

var_dump(validate_array($data)); // ['foo' => 'bar']
```

**When an JSON object is passed :**

```php
var_dump(validate_array('{"foo": "bar"}')); // ['foo' => 'bar']
```

**Parameter return default value when there's no a correct array :**

```php
var_dump(validate_array(false)); // null

var_dump(validate_array(false, ['foo', 'bar'])); // ['foo', 'bar']
```

### OBJECT

**When an object is passed :**

```php
$data = new \StdClass;

$data->foo = 'bar';

$object = validate_object($data);

echo $object->foo; // 'bar'
```

**When an JSON object is passed :**

```php
$object = validate_object('{"foo": "bar"}');

echo $object->foo; // 'bar'
```

**When an array is passed :**

```php
$object = validate_object(['foo' => 'bar']));

echo $object->foo; // 'bar'
```

**Parameter return default value when there's no a correct object :**

```php
var_dump(validate_object(false)); // null

$object = validate_object(false, ['foo' => 'bar']);

echo $object->foo; // 'bar'
```

### JSON

**When an JSON object is passed :**

```php
echo validate_json('{"foo": "bar"}'); // '{"foo": "bar"}'
```

**When an array is passed :**

```php
echo validate_json(['foo' => 'bar']); // '{"foo":"bar"}'
```

**When an object is passed :**

```php
$data = new \StdClass;

$data->foo = 'bar';

echo validate_json($data); // '{"foo":"bar"}'
```

**Parameter return default value when there's no a correct JSON :**

```php
var_dump(validate_json(false)); // null

echo validate_json(false, '["foo", "bar"]'); // '["foo", "bar"]'
```

### STRING

**When an string is passed :**

```php
echo validate_string('foo'); // 'foo'
```

**When an integer is passed :**

```php
echo validate_string(221104); // '221104'
```

**Parameter return default value when there's no a correct string :**

```php
var_dump(validate_string(false)); // null

echo validate_string(false, 'foo'); // 'foo'
```

### INTEGER

**When an integer is passed :**

```php
echo validate_integer(8); // 8
```

**When an string is passed :**

```php
echo validate_integer('8'); // 8
```

**Parameter return default value when there's no a correct integer :**

```php
var_dump(validate_integer(false)); // null

echo validate_integer(false, 8); // 8
```

### FLOAT

**When an float is passed :**

```php
echo validate_float(8.8); // 8.8
```

**When an string is passed :**

```php
echo validate_float('8.8'); // 8.8
```

**Parameter return default value when there's no a correct float :**

```php
var_dump(validate_float(false)); // null

echo validate_float(false, 8.8); // 8.8
```

### BOOLEAN

**When an boolean true is passed :**

```php
var_dump(validate_boolean(true)); // true
```

**When an string true is passed :**

```php
var_dump(validate_boolean('true')); // true
```

**When an integer one is passed :**

```php
var_dump(validate_boolean(1)); // true
```

**When an string one is passed :**

```php
var_dump(validate_boolean('1')); // true
```

**When an boolean false is passed :**

```php
var_dump(validate_boolean(false)); // false
```

**When an string false is passed :**

```php
var_dump(validate_boolean('false')); // false
```

**When an integer zero is passed :**

```php
var_dump(validate_boolean(0)); // false
```

**When an string zero is passed :**

```php
var_dump(validate_boolean('0')); // false
```

**Parameter return default value when there's no a correct boolean :**

```php
var_dump(validate_boolean(null)); // null

echo validate_boolean(null, true); // true
```

### IP

**When an IP is passed :**

```php
echo validate_ip('255.255.255.0'); // '255.255.255.0'
```

**Parameter return default value when there's no a correct IP :**

```php
var_dump(validate_ip(null)); // null

echo validate_ip(null, '255.255.255.0'); // '255.255.255.0'
```

### URL

**When an URL is passed :**

```php
echo validate_url('https://josantonius.com'); // 'https://josantonius.com'
```

**Parameter return default value when there's no a correct URL :**

```php
var_dump(validate_url(null)); // null

echo validate_url(null, 'https://josantonius.com'); // 'https://josantonius.com'
```

### Email

**When an email is passed :**

```php
echo validate_email('hello@josantonius.com'); // 'hello@josantonius.com'
```

**Parameter return default value when there's no a correct email :**

```php
var_dump(validate_email(null)); // null

echo validate_email(null, 'hello@josantonius.com'); // 'hello@josantonius.com'
```

---

## LanguageCode Method

**Get all language codes as array :**

```php
get_all_lang();
```

```php
print_r( get_all_lang() );
```

**# Return** (array) → language codes and language names

**Get language name from language code :**

```php
get_lang_name($languageCode);
```

```php
get_lang_name('id');
```

**# Return** (tring|false) → country name

**Get language code from language name :**

```php
get_lang_code($languageName);
```

```php
get_lang_code('Indonesian');
```

**# Return** (string|false) → language code

---

## LoadTime Method

### Set initial time

```php
loadtime_start();
```

**# Return** (float) → microtime

### Set end time

```php
loadtime_end();
```

**# Return** (float) → seconds

### Check if the timer has been started

```php
loadtime_active();
```

**# Return** (boolean)

### Example of use for this library

```php
loadtime_start();

for ($i=0; $i < 100000; $i++) {
    // print_r($i . ' ');
}

print_r('Script executed in: ' . loadtime_end() . ' seconds.');

/* Script executed in: 0.0012 seconds. */
```

---

## Json Library

Use this namespace in the controller :

```php
use System\Libraries\Json;
```

**Usage :**

Go to the Json Library documentation page, [HERE](https://github.com/josantonius/php-json)

---

## Curl Library

Use this namespace in the controller :
```
use System\Vendor\Curl;
```

**Usage :**
Go to the Curl Library documentation page, [HERE](https://github.com/php-curl-class/php-curl-class/tree/9.14.2)

---

## File Library

Use this namespace in the controller :

```php
use System\Libraries\File;
```

### Example of use for this library

#### Check if a local file exists :

```php
check_file('path/to/file.php');
```

#### Check if a external file exists :

```php
check_file('https://raw.githubusercontent.com/Josantonius/PHP-File/master/composer.json');
```

#### Delete a local file :

```php
delete_file(public_path('file.txt'));
```

#### Create directory :

```php
create_dir(public_path('/test/'));
```

#### Delete empty directory :

```php
delete_dir(public_path('/test/'));
```

#### Delete directory recursively :

```php
delete_dir_recur(public_path('/test/'));
```

#### Copy directory recursively :

```php
copy_dir_recur(public_path('/test/'), public_path('/copy/'));
```

#### Get file paths from directory :

```php
get_files_from_dir(__DIR__);
```

#### Writes data to the file specified in the path :

```php
create_file($path, $data, $mode = 'wb');
```

#### Get Filenames :

```php
get_filenames($source_dir, $include_path = false, $_recursion = false);
```

#### Get Directory File Information :

```php
get_dir_file_info($source_dir, $top_level_only = true, $_recursion = false);
```

#### Get File Info :

```php
get_file_info($file, $returned_values = array('name', 'server_path', 'size', 'date'));
```

#### Get Mime by Extension :

```php
get_mime_by_extension($filename);
```

#### Returns the MIME types array from Config/Mimes.php :

```php
get_mimes();
```