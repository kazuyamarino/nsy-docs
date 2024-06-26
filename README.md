# NSY PHP Framework

---

## About

NSY is a simple PHP Framework that works well on MVC or HMVC mode.

Site example :
[https://nsyframework.com/](https://nsyframework.com/).

## Codename

*Talindo*. The traditional West Sulawesi musical instrument Talindo is made from basic materials such as wood, coconut shells and strings. The way to play the Talindo musical instrument is by plucking the strings, then the function of the coconut shell is as a resonance hole. This traditional musical instrument is very popular in the community because it is always present or appears when the harvest season arrives. Not only in West Sulawesi, Talindo is also in Central Sulawesi but has a different name, namely Popondi.

*Wadaya, <http://www.wadaya.rey1024.com/budaya/detail/talindo-tolindo>*.

---

## How to dating with NSY?

## The Requirement

Before installing NSY, there are several applications that must be installed to support NSY operation.

### 1. Install Wget

**Windows Installation :**

* Download Wget from this site [https://eternallybored.org/misc/wget/](https://eternallybored.org/misc/wget/).
* Copy the `wget.exe` file into your `C:\Windows\System32` folder. Simply copy it from one location to the other.
* Verify the Installation on Windows, open the command prompt (cmd.exe) and run `wget -V` to see if it is installed.

**Linux Installation (Debian based) :**

* To install Wget on Linux Ubuntu/Debian use the apt-get command `apt-get install wget`.
* And verify installation with the wget command with the `wget --version` flag.

**MacOS Installation :**

* Install Homebrew, In Terminal type the following command:

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

* Install Wget, In Terminal Type the following command: `brew install wget`.
* Check if Wget is installed open Terminal and type `wget -V`.

### 2. Install Composer

**Windows Installation :**

* Download Composer here, [https://getcomposer.org/doc/00-intro.md#installation-windows](https://getcomposer.org/doc/00-intro.md#installation-windows).
* Run the installer and follow the instructions to install Composer.
* Verify the Installation on Windows, open the command prompt (cmd.exe) and run `composer -V` to see if it is installed.

**Linux Installation (Debian based) :**

* Download the installer and composer setup:

```bash
sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');".
```

* Run the installer:

```bash
sudo php composer-setup.php --install-dir=/usr/bin --filename=composer
```

* Verify the Installation, open Terminal and run `composer -V` to see if it is installed.

**MacOS Installation :**

* Download and install Composer using the following commands:

```bash
curl -sS https://getcomposer.org/installer -o composer-setup.php
```

```bash
HASH="$(curl -sS https://composer.github.io/installer.sig)"
```

```bash
php -r "if (hash_file('sha384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

* If the installer is verified, proceed with the installation:

```bash
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer.
```

* Remove the installer script: `rm composer-setup.php`.
* Check that Composer is installed and accessible: `composer`.

### 3. Install Git

**Windows Installation :**

* Go to the official Git website at [https://git-scm.com/](https://git-scm.com/).
* Click on the `Download` button to get the latest version of Git for Windows.

**Linux Installation (Debian based) :**

* Install Git using the package manager: `sudo apt install git`
* Check the installed Git version: `git --version`

**MacOS Installation :**

* Install Homebrew, In Terminal type the following command:

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

* Once Homebrew is installed, use it to install Git: `brew install git`

* Check the installed Git version: `git --version`

---

## NSY Installation

### Download from Github

* Download source from this link, [https://github.com/kazuyamarino/nsy/releases](https://github.com/kazuyamarino/nsy/releases).
* Simply rename the source folder that has been downloaded to `nsy` & copy it to your `html` or `htdocs` or anythings folder.

For apache, please go to the `docs/apache` folder and read the `Readme.txt`.

```text
// docs/apache/Readme.txt

1. Copy .htaccess inside 'for_public' folder to 'public' folder
2. Copy .htaccess inside 'for_root' folder to 'root(nsy)' folder
```

For nginx, please go to the `docs/nginx` folder and read the `Readme.txt` too.

```text
// docs/nginx/Readme.txt

1. Open 'sudo nano /etc/nginx/sites-enabled/default'
2. Copy the text in the 'default' file and paste it to /etc/nginx/sites-enabled/default
3. And restart nginx service, 'sudo service nginx restart'
```

* Go to the `docs/env.example.php` folder and copy the `env.example.php` to root folder, and rename it to `env.php`.
* And save the date.

### Download from Composer

**1. Install NSY by creating a new directory called blog.**

```sh
composer create-project --prefer-dist vikry/nsy blog
```

**2. Restart Bash.**

```sh
source ~/reloader.sh
```

**3. NSY Setup.**

```sh
cd blog && nsy --setup

Enter directory name >
blog
```

**4. NSY is ready to create project.**

---

## CRUD Example?

Here it is [Vylma CRUD Example](https://vylma.nsyframework.com/)
And [Shyffon CRUD Example](https://shyffon.nsyframework.com/).

---

## Overview

See [OVERVIEW](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md).

* Composer, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#composer).
* Framework Configuration, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#framework-configuration).
* Helpers, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#helpers).
* Routes, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#routes).
* MVC & HMVC, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#mvc--hmvc).
* Introducting to NSY Assets Manager, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#introducting-to-nsy-assets-manager).
* PSR4 Autoloading, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#psr-4-autoloading).
* NSY CLI (Command Line Interface), [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#nsy-cli-command-line-interface).

---

## Features

* Composer, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#composer-on-nsy-framework).
* Simple Routes System, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#routes).
* MVC & HMVC Mode, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#mvc--hmvc).
* Introducting to NSY Assets Manager, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#introducting-to-nsy-assets-manager).
* PSR-4 Autoloading, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#psr-4-autoloading).
* NSY CLI (Command Line Interface)., [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/OVERVIEW.md#nsy-cli-command-line-interface).
* Security Helper, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_SECURITY_FUNCTION.md#security-helper).
* CSRF Token, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_SECURITY_FUNCTION.md#return-csrf-input-form-with-token-).
* XSS Clean, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_SECURITY_FUNCTION.md#xss-clean).
* [NSY Model] NSY Transaction, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MODEL.md#nsy-transaction).
* [NSY Model] Primary and Secondary Database Connection, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MODEL.md#primary--secondary-database-connections).
* [NSY Model] To input multiple data into the database at once in one command, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MODEL.md#multi-insert-multi_insert).
* Razr is a powerful PHP template engine for PHP, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_RAZR.md).
* Migration is like version control for your database, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MIGRATION.md).
* Latitude is a SQL query builder with zero dependencies and a fluent interface, [See Documentation](https://latitude.shadowhand.com/).

---

## NSY Helper Function

### Standar Helper Function

* The PHP superglobals post, deposer and get are used to collect form-data, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#the-php-superglobals-post-deposer-and-get-are-used-to-collect-form-data).
* Returns your site full path public directory, as specified in your config file, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#public-directory-path).
* Return img directory location on the public directory, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#images-directory-url).
* Return js directory location on the public directory, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#javascript-directory-url).
* Return css directory location on the public directory, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#css-directory-url).
* Get version parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-version).
* Get codename parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-codename).
* Get locale parameter value from Config/App.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-language-code).
* Get prefix_attr parameter value from Config/App.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#open-graph-prefix).
* Get sitetitle parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-title).
* Get sitedesc parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-description).
* Get sitekeywords parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-keywords).
* Get siteauthor parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-author).
* Get session_prefix parameter value from Config/App.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-session-prefix).
* Get siteemail parameter value from Config/Site.php, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-site-email).
* Getting Config Value, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#getting-config-value).
* Define an empty variable or a non-empty variable, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#define-an-empty-variable-or-a-non-empty-variable).
* Base URL, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#base-url).
* Simple Ternary, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#simple-ternary).
* Aurora File Export, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#aurora-file-export).
* Get User Agent, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-user-agent).
* Generate Random Number, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#generate-random-number).
* Get URI Segment, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#get-uri-segment).
* Simple string encryption/decryption function, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#simple-string-encryptiondecryption-function).
* Convert image file to base64, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#convert-image-file-to-base64).
* Convert image string to base64, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#convert-image-string-to-base64).
* Convert large positive numbers in to short form, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#convert-large-positive-numbers-in-to-short-form).
* Convert a multi-dimensional array into a single-dimensional array, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#array-flatten).
* Fetch to JSON, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#fetch-to-json).
* PHP Session Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#php-session-library).
* Cookie Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#cookie-library).
* NSY FTP Client Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#nsy-ftp-client-library).
* PHP simple library for managing of data types, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#validate-library).
* PHP library to get language name from code, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#languagecode-method).
* Calculate load time of pages or scripts, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#loadtime-method).
* PHP simple library for managing JSON files, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#json-library).
* PHP Curl Class makes it easy to send HTTP requests and integrate with web APIs, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#curl-library).
* File Library, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_HELPER_FUNCTION.md#file-library).

---

## External Helper Function

* CI helpers, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/CI_HELPER_FUNCTION.md).
* Carbon DateTime, [See Documentation](https://carbon.nesbot.com/docs/).

---

## NSY Middleware

NSY has support middleware, which is the process of filtering a process before it is run by the controller by NSY, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MIDDLEWARE.md).

---

## NSY Migration

Migration is like version control for your database, allowing your team to easily modify and share application database schemes, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MIGRATION.md).

---

## Razr Template Engine

Razr is a powerful PHP template engine for PHP, whose syntax was inspired by ASP.NET Razor.

NSY has supported Razr in the View component. In addition NSY also still supports PHP code in the View component. Either using Razr or PHP, they can run together in one View component, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_RAZR.md).

---

## NSY Security Function

NSY provides security functions including antiXSS and CSRF, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_SECURITY_FUNCTION.md).

---

## NSY Controller

Controllers act as an interface between Model and View components to process all the business logic and incoming requests, manipulate data using the Model component and interact with the Views to render the final output, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_CONTROLLER.md).

---

## NSY Model

The Model component corresponds to all the data-related logic that the user works with. This can represent either the data that is being transferred between the View and Controller components or any other business logic-related data, [See Documentation](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MODEL.md).

---

## License

The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt).

NSY Framework 2019 - 2023.
