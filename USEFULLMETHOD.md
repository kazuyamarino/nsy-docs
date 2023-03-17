# Usefull Function

## NSY Global Function

### The PHP superglobals `post`, `deposer` and `get` are used to collect form-data.

```
post('hello');

// Same as $_POST['hello'];
```

```
get('hello');

// Same as $_GET['hello'];
```

```
deposer(array(some_array));

// Same as $_FILE[ array(some_array) ];
```

### Public directory path :
Returns your site full path `public` directory, as specified in your config file.

```
echo public_path();

// for example
usr/share/../html/nsy/public/
```

### Images directory uri :
Return img directory location on the `public` directory

```
echo img_url();

// for Example
// http://example.com/public/img
```

### Javascript directory uri :
Return js directory location on the `public` directory

```
echo js_url();

// for Example
// http://example.com/public/js
```

### CSS directory uri :
Return css directory location on the `public` directory

```
echo css_url();

// for Example
// http://example.com/public/css
```

### Get Version :
Get `version` parameter value from Config/Site.php.

```
echo get_version();

// 3.0.0
```

### Get Codename :
Get `codename` parameter value from Config/Site.php.

```
echo get_codename();

// Tifa
```

### Get Language Code :
Get `locale` parameter value from Config/App.php.

```
echo get_lang_code();

// en
```

### Open Graph Prefix :
Get `prefix_attr` parameter value from Config/App.php.

```
echo get_og_prefix();
```

### Get Site Title :
Get `sitetitle` parameter value from Config/Site.php.

```
echo get_title();
```

### Get Site Description :
Get `sitedesc` parameter value from Config/Site.php.

```
echo get_desc();
```

### Get Site Keywords :
Get `sitekeywords` parameter value from Config/Site.php.

```
echo get_keywords();
```

### Get Site Author :
Get `siteauthor` parameter value from Config/Site.php.

```
echo get_author();
```

### Get Session Prefix :
Get `session_prefix` parameter value from Config/App.php.

```
echo get_session_prefix();
```

### Get Site Email :
Get `siteemail` parameter value from Config/Site.php.

```
echo get_site_email();
```

### Get Site Email :
Get `siteemail` parameter value from Config/Site.php.

```
echo get_site_email();
```

---

## Base URL
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