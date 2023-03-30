## NSY Models

### <ins>Primary & Secondary Database Connections</ins>
NSY has supported 2 database connections in one running application.

You can see the env in root. There seems to be a configuration like this :

```
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

Example for define Connection :

```
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
```

For example, in the model you want to run an sql query on the `primary` database connection :

```
$q = 'SELECT * FROM blabla';
DB::connect()->query($q)->vars()->bind()-fetch_all();;
```

Then, if you want to run an sql query on the `secondary` database connection :

```
$q = 'SELECT * FROM blabla';
DB::connect('secondary')->query($q)->vars()->bind()-fetch_all();;
```

### <ins>Getting data out of statement in dozens different formats. fetch_all()</ins>
That's most interesting function, with most astonishing features. Mostly thanks to its existence one can call PDO a wrapper, as this function can automate many operations otherwise performed manually.

`fetch_all()` returns an array that consists of all the rows returned by the query. From this fact we can make two conclusions:

This function should not be used, if many rows has been selected. In such a case conventional while loop ave to be used, fetching rows one by one instead of getting them all into array at once. "Many" means more than it is suitable to be shown on the average web page.

This function is mostly useful in a modern web application that never outputs data right away during fetching, but rather passes it to template.
You'd be amazed, in how many different formats this function can return data in (and how little an average PHP user knows of them), all controlled by `FETCH...` variables. Some of them are: `FETCH_NUM, FETCH_ASSOC, FETCH_BOTH, FETCH_CLASS, FETCH_KEY_PAIR, FETCH_UNIQUE, FETCH_GROUP, and FETCH_FUNC`.

#### Getting a plain array.
By default, this function will return just simple enumerated array consists of all the returned rows. Row formatting constants, such as `FETCH_NUM, FETCH_ASSOC, FETCH_COLUMN` etc can change the row format.

```
$q = 'SELECT id, name, username FROM users';
$d = DB::connect()->query($q)->style(FETCH_ASSOC)->fetch_all();

print_r($d);

// output
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

#### Getting a column number.
It is often very handy to get plain one-dimensional array right out of the query, if only one column out of many rows being fetched. Here you go:

```
$q = 'SELECT name FROM users';
$d = DB::connect()->query($q)->style(FETCH_COLUMN)->fetch_all();

print_r($d);

// output
Array
(
    [0] => Vikry Yuansah
)
```

#### Getting key-value pairs.
Also extremely useful format, when we need to get the same column, but indexed not by numbers in order but by another field. Here goes `FETCH_KEY_PAIR` constant:

```
$q = 'SELECT name FROM users';
$d = DB::connect()->query($q)->style(FETCH_KEY_PAIR)->fetch_all();

print_r($d);

// output
Array
(
    [1] => Vikry Yuansah
    [2] => Nayla Syifa
)
```

and many other modes in fetch_all.

### Getting data out of statement. fetch()
It fetches a single row from database, and moves the internal pointer in the result set, so consequent calls to this function will return all the resulting rows one by one.

```
$q = 'SELECT id, name FROM users';
$d = DB::connect()->query($q)->style(FETCH_NUM)->fetch();

print_r($d);

// output
Array
(
    [0] => 1
    [1] => Vikry Yuansah
)
```

Another way would be to bind these variables explicitly while setting the proper param type:

Binds a PHP variable to a corresponding named or question mark placeholder in the SQL statement that was used to prepare the statement.

BindValue with PARAM_INT (Defines variable type as integer/number) :

```
$id = [ ':id' => [3, PAR_INT] ];

$q = "SELECT id, name, user_name FROM tbl_users WHERE id = :id";
$d = DB::connect()->query($q)->vars($id)->bind(BINDVAL)->fetch();

print_r($d);

// output
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

```
$string = [ ':name' => ['%yuan%', PAR_STR] ];

$q = "SELECT id, name, user_name FROM tbl_users WHERE name LIKE :name";
$d = DB::connect()->query($q)->vars($string)->bind(BINDPAR)->fetch();

print_r($d);

// output
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

`BINDPAR` to bind PHP variables to the parameter markers: bound variables pass their value as input and receive the output value, if any, of their associated parameter markers

### Getting data out of statement. fetch_column()
A neat helper function that returns value of the single field of returned row. Very handy when we are selecting only one field:

```
// Getting the name based on id
$id = [ ':id' => 2 ];

$q = "SELECT name FROM tbl_users WHERE id = :id";
$d = DB::connect()->query($q)->vars($id)->fetch_column();

return $d;

// output
Nayla Syifa
```

