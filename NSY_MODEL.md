# NSY Models

---

## Primary & Secondary Database Connections

NSY supports multiple database connections in one running application.

You can see the `env` in root directory. There seems to be a configuration like this :

```php
// Primary connection
'primary' => [
    'CONNECTION_NAME' => 'primary',
    'DB_CONNECTION' => '',
    'DB_HOST' => '',
    'DB_PORT' => '',
    'DB_NAME' => '',
    'DB_USER' => '',
    'DB_PASS' => '',
    'DB_CHARSET' => '',
    'DB_PREFIX' => '',
    'DB_ATTR' => [
        \PDO::ATTR_ERRMODE => \PDO::ERRMODE_WARNING
    ]
],

// Secondary connection
'secondary' => [
    'CONNECTION_NAME' => 'secondary',
    'DB_CONNECTION' => '',
    'DB_HOST' => '',
    'DB_PORT' => '',
    'DB_NAME' => '',
    'DB_USER' => '',
    'DB_PASS' => '',
    'DB_CHARSET' => '',
    'DB_PREFIX' => '',
    'DB_ATTR' => [
        \PDO::ATTR_ERRMODE => \PDO::ERRMODE_WARNING
    ]
],
```

**Example for defining Primary & Secondary Connection :**

```php
'primary' => [
    'CONNECTION_NAME' => 'primary',
    'DB_CONNECTION' => 'mysql',
    'DB_HOST' => 'localhost',
    'DB_PORT' => '3306',
    'DB_NAME' => 'dev_example',
    'DB_USER' => 'root',
    'DB_PASS' => 'password',
    'DB_CHARSET' => 'UTF8',
    'DB_PREFIX' => '',
    'DB_ATTR' => [
        \PDO::ATTR_ERRMODE => \PDO::ERRMODE_WARNING
    ]
],

'secondary' => [
    'CONNECTION_NAME' => 'secondary',
    'DB_CONNECTION' => 'mysql',
    'DB_HOST' => 'localhost',
    'DB_PORT' => '3306',
    'DB_NAME' => 'dev_example_secondary',
    'DB_USER' => 'root_secondary',
    'DB_PASS' => 'password_secondary',
    'DB_CHARSET' => 'UTF8',
    'DB_PREFIX' => '',
    'DB_ATTR' => [
        \PDO::ATTR_ERRMODE => \PDO::ERRMODE_WARNING
    ]
],
```

From your model if you want to run sql query on `primary` database connection, then below is way to show how to call query with `primary` connection :

```php
$q = 'SELECT * FROM blabla';
DB::connect()->query($q)->vars()->bind()->style()->fetch_all();
```

Then, if you want to run sql query on the `secondary` database connection :

```php
$q = 'SELECT * FROM blabla';
DB::connect('secondary')->query($q)->vars()->bind()->style()->fetch_all();
```

The `secondary` name is taken from the name `CONNECTION_NAME` from the database connection configuration.
If you have a connection name for example `amazon_aws`, then you should call it by that name.

```php
$q = 'SELECT * FROM blabla';
DB::connect('amazon_aws')->query($q)->vars()->bind()->style()->fetch_all();
```

---

## Getting Data Out of Statement in Dozens Different Formats | `fetch_all()`

That's most interesting function, with most astonishing features. Mostly thanks to its existence one can call PDO a wrapper, as this function can automate many operations otherwise performed manually.

`fetch_all()` returns an array that consists of all the rows returned by the query. From this fact we can make two conclusions:

This function should not be used, if many rows has been selected. In such a case conventional while loop ave to be used, fetching rows one by one instead of getting them all into array at once. "Many" means more than it is suitable to be shown on the average web page.

This function is mostly useful in a modern web application that never outputs data right away during fetching, but rather passes it to template.
You'd be amazed, in how many different formats this function can return data in (and how little an average PHP user knows of them), all controlled by `FETCH...` variables. Some of them are: `FETCH_NUM, FETCH_ASSOC, FETCH_BOTH, FETCH_CLASS, FETCH_KEY_PAIR, FETCH_UNIQUE, FETCH_GROUP, and FETCH_FUNC`.

### Getting a plain array

By default, this function will return just simple enumerated array consists of all the returned rows. Row formatting constants, such as `FETCH_NUM, FETCH_ASSOC, FETCH_COLUMN` etc can change the row format.

```php
$q = 'SELECT id, name, username FROM users';
$d = DB::connect()->query($q)->vars()->style(FETCH_ASSOC)->fetch_all();

print_r($d);
```

it will return this,

