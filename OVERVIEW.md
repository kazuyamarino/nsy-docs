# Overview

---

## Composer

Composer helps you declare, manage, and install dependencies of PHP projects.

See [https://getcomposer.org/](https://getcomposer.org/) for more information and documentation.

#### Installation / Usage
>
> Download and install Composer by following the [official instructions](https://getcomposer.org/download/).
>
> For usage, see [the documentation](https://getcomposer.org/doc/).

#### Packages
>
> Find packages on [Packagist](https://packagist.org).

#### Composer on NSY framework
>
> The composer on the nsy framework has a function to generate autoload in the HMVC module folder.
>
>NSY applies the concept of PSR-4 Autoloading. NSY has the `composer.json` file that can be dumped with [composer](https://getcomposer.org/download/) command `composer dump-autoload -o` or [NSY CLI](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#nsy-cli-command-line) command `nsy dump:autoload` when creating a folder structure that contains new class files.
>
>#### For example :
>
> * There is an example folder in the module folder that was created named `Homepage`, along with the namespaces.
>
> * In the `Homepage` folder there must be a `Models` folder, `Views` folder, and `Controllers` folder.
>
> The folder structure should be like this
>
>```
>Modules
>    │   └── Homepage
>    │       ├── Controllers
>    │       │  
>    │       ├── Models
>    │       │  
>    │       └── Views
>    │           
>```
>
> * Now, you can generate autoload class in the `Models` folder & `Controllers` folder for the `Homepage` with `composer dump-autoload -o` or [NSY CLI](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#nsy-cli-command-line) command `nsy dump:autoload` on the command line terminal.

---

## Framework Configuration

The NSY_Framework Configuration is very simple. There are 3 config file in `System/Config` directory :

* `App.php` for application setting such as system path of the framework.
* `Assets.php` for css or js configuration.
* `Site.php` for meta site configuration.
* `Mimes.php` this file contains an array of mime types.

```
├── Config
    │   ├── App.php
    │   ├── Assets.php
    │   └── Site.php
    │   └── Mimes.php
```

* `system.js` file

```
system.js is located in `public/js/config/system.js` folder.
```

In system.js there is a `base_url` configuration for javascript *(see line 13 - 15)*. This `base_url` is used for the purpose of initializing the function of the <strong>Datatable Ajax URL</strong> in the `public/js/datatables/init.js`*

```For Example see Shyffon repository [https://github.com/kazuyamarino/shyffon](Here!)```

---

## Helpers

The `System/Helpers` folder is useful for creating custom methods that match what you want and need.

If you want to make your own helper, then just make the desired method in the php file then save it in`System/Helpers`. And don't forget to autoload it on `composer.json` in the `files` parameters.

```
"autoload": {
 "psr-4": {
  "System\\": "System/"
 },
 "files": [
  "System/Helpers/Custom_Method.php" // your custom helpers file
 ]
}
```

---

## Routes

NSY Routing system using classes from [Macaw route by Noah Buscher](https://github.com/noahbuscher/macaw), and it's located in the `System/Routes` directory.

```
├── Routes
    │   ├── Api.php
    │   └── Web.php
    │   └── Migration.php
```

> #### Examples :
>
> ```PHP
> Route::get('/', function() {
> echo 'Hello world!';
> });
> ```

Route also supports regex parameters (Uri params), such as:

```
':all'   => '.*',
':any'   => '[^/]+',
':slug'   => '[a-z0-9-]+',
':uslug'  => '[\w-]+',   // slug + underscores
':num'   => '[0-9]+',
':alpha'  => '[A-Za-z]+',
':alnum'  => '[0-9A-Za-z]+',
':date'    => '[0-9]{4}-[0-9]{2}-[0-9]{2}'
```

```PHP
Route::get('/(:any)', function($slug) {
  echo 'The slug is: ' . $slug;
});

// equivalent to Route::match('get|post|put|patch|delete|head|options',..)
Route::any('/', function() {};)
```

You can also make requests for HTTP methods in NSY_Router, so you could also do:

```PHP
Route::get('/', function() {
  echo 'I'm a GET request!';
});

Route::post('/', function() {
  echo 'I'm a POST request!';
});

Route::any('/', function() {
  echo 'I can be both a GET and a POST request!';
});
```

#### Example passing to a controller instead of a closure

It's possible to pass the namespace path to a controller instead of the closure:

For this demo lets say I have a folder called controllers with a demo.php

```php
// demo.php :

<?php
namespace System\Controllers;

class Demo {

    public function __contruct()
    {

    }

    public function index()
    {
        echo 'home';
    }

    public function page()
    {
        echo 'page';
    }

    public function view($id)
    {
        echo $id;
    }

}
```

```php
// Web.php :

Route::get('/', function() {
 Route::goto('Demo@index');
});

Route::get('/page', function() {
 Route::goto('Demo@page');
});

Route::get('/view/(:num)', function($id) {
 Route::goto('Demo@view', $id);
});
```

#### Example passing to a controller inside hmvc module

For this demo lets say I have a module folder called `Homepage` and folder controllers inside with a login.php name.

```php
// login.php :

namespace System\Modules\Homepage\Controllers;

class Login {

    public function index()
    {
        echo 'login dashboard';
    }

    public function view($params)
    {
        echo $params['id'];
        echo "<br>";
        echo $params['user'];
    }

}
```

```php
// Web.php :

Route::get('/Homepage', function() {
 Route::goto('Homepage\Login@index');
});

Route::get('/view/(:num)/(:alpha)', function($id, $user) {
  $params = [
    'id' => $id,
    'user' => $user
  ];
 Route::goto('Homepage\Login@view', $params);
});
```

#### Another way to call a controller with minimal code instead of Route::goto()

```php
Route::get('/', 'Welcome@index');
Route::get('/hmvc', 'Homepage\Hello@index_hmvc');
```

#### Route group with (base path)

```php
Route::group('/admin', function() {
  // map to /admin/input
 Route::get('/input', function() {
  echo 'input user';
 });

  // map to /admin/delete
 Route::get('/delete', function() {
  echo 'delete user';
 });
});
```

#### If there is no route defined for a certain location, you can make NSY_Router run a custom callback

```php
Route::error(function() {
  echo '404 :: Not Found';
});
```

If you don't specify an error callback, NSY_Router will just echo `404`.

---

## MVC & HMVC

* The Model View Controller (MVC) design pattern specifies that an application consist of a data model, presentation information, and control information. The pattern requires that each of these be separated into different objects.
* The Hierarchical Model View Controller (HMVC) is an evolution of the MVC pattern used for most web applications today. It came about as an answer to the scalability problems apparent within applications which used MVC.

---

## Introducting to NSY Assets Manager

The easiest & best assets manager in history
made with love by Vikry Yuansah

How to use it? Simply follow this.

* First, you need to go to `System/Config/`, there are 1 files, that is `Assets.php`.
* `NSY_AssetManager.php` is the core, it is located in `System/Core` folder. `Assets.php` is the controller which regulates assets, if you want to manage the assets, please go to `Assets.php`.

#### Create `<meta>` tag

```
Add::meta('name', 'content');
```

#### Create `<link>` tag

```
Add::link('filename/url_filename', 'attribute_rel', 'attribute_type');
```

#### Create `<script>` tag

```
Add::script('filename/url_filename', 'attribute_type', 'attribute_charset', 'async defer');
```

#### You can write any html tags with custom method

```
Add::custom('anythings');
```

#### After that, to use it in View, you only need to call the static method name that you created like this

```
method_name();
```

> #### For example :
>
> ```
> header_assets();
> footer_assets();
> ```

---

## PSR-4 Autoloading

NSY applies the concept of PSR-4 Autoloading. NSY has the `composer.json` file that can be dumped with [composer](https://getcomposer.org/download/) command `composer dump-autoload -o` when creating a folder structure that contains new class files.

Complete information about PSR-4 can be read on the official [PHP-FIG](https://www.php-fig.org/psr/psr-4/) website.

---

## NSY CLI (Command Line Interface)

NSY CLI is a collection of commands to facilitate users in operating NSY. To start, open the `terminal` or `git bash` on your project directory, then install it with:

>### Note :
>
>```
>If you install the NSY Framework through >the >`composer create-project`, it >automatically >includes the NSY CLI.
>```

### <ins>NSY CLI Manual Install</ins>

* Open Linux Terminal or Git Bash Terminal inside your project directory.
* `sudo chmod +x INSTALL.sh` (use this if you want to install on a linux operating system that requires permission, or if you are a Windows user, then skip this command).

```
sudo chmod +x INSTALL.sh
```

* `bash INSTALL.sh` or `./INSTALL.sh`.

```
bash INSTALL.sh
```

* Close the `terminal` or `git bash`, & open it again or reset bashrc with the command `source ~/reloader.sh`.

```
source ~/reloader.sh
```

* If NSY CLI installer successfully, it should display.

```
NSY CLI installed
Please close the Terminal & reopen it again
Or
Please reset bashrc with the command 'source ~/reloader.sh'
```

* Then if you type command `nsy --hello` it should display.

```
nsy --hello
```

```
Welcome to NSY CLI
NSY CLI installed successfully
```

### <ins>Example of Commands</ins>

#### Show list of Migration Class file

```
nsy show:migration
```

#### Show list of HMVC Modules directory

```
nsy show:module
```

#### Show list of HMVC Controller files

```
nsy show:controller hmvc <module-directory-name>
```

#### Show list of HMVC Model files

```
nsy show:model hmvc <module-directory-name>
```

#### Show list of MVC Controller files

```
nsy show:controller mvc
```

#### Show list of MVC Model files

```
nsy show:model mvc
```

#### Show welcome message

```
nsy --hello
```

#### Show help message

```
nsy --help
```

#### Dump mysql database

```
nsy dump:mysql <database-name> <username> <password>
```

#### Dump mysql database (table only)

```
nsy dump:mysql <database-name> <username> <password> <table-name>
```

#### Make HMVC Module

```
nsy make:module <module-directory-name>
```

#### Make HMVC Controller

```
nsy make:controller hmvc <module-directory-name> <controller-name>
```

#### Make HMVC Model

```
nsy make:model hmvc <module-directory-name> <model-name>
```

#### Make MVC Controller

```
nsy make:controller mvc <controller-name>
```

#### Make MVC Model

```
nsy make:model mvc <model-name>
```

#### Make Migration Class

```
nsy make:migration <class-name>
```

#### First time setting up NSY

```
nsy --setup
```

#### Generate optimized Composer autoload

```
nsy dump:autoload
```

#### NSY CLI install/update

```
nsy --install
```

#### Make before Middleware Class

```
nsy make:before-middleware <class-name>
```

#### Make after Middleware Class

```
nsy make:after-middleware <class-name>
```

---

## License

The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt)