```
// getting number of rows in the table utilizing method chaining
$q = "SELECT count(*) FROM tbl_users";
$d = DB::connect()->query($q)->fetch_column();

return $d;

// output
3 => number of row data
```

### Getting row count
NSY uses PDO. PDO offers a function for returning the number of rows found by the query, `row_count()`, for example:

```
$q = "SELECT * FROM tbl_users";
$d = DB::connect()->query($q)->row_count();

return $d->result;

// output
3 => number of row data
```

However, if you want to get the number of affected rows, here is an example:

```
$id = [ ':id' => 2 ];

$q = "DELETE FROM tbl_users WHERE id = :id";
$deleted_data = DB::connect()->vars($id)->query($q)->row_count();

return deleted_data->result;

// output
1 => number of row data that was deleted
```

### Executes a prepared statement. exec()

#### Update data :

```
$id = [ ':id' => 2 ];

$q = "UPDATE tbl_users SET name = :name WHERE id = :id";
DB::connect()->query($q)->vars($id)->exec();

// Update field name from tbl_users where id is 2
```

#### Multi Update data :

```
$id = [ 11025, 11026 ];
foreach ( $id as $key => $ids ) {
  $params = [
    ':id' => $ids,
    ':user_name' => 'nsy_for_kids'
  ];
  $q = "UPDATE tbl_users SET user_name = :user_name WHERE id = :id";
  DB::connect()->query($q)->vars($params)->exec();
}

// Update field user_name to 'nsy_for_kids' from tbl_users where id is 11025 & 11026
```

#### Delete data :

```
$id = [ ':id' => 2 ];

$q = "DELETE FROM tbl_users WHERE id = :id";
DB::connect()->query($q)->vars($id)->exec();

// Delete data from tbl_users where id is 2
```

#### Multi Delete data :

```
$id = [ 11025, 11026 ];
foreach ( $id as $key => $ids ) {
  $params = [
    ':id' => $ids
  ];
  $q = "DELETE FROM tbl_users WHERE id = :id";
  DB::connect()->query($q)->vars($params)->exec();
}

// Delete data from tbl_users where id is 11025 & 11026
```

#### Insert data :

```
$param = [ ':user_name' => 'Harmoni' ];

$q = "INSERT INTO tbl_users (user_name) VALUES (:user_name)";
DB::connect()->query($q)->vars($param)->exec();

// Insert data to field user_name from tbl_users where user_name is 'Harmoni'
```

### Multi Insert. multi_insert()
To input multiple data into the database at once in one command.

```
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

### NSY Transaction
Database transactions ensure that a set of data changes will only be made permanent if every statement is successful. Any query or code failure during a transaction can be caught and you then have the option to roll back the attempted changes.

NSY provides simple methods for beginning, committing, and rollbacking back transactions.

#### Begin transaction :

```
DB::begin_trans();
```

#### Commit transaction :

```
DB::end_trans();
```

#### Rollback transaction :

```
DB::null_trans();
```

#### First example of transaction in `multi_insert()`.

```
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
DB::connect()->begin_trans()->query($q)->vars($arr)->multi_insert()->end_trans();
```

#### Second example of transaction in `multi_insert()`.

```
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
$conn->end_trans();
```

`begin_trans()` must be located in each code after we define the connection `DB::connect()`.

And before using a transaction, you must turn on the transaction mode in `Config/App.php` => `transaction` to `on` (default is `off`), to turn on the rollback function (The rollback function is enabled by default when `transaction = on`, so there's no need to call the `null_trans()`).

### Emulation mode, set ATTR_EMULATE_PREPARES to FALSE
For more information about this, go to the following URL [Emulation mode](https://phpdelusions.net/pdo#emulation).

```
DB::emulate_prepares_false();
```

### Mysqlnd and buffered queries. Huge datasets.
For more information about this, go to the following URL [Mysqlnd and buffered queries](https://phpdelusions.net/pdo#mysqlnd).

#### set MYSQL_ATTR_USE_BUFFERED_QUERY to FALSE

```
DB::use_buffer_query_false();
```

#### set MYSQL_ATTR_USE_BUFFERED_QUERY to TRUE

```
DB::use_buffer_query_true();
```

### Return type, set ATTR_STRINGIFY_FETCHES to TRUE
For more information about this, go to the following URL [Return type](https://phpdelusions.net/pdo#returntypes).

```
DB::stringify_fetches_true();
```