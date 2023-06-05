# NSY PHP Framework
## <ins>About</ins>
NSY is a simple PHP Framework that works well on MVC or HMVC mode.

Site example :
[https://nsyframework.com/](https://nsyframework.com/)

## <ins>Codename</ins>
Lalove is a traditional musical instrument that is blown and comes from Central Sulawesi. The function of this musical instrument is to accompany dances from the Central Sulawesi region or certain customs. The shape is shaped like a long flute musical instrument.
*Kementerian Pendidikan, Kebudayaan, Riset, dan Teknologi - https://ayoguruberbagi.kemdikbud.go.id/artikel/melestarikan-alat-musik-tradisional/#:~:text=Lalove%20termasuk%20alat%20musik%20tradisional,alat%20musik%20Suling%20yang%20panjang.*

---

# How to dating with NSY?
## <ins>Download from Github</ins>
* Download source from this link [https://github.com/kazuyamarino/nsy/releases](https://github.com/kazuyamarino/nsy/releases).
* Simply rename the source folder that has been downloaded to `nsy` & copy it to your `html` or `htdocs` or anythings folder.

```For apache, please go to the `docs/apache` folder and read the `Readme.txt`.```
```
// docs/apache/Readme.txt

1. Copy .htaccess inside 'for_public' folder to 'public' folder
2. Copy .htaccess inside 'for_root' folder to 'root(nsy)' folder
```

```For nginx, please go to the `docs/nginx` folder and read the `Readme.txt` too.```
```
// docs/nginx/Readme.txt

1. Open 'sudo nano /etc/nginx/sites-enabled/default'
2. Copy the text in the 'default' file and paste it to /etc/nginx/sites-enabled/default
3. And restart nginx service, 'sudo service nginx restart'
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

#### 4. NSY is ready to create project!

---

# CRUD Example?
Here it is [Vylma CRUD Example](https://vylma.nsyframework.com/)
And [Shyffon CRUD Example](https://shyffon.nsyframework.com/)

---

# Overview :
See [OVERVIEW.md](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md).
* Composer, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#composer)
* Framework Configuration, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#framework-configuration)
* Helpers, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#helpers)
* Routes, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#routes)
* MVC & HMVC, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#mvc--hmvc)
* Introducting to NSY Assets Manager, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#introducting-to-nsy-assets-manager)
* PSR4 Autoloading, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#psr-4-autoloading)
* NSY CLI (Command Line Interface), [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#nsy-cli-command-line-interface)

---

# Features :
* Composer, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#composer-on-nsy-framework)
* Simple Routes System, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#routes)
* MVC & HMVC Mode, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#mvc--hmvc)
* Introducting to NSY Assets Manager, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#introducting-to-nsy-assets-manager)
* PSR-4 Autoloading, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#psr-4-autoloading)
* NSY CLI (Command Line Interface), [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#nsy-cli-command-line-interface)
* Security Helper, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_SECURITY_FUNCTION.md#security-helper)
* CSRF Token, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_SECURITY_FUNCTION.md#return-csrf-input-form-with-token-)
* XSS Clean, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_SECURITY_FUNCTION.md#xss-clean)
* [NSY Model] NSY Transaction, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MODEL.md#nsy-transaction)
* [NSY Model] Primary and Secondary Database Connection, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MODEL.md#primary--secondary-database-connections)
* [NSY Model] To input multiple data into the database at once in one command, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MODEL.md#multi-insert-multi_insert)
* Razr is a powerful PHP template engine for PHP, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_RAZR.md)
* Migration is like version control for your database, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MIGRATION.md)

---

# NSY Helper Function :

## Standar Helper Function
* The PHP superglobals post, deposer and get are used to collect form-data, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#the-php-superglobals-post-deposer-and-get-are-used-to-collect-form-data)
* Returns your site full path public directory, as specified in your config file, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#public-directory-path)
* Return img directory location on the public directory, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#images-directory-uri)
* Return js directory location on the public directory, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#javascript-directory-uri)
* Return css directory location on the public directory, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#css-directory-uri)
* Get version parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-version)
* Get codename parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-codename)
* Get locale parameter value from Config/App.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-language-code)
* Get prefix_attr parameter value from Config/App.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#open-graph-prefix)
* Get sitetitle parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-title)
* Get sitedesc parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-description)
* Get sitekeywords parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-keywords)
* Get siteauthor parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-author)
* Get session_prefix parameter value from Config/App.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-session-prefix)
* Get siteemail parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-email)
* Getting Config Value, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#getting-config-value)
* Define an empty variable or a non-empty variable, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#define-an-empty-variable-or-a-non-empty-variable)
* Base URL, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#base-url)
* Simple Ternary, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#simple-ternary)
* Aurora File Export, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#aurora-file-export)
* Get User Agent, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-user-agent)
* Generate Random Number, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#generate-random-number)
* Get URI Segment, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-uri-segment)
* Simple string encryption/decryption function, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#simple-string-encryptiondecryption-function)
* Convert image file to base64, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#convert-image-file-to-base64)
* Convert image string to base64, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#convert-image-string-to-base64)
* Convert large positive numbers in to short form, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#convert-large-positive-numbers-in-to-short-form)
* Convert a multi-dimensional array into a single-dimensional array, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#array-flatten)
* Fetch to JSON, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#fetch-to-json)
* PHP Session Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#php-session-library)
* Cookie Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#cookie-library)
* NSY FTP Client Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#nsy-ftp-client-library)
* PHP simple library for managing of data types, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#validate-library)
* PHP library to get language name from code, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#languagecode-method)
* Calculate load time of pages or scripts, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#loadtime-method)
* PHP simple library for managing JSON files, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#json-library)
* PHP Curl Class makes it easy to send HTTP requests and integrate with web APIs, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#curl-library)
* File Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#file-library)

---

# External Helper Function :

* CI helpers, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/CI_HELPER_FUNCTION.md)
* Carbon DateTime, [See Documentation](https://carbon.nesbot.com/docs/)

---

# NSY Middleware

NSY has support middleware, which is the process of filtering a process before it is run by the controller by NSY, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MIDDLEWARE.md)

---
# NSY Migration

Migration is like version control for your database, allowing your team to easily modify and share application database schemes, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MIGRATION.md)

---

# Razr Template Engine

Razr is a powerful PHP template engine for PHP, whose syntax was inspired by ASP.NET Razor.

NSY has supported Razr in the View component. In addition NSY also still supports PHP code in the View component. Either using Razr or PHP, they can run together in one View component, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_RAZR.md)

---

# NSY Security Function

NSY provides security functions including antiXSS and CSRF, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_SECURITY_FUNCTION.md)

---

# NSY Controller

Controllers act as an interface between Model and View components to process all the business logic and incoming requests, manipulate data using the Model component and interact with the Views to render the final output, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_CONTROLLER.md)

---

# NSY Model

The Model component corresponds to all the data-related logic that the user works with. This can represent either the data that is being transferred between the View and Controller components or any other business logic-related data, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MODEL.md)

---

# License
The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt)

NSY Framework 2019 - 2023
