

## Security Helper

#### Sanitize element data retrieved from a database or from an HTML form :

```
secure_input('attr_name')
```

#### Sanitize multiple element data retrieved from a database or from an HTML form :

```
secure_form(array('attr_name'))
```

#### Return CSRF Input form with Token :

```
echo csrf_token_form();
```

#### Return only CSRF Token :

```
echo csrf_token();
```

---

## XSS Clean

Sanitizes data so that "Cross Site Scripting" hacks can be prevented. This method does a fair amount of work but it is extremely thorough, designed to prevent even the most obscure XSS attempts. But keep in mind that nothing is ever 100% foolproof.

Note : Should only be used to deal with data upon submission. It's not something that should be used for general runtime processing.
```
anti_xss('value');
```

For more information, https://github.com/voku/anti-xss