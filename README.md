# NSY
NSY is a simple PHP Framework that works well on MVC or HMVC mode.

[![Build Status](https://travis-ci.org/kazuyamarino/nsy.svg?branch=master)](https://travis-ci.org/kazuyamarino/nsy)

Site example :
[https://nsy.kazuyamarino.com/](https://nsy.kazuyamarino.com/)

## Codename
Tifa is a musical instrument typical of Eastern Indonesia, especially Maluku and Papua. This instrument looks like a drum and is made of wood with a hole in the middle. *Wikipedia - https://id.wikipedia.org/wiki/Tifa*

## How to dating with NSY?
### Download from Github
* Download source from this link [https://github.com/kazuyamarino/nsy/releases](https://github.com/kazuyamarino/nsy/releases).
* Simply rename the source folder that has been downloaded to `nsy` & copy it to your `html` or `htdocs` or anythings folder.
* For apache, please go to the `docs/apache` folder and read the `Readme.txt`.

```
// Apache Readme.txt
1. Copy .htaccess inside 'for_public' folder to 'public' folder
2. Copy .htaccess inside 'for_root' folder to 'root(nsy)' folder
```

* Go to the `docs/env.example` folder and copy the `env.example` to root folder, and rename it to `env`.
* And save the date..

### From Composer

### Install NSY by creating a new directory called `blog`

```
composer create-project --prefer-dist vikry/nsy blog
```

##### 2. Restart Bash

```
source ~/reloader.sh
```

##### 3. NSY Setup

```
cd blog && nsy --setup

Enter directory name >
blog
```

---

**Note :**
For nginx, please go to the `docs/nginx` folder and read the `Readme.txt` too.

```
// Nginx Readme.txt
1. Open 'sudo nano /etc/nginx/sites-enabled/default'
2. Copy the text in the 'default' file and paste it to /etc/nginx/sites-enabled/default
3. And restart nginx service, 'sudo service nginx restart'
```

---

## CRUD Example?
Here it is [Vylma CRUD Example](https://vylma.kazuyamarino.com/)
And [Shyffon CRUD Example](https://shyffon.kazuyamarino.com/)


## NSY Features :
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

## User Guide.
See [USERGUIDE.md](https://github.com/kazuyamarino/nsy-docs/blob/master/USERGUIDE.md).


## System Guide.
* Part 1 of [SYSGUIDE.md](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_1.md).<br/>
* Part 2 of [SYSGUIDE.md](https://github.com/kazuyamarino/nsy-docs/blob/master/SYSGUIDE_2.md).


## License
The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt)