```php
Array
(
    [0] => Array
        (
            [id] => 1
            [name] => Vikry Yuansah
            [user_name] => vikry
        )
)
```

### Getting a column number

It is often very handy to get plain one-dimensional array right out of the query, if only one column out of many rows being fetched. Here you go :

```php
$q = 'SELECT name FROM users';
$d = DB::connect()->query($q)->vars()->style(FETCH_COLUMN)->fetch_all();

print_r($d);
```

it will return this,

```php
Array
(
    [0] => Vikry Yuansah
)
```

### Getting key-value pairs

Also extremely useful format, when we need to get the same column, but indexed not by numbers in order but by another field. Here goes `FETCH_KEY_PAIR` constant :

```php
$q = 'SELECT name FROM users';
$d = DB::connect()->query($q)->vars()->style(FETCH_KEY_PAIR)->fetch_all();

print_r($d);
```

it will return this,

```php
Array
(
    [1] => Vikry Yuansah
    [2] => Nayla Syifa
)
```

and many other modes in fetch_all.

---

## Getting Data Out of Statement | `fetch()`

It fetches a single row from database, and moves the internal pointer in the result set, so consequent calls to this function will return all the resulting rows one by one.

```php
$q = 'SELECT id, name FROM users';
$d = DB::connect()->query($q)->vars()->style(FETCH_NUM)->fetch();

print_r($d);
```

it will return this,

```php
Array
(
    [0] => 1
    [1] => Vikry Yuansah
)
```

Another way would be to bind these variables explicitly while setting the proper param type.

Binds a PHP variable to a corresponding named or question mark placeholder in the SQL statement that was used to prepare the statement.

BindValue with PARAM_INT (Defines variable type as integer/number) :

```php
$id = [ ':id' => [3, PAR_INT] ];

$q = "SELECT id, name, user_name FROM tbl_users WHERE id = :id";
$d = DB::connect()->query($q)->vars($id)->bind(BINDVAL)->fetch();

print_r($d);
```

it will return this,

```php
Array
(
    [id] => 3
    [0] => 3
    [name] => Tialuna
    [1] => Tialuna
    [user_name] => tia
    [2] => tia
)
```

BindParam with PARAM_STR (Defines the variable type as a text string) :

```php
$string = [ ':name' => ['%yuan%', PAR_STR] ];

$q = "SELECT id, name, user_name FROM tbl_users WHERE name LIKE :name";
$d = DB::connect()->query($q)->vars($string)->bind(BINDPAR)->fetch();

print_r($d);
```

it will return this,

```php
Array
(
    [id] => 1
    [0] => 1
    [name] => Vikry Yuansah
    [1] => Vikry Yuansah
    [user_name] => vikry
    [2] => vikry
)
```

Unlike `BINDVAL`, the variable is bound as a reference and will only be evaluated at the time that `exec()` is called.

`BINDPAR` to bind PHP variables to the parameter markers: bound variables pass their value as input and receive the output value, if any, of their associated parameter markers.

---

## Getting Data Out of Statement |`fetch_column()`

A neat helper function that returns value of the single field of returned row. Very handy when we are selecting only one field :

```php
// Getting the name based on id
$id = [ ':id' => 2 ];

$q = "SELECT name FROM tbl_users WHERE id = :id";
$d = DB::connect()->query($q)->vars($id)->bind()->style(FETCH_ASSOC)->fetch_column();

return $d;
```

it will return this,

```text
Nayla Syifa
```

```php
// getting number of rows in the table utilizing method chaining
$q = "SELECT count(*) FROM tbl_users";
$d = DB::connect()->query($q)->vars()->style(FETCH_ASSOC)->fetch_column();

return $d;
```

will return this,

```php
3 => number of row data
```

---

## Getting Row Count | `row_count()`

NSY uses PDO. PDO offers a function for returning the number of rows found by the query, `row_count()`, for example :

```php
$q = "SELECT * FROM tbl_users";
$d = DB::connect()->query($q)->vars()->row_count();

return $d->result;
```

it will return,

```php
3 => number of row data
```

However, if you want to get the number of affected rows, here is an example :

```php
$id = [ ':id' => 2 ];

$q = "DELETE FROM tbl_users WHERE id = :id";
$deleted_data = DB::connect()->query($q)->vars($id)->bind()->row_count();

return deleted_data->result;
```

Result,

```php
1 => number of row data that was deleted
```

---

## Executes a Prepared Statement | `exec()`

### Update data

```php
$id = [ ':id' => 2 ];

$q = "UPDATE tbl_users SET name = :name WHERE id = :id";
DB::connect()->query($q)->vars($id)->bind()->exec();

// Update field name from tbl_users where id is 2
```

