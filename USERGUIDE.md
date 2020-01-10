# NSY USER GUIDE
NSY is a simple PHP Framework that works well on MVC or HMVC mode.

Site example :
<a href="https://nsy.kazuyamarino.com/" target="_blank">https://nsy.kazuyamarino.com/</a>

### Composer
Composer helps you declare, manage, and install dependencies of PHP projects.

See [https://getcomposer.org/](https://getcomposer.org/) for more information and documentation.

Installation / Usage
--------------------

Download and install Composer by following the [official instructions](https://getcomposer.org/download/).

For usage, see [the documentation](https://getcomposer.org/doc/).

Packages
--------

Find packages on [Packagist](https://packagist.org).

Composer on NSY framework
-------------------------

The composer on the nsy framework has a function to generate autoload in the HMVC module folder.

NSY applies the concept of PSR-4 Autoloading. NSY has the `composer.json` file that can be dumped with [composer](https://getcomposer.org/download/) command `composer dump-autoload -o` or [NSY CLI](https://github.com/kazuyamarino/nsy/blob/master/docs/USERGUIDE.md#nsy-cli-command-line) command `nsy dump:autoload` when creating a folder structure that contains new class files.

For example,
* There is an example folder in the module folder that was created named `homepage`, along with the namespaces.

* In the `homepage` folder there must be a `models` folder, `views` folder, and `controllers` folder.

```
modules
    │   └── homepage
    │       ├── controllers
    │       │  
    │       ├── models
    │       │  
    │       └── views
    │           
```

Should be like this. That it is!

* Now, you can generate autoload class in the `models` folder & `controllers` folder for the `homepage` with `composer dump-autoload -o` or [NSY CLI](https://github.com/kazuyamarino/nsy/blob/master/docs/USERGUIDE.md#nsy-cli-command-line) command `nsy dump:autoload` on the command line terminal.

<hr>

### Framework Configuration
The NSY_Framework Configuration is very simple. There are 3 config file in `system/config` directory :
* `App.php` for application setting such as system path of the framework.
* `Database.php` for database connection setting.
* `Site.php` for meta site configuration.

```
├── config
    │   ├── App.php
    │   ├── Database.php
    │   └── Site.php
```

By default NSY support `phpdotenv` library, that can read `env` file *(see `env` file on root directory)*.

* system.js file

>system.js is located in `public/js/config/system.js` folder.

In system.js there is a `base_url` configuration for javascript *(see line 1 to 20)*. This `base_url` is used for the purpose of initializing the function of the <strong>Datatable Ajax URL</strong> in the `public/js/datatables/init.js`*

(*) For Example see Shyffon repository [https://github.com/kazuyamarino/shyffon](Here!)

<hr>

### Helpers
The `system/helpers` folder is useful for creating custom methods that match what you want and need.

There is a helper files that are by default available in NSY, namely `Helpers_CI`. `Helpers_CI` are a set of `Codeigniter` built-in helper (there are only a few) methods that can run on NSY.

If you want to make your own helper, then just make the desired method in the php file then save it in system/helpers. And don't forget to autoload it on `composer.json` in the parameters `files`.

```
"autoload": {
	"psr-4": {
		"System\\": "system/"
	},
	"files": [
		"system/helpers/Helpers_CI.php"
		"system/helpers/Custom_Method.php" // your custom helpers file
	]
}
```

<hr>

### Routes
NSY Routing system using classes from [Macaw route by Noah Buscher](https://github.com/noahbuscher/macaw), and it's located in the `system/routes` directory.

```
├── routes
    │   ├── Api.php
    │   └── Web.php
```

>Macaw is a simple, open source PHP router. It's super small (~150 LOC), fast, and has some great >annotated source code. This class allows you to just throw it into your project and start using it >immediately.

#### Examples :

```PHP
Route::get('/', function() {
  echo 'Hello world!';
});

Route::dispatch();
```

Route also supports lambda URIs, such as:

```PHP
Route::get('/(:any)', function($slug) {
  echo 'The slug is: ' . $slug;
});

Route::dispatch();
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

#### Example passing to a controller instead of a closure :

It's possible to pass the namespace path to a controller instead of the closure:

For this demo lets say I have a folder called controllers with a demo.php

index.php:

```php
Route::get('/', 'Controllers\demo@index');
Route::get('page', 'Controllers\demo@page');
Route::get('view/(:num)', 'Controllers\demo@view');
```

demo.php:

```php
<?php
namespace controllers;

class Demo {

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

Lastly, if there is no route defined for a certain location, you can make NSY_Router run a custom callback, like:

```PHP
Route::error(function() {
  echo '404 :: Not Found';
});
```

If you don't specify an error callback, NSY_Router will just echo `404`.

<hr>

## MVC & HMVC
* The Model View Controller (MVC) design pattern specifies that an application consist of a data model, presentation information, and control information. The pattern requires that each of these be separated into different objects.
* The Hierarchical Model View Controller (HMVC) is an evolution of the MVC pattern used for most web applications today. It came about as an answer to the scalability problems apparent within applications which used MVC.

<hr>

## Introducting to NSY Assets Manager
The easiest & best assets manager in history
made with love by Vikry Yuansah

How to use it? Simply follow this.
* First, you need to go to `system/libraries/`, there are 1 files, that is `Assets.php`.
* `NSY_AssetManager.php` is the core, it is located in `system/core` folder. `Assets.php` is the controller which regulates assets, if you want to manage the assets, please go to `Assets.php`.

Create `<meta>` tag :

```
Add::meta('name', 'content');
```

Create `<link>` tag :

```
Add::link('filename/url_filename', 'attribute_rel', 'attribute_type');
```

Create `<script>` tag :

```
Add::script('filename/url_filename', 'attribute_type', 'attribute_charset', 'async defer');
```

You can write any html tags with custom method :

```
Add::custom('anythings');
```

* After that, to use it in View, you only need to call the static method name that you created like this.

```
Pull::method_name();
```

For example :

```
Pull::header_assets();
Pull::footer_assets();
```

<hr>

## PSR-4 Autoloading
* NSY applies the concept of PSR-4 Autoloading. NSY has the `composer.json` file that can be dumped with [composer](https://getcomposer.org/download/) command `composer dump-autoload -o` when creating a folder structure that contains new class files.
* Complete information about PSR-4 can be read on the official [PHP-FIG](https://www.php-fig.org/psr/psr-4/) website.

<hr>

## NSY CLI (Command Line)
NSY CLI is a collection of commands to facilitate users in operating NSY. To start, open the `terminal` or `git bash` on your project directory, then install it with:

---

### Note
If you install the NSY Framework through the `composer create-project`, it automatically includes the NSY CLI.

---

### NSY CLI Manual Install
* Open Linux Terminal or Git Bash Terminal inside your project directory.
* `sudo chmod +x INSTALL.sh` (use this if you want to install on a linux operating system that requires permission, or if you are a Windows user, then skip this command).

```
html/nsy$ sudo chmod +x INSTALL.sh
```

* `bash INSTALL.sh` or `./INSTALL.sh`.

```
html/nsy$ bash INSTALL.sh
```

* Close the `terminal` or `git bash`, & open it again or reset bashrc with the command `source ~/reloader.sh`.

```
html/nsy$ source ~/reloader.sh
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
html/nsy$ nsy --hello
```

```
Welcome to NSY CLI
NSY CLI installed successfully
```

For example of commands see below.
* Show list of Migration Class file :

```
nsy show:migration
```

* Show list of HMVC Modules directory :

```
nsy show:module
```

* Show list of HMVC Controller files :

```
nsy show:controller hmvc <module-directory-name>
```

* Show list of HMVC Model files :

```
nsy show:model hmvc <module-directory-name>
```

* Show list of MVC Controller files :

```
nsy show:controller mvc
```

* Show list of MVC Model files :

```
nsy show:model mvc
```

* Show Welcome Message :

```
nsy --hello
```

* Show Help Message :

```
nsy --help
```

* Dump mysql database :

```
nsy dump:mysql <database-name> <username> <password>
```

* Dump mysql database (table only) :

```
nsy dump:mysql <database-name> <username> <password> <table-name>
```

* Make HMVC Module :

```
nsy make:module <module-directory-name>
```

* Make HMVC Controller :

```
nsy make:controller hmvc <module-directory-name> <controller-name>
```

* Make HMVC Model :

```
nsy make:model hmvc <module-directory-name> <model-name>
```

* Make MVC Controller :

```
nsy make:controller mvc <controller-name>
```

* Make MVC Model :

```
nsy make:model mvc <model-name>
```

* Make Migration Class :

```
nsy make:migration <class-name>
```

* First time setting up NSY :

```
nsy --setup
```

* Generate optimized composer autoload :

```
nsy dump:autoload
```

* NSY CLI install/update :

```
nsy --install
```

<hr>

## License
The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt)