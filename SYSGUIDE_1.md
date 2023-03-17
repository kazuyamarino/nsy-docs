

## Security helper
### For filtering input value :

```
secure_input('attr_name')
```

### Get CSRF Token on form :

```
echo form_csrf_token();
```

### Get CSRF Token/Only Token :

```
echo csrf_token();
```

### Filtering variable from XSS :

```
xss_filter('value');
```

### Allow http :

```
allow_http();
```

### Disallow http :

```
disallow_http();
```

### Remove get parameter :

```
remove_get_parameters('url');
```