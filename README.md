# NSY PHP Framework
## <ins>About</ins>
NSY is a simple PHP Framework that works well on MVC or HMVC mode.

[![Build Status](https://travis-ci.org/kazuyamarino/nsy.svg?branch=master)](https://travis-ci.org/kazuyamarino/nsy)

Site example :
[https://nsyframework.com/](https://nsyframework.com/)

## <ins>Codename</ins>
The Sasando, also called Sasandu from Sandu or Sanu, is a tube zither, a harp-like traditional music string instrument native to Rote Island of East Nusa Tenggara, Indonesia.
*Wikipedia - https://en.wikipedia.org/wiki/Sasando*

---

# How to dating with NSY?
## <ins>Download from Github</ins>
* Download source from this link [https://github.com/kazuyamarino/nsy/releases](https://github.com/kazuyamarino/nsy/releases).
* Simply rename the source folder that has been downloaded to `nsy` & copy it to your `html` or `htdocs` or anythings folder.
* For apache, please go to the `docs/apache` folder and read the `Readme.txt`.

```
// Apache Readme.txt

1. Copy .htaccess inside 'for_public' folder to 'public' folder
2. Copy .htaccess inside 'for_root' folder to 'root(nsy)' folder
```

* Go to the `docs/env.example.php` folder and copy the `env.example.php` to root folder, and rename it to `env.php`.
* And save the date..

## <ins>From Composer</ins>

#### 1. Install NSY by creating a new directory called `blog`

```
composer create-project --prefer-dist vikry/nsy blog
```

#### 2. Restart Bash

```
source ~/reloader.sh
```

#### 3. NSY Setup

```
cd blog && nsy --setup

Enter directory name >
blog
```

#### 4. NSY is Ready to create project!

__Note :__
```For nginx, please go to the `docs/nginx` folder and read the `Readme.txt` too.```

```
// Nginx Readme.txt

1. Open 'sudo nano /etc/nginx/sites-enabled/default'
2. Copy the text in the 'default' file and paste it to /etc/nginx/sites-enabled/default
3. And restart nginx service, 'sudo service nginx restart'
```

---

# CRUD Example?
Here it is [Vylma CRUD Example](https://vylma.nsyframework.com/)
And [Shyffon CRUD Example](https://shyffon.nsyframework.com/)

---

# User Guide :
See [USERGUIDE.md](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md).
* Composer, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#composer)
* Composer on NSY, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#composer-on-nsy-framework)
* Framework Configuration, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#framework-configuration)
* Helpers, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#helpers)
* Routes, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#routes)
* MVC & HMVC, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#mvc--hmvc)
* Introducting to NSY Assets Manager, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#introducting-to-nsy-assets-manager)
* PSR4 Autoloading, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#psr-4-autoloading)
* NSY CLI (Command Line), [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#nsy-cli-command-line)

---

# NSY Features :
* Composer, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#composer-on-nsy-framework)
* NSY Routing System, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#routes)
* MVC or HMVC, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#mvc--hmvc)
* NSY Assets Manager, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#introducting-to-nsy-assets-manager)
* PSR-4 Autoloading, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#psr-4-autoloading)
* NSY CLI (Command Line), [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md#nsy-cli-command-line)
* Anti XSS & CSRF Token, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#security-helper)
* Primary and Secondary Database Connection, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#primary--secondary-database-connections)
* Aurora File Export, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#aurora-file-export)
* FTP Client, See [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#nsy-ftp-client-library)
* ImageResize Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#imageresize-library)
* Carbon DateTime, [See Documentation](https://carbon.nesbot.com/docs/)
* NSY Database Migrations, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#nsy-migrations)
* Razr Template Engine, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#razr---the-powerful-php-template-engine)
* Middleware, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#the-middlewares)

---

# System Guide :
See [System Guide.md](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md).
* Using Controllers, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#the-controllers)
* Using Models, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#the-models)
* NSY Transaction, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#nsy-transaction)
* Razr - The powerful PHP template engine, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#razr---the-powerful-php-template-engine)
* NSY Migrations, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#nsy-migrations)
* The Middlewares, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md#the-middlewares)
* Usefull Method, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#usefull-method).<br/>
    * The PHP superglobals post and get are used to collect form-data, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#the-php-superglobals-post-and-get-are-used-to-collect-form-data)
    * Check if it's a PUT request, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#check-if-its-a-put-request-)
    * Check if it's a DELETE request, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#check-if-its-a-delete-request-)
    * Check if it's a GET request, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#check-if-its-a-get-request-)
    * Check if it's a POST request, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#check-if-its-a-post-request-)
    * Get request content type, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-request-content-type-)
    * Parse array data from request method, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#parse-array-data-from-request-method-)
    * Parse object data from request method, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#parse-object-data-from-request-method-)
    * Get data from request method and parse to json, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-data-from-request-method-and-parse-to-json-)
    * Get data from request method and parse to string, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-data-from-request-method-and-parse-to-string-)
    * Get data from request method and parse to integer, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-data-from-request-method-and-parse-to-integer-)
    * Get data from request method and parse to float, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-data-from-request-method-and-parse-to-float-)
    * Get data from request method and parse to boolean, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-data-from-request-method-and-parse-to-boolean-)
    * Get data from request method and parse to ip, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-data-from-request-method-and-parse-to-ip-)
    * Get data from request method and parse to url, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-data-from-request-method-and-parse-to-url-)
    * Get data from request method and parse to email, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-data-from-request-method-and-parse-to-email-)
    * Public directory path, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#public-directory-path)
    * Images directory uri, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#images-directory-uri)
    * Javascript directory uri, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#javascript-directory-uri)
    * CSS directory uri, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#css-directory-uri)
    * Get Version, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-version)
    * Get Codename, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-codename)
    * Get Language Code, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-language-code)
    * Open Graph Prefix, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#open-graph-prefix)
    * Get Site Title, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-site-title)
    * Get Site Description, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-site-description)
    * Get Site Keywords, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-site-keywords)
    * Get Site Author, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-site-author)
    * Get Session Prefix, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-session-prefix)
    * Get Site Email, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-site-email)
* Base URL, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#base-url)
* Array Flatten, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#array-flatten)
* Fetch to JSON, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#fetch-to-json)
* Getting Config Value, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#getting-config-value)
* Security helper, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#security-helper)
* Get URI Segment, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-uri-segment)
* Generate Random Number, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#generate-random-number)
* PHP SESSION, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#php-session)
* Cookie Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#cookie-library)
* Simple Ternary, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#simple-ternary)
* Specify an empty variable or not, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#specify-an-empty-variable-or-not)
* Get User Agent, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#get-user-agent)
* Aurora File Export, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#aurora-file-export)
* NSY FTP Client Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#nsy-ftp-client-library)
* ImageResize Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#imageresize-library)
* Carbon Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#carbon-library)
* String Method, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#string-method)
* LanguageCode Method, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#languagecode-method)
* LoadTime Method, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#loadtime-method)
* Json Method, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#json-method)
* Curl Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#curl-library)
* File Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#file-library)
* IP Method, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#ip-method)
* Validate Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#validate-library)
* CI helpers, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md#ci-helpers)

---

# License
The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt)

NSY Framework 2020 - 2023