### Multi update data

```php
$id = [ 11025, 11026 ];
foreach ( $id as $key => $ids ) {
  $params = [
    ':id' => $ids,
    ':user_name' => 'nsy_for_kids'
  ];
  $q = "UPDATE tbl_users SET user_name = :user_name WHERE id = :id";
  DB::connect()->query($q)->vars($params)->bind()->exec();
}

// Update field user_name to 'nsy_for_kids' from tbl_users where id is 11025 & 11026
```

### Delete data

```php
$id = [ ':id' => 2 ];

$q = "DELETE FROM tbl_users WHERE id = :id";
DB::connect()->query($q)->vars($id)->bind()->exec();

// Delete data from tbl_users where id is 2
```

### Multi delete data

```php
$id = [ 11025, 11026 ];
foreach ( $id as $key => $ids ) {
  $params = [
    ':id' => $ids
  ];
  $q = "DELETE FROM tbl_users WHERE id = :id";
  DB::connect()->query($q)->vars($params)->bind()->exec();
}

// Delete data from tbl_users where id is 11025 & 11026
```

### Insert data

```php
$param = [ ':user_name' => 'Harmoni' ];

$q = "INSERT INTO tbl_users (user_name) VALUES (:user_name)";
DB::connect()->query($q)->vars($param)->bind()->exec();

// Insert data to field user_name from tbl_users where user_name is 'Harmoni'
```

---

## Multi Insert | `multi_insert()`

To input multiple data into the database at once in one command.

```php
$arr = [
    [0] => [
        [0] => 11043 // for column id on tbl_users
        [1] => Vikry Yuansah // for column name on tbl_user
        [2] => vikry // for column user_name on tbl_user
    ],
    [1] => [
        [0] => 11042 // for column id on tbl_users
        [1] => Tialuna // for column name on tbl_user
        [2] => tia // for column user_name on tbl_user
    ]
];
$q = "INSERT INTO tbl_users (id, name, user_name)";
DB::connect()->query($q)->vars($arr)->multi_insert();
```

---

## NSY Transaction

Database transactions ensure that a set of data changes will only be made permanent if every statement is successful. Any query or code failure during a transaction can be caught and you then have the option to roll back the attempted changes.

NSY provides simple methods for beginning, committing, and rollbacking back transactions.

### Begin transaction

```php
DB::begin_trans();
```

### Commit transaction

```php
DB::commit_trans();
```

### Rollback transaction

```php
DB::rollback_trans();
```

### First example of transaction in `multi_insert()`

```php
$arr = [
    [0] => [
        [0] => 11043 // for column id on tbl_users
        [1] => Vikry Yuansah // for column name on tbl_user
        [2] => vikry // for column user_name on tbl_user
    ],
    [1] => [
        [0] => 11042 // for column id on tbl_users
        [1] => Tialuna // for column name on tbl_user
        [2] => tia // for column user_name on tbl_user
    ]
];
$q = "INSERT INTO tbl_users (id, name, user_name)";
DB::connect()->begin_trans()->query($q)->vars($arr)->multi_insert()->commit_trans();
```

### Second example of transaction in `multi_insert()`

```php
$arr = [
    [0] => [
        [0] => 11043 // for column id on tbl_users
        [1] => Vikry Yuansah // for column name on tbl_user
        [2] => vikry // for column user_name on tbl_user
    ],
    [1] => [
        [0] => 11042 // for column id on tbl_users
        [1] => Tialuna // for column name on tbl_user
        [2] => tia // for column user_name on tbl_user
    ]
];
$q = "INSERT INTO tbl_users (id, name, user_name)";
$conn = DB::connect();
$conn->begin_trans();
$conn->query($q);
$conn->vars($arr);
$conn->multi_insert();
$conn->commit_trans();
```

`begin_trans()` must be located in each code after we define the connection `DB::connect()`.

And before using a transaction, you must turn on the transaction mode in `Config/App.php` => `transaction` to `on` (default is `off`), to turn on the rollback function (The rollback function is enabled by default when `transaction = on`, so there's no need to call the `rollback_trans()`).

---

## Sets an Attribute on The Database Handle

Sets an attribute on the database handle. Some available generic attributes are listed below; some drivers may make use of additional driver specific attributes.
[See complete documentation](https://www.php.net/manual/en/pdo.setattribute.php).

```php
pdo_set_attr(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION)
```

**How to retrieve a statement attribute?**
[See complete documentation](https://www.php.net/manual/en/pdo.getattribute.php).

```php
pdo_get_attr(PDO::ATTR_ERRMODE)
```
