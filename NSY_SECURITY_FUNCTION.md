# Security Helper

---

## Secure Input

Sanitize element data retrieved from a database or from an HTML form.

```php
secure_input('attr_name');
```

**Example :**

```php
<form>
    <label for="fname">First name:</label><br>
    <input type="text" id="fname" name="fname"><br>
    <label for="lname">Last name:</label><br>
    <input type="text" id="lname" name="lname">
</form>

---

secure_input('fname');
secure_input('lname');

```

## Secure Form

Sanitize multiple element data retrieved from a database or from an HTML form.

```php
secure_form(array('attr_name'))
```

**Example :**

```php
<form>
    <label for="fname">First name:</label><br>
    <input type="text" id="fname" name="fname"><br>
    <label for="lname">Last name:</label><br>
    <input type="text" id="lname" name="lname">
</form>

---

secure_form(['fname', 'lname']);

```

## CSRF Token Form

Return a CSRF Input form with a randomly generated token.

```php
echo csrf_token_form();
```

## CSRF Token

Return randomly generated token only.

```php
echo csrf_token();
```

## XSS Clean

Sanitizes data so that "Cross Site Scripting" hacks can be prevented. This method does a fair amount of work but it is extremely thorough, designed to prevent even the most obscure XSS attempts. But keep in mind that nothing is ever 100% foolproof.

Note : Should only be used to deal with data upon submission. It's not something that should be used for general runtime processing.

```php
anti_xss('value');
```

For more information, [https://github.com/voku/anti-xss]
