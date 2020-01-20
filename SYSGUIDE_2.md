# NSY SYSTEM GUIDE PART 2
NSY is a simple PHP Framework that works well on MVC or HMVC mode.

Site example :
<a href="https://nsy.kazuyamarino.com/">https://nsy.kazuyamarino.com/</a>

## The Controllers

### Get variables from HTTP Request method.
```
$array = get_parsed_body();

print_r($array);
```

### Passing variable to view
If you want to passing variable to view, you can use example below :

```
$arr = [
	'my_name' => $this->m_welcome->welcome(),
	'mvc_page' => $this->m_hello->mvc_page(),
	'date' => Carbon::now()
];

$this->load_template('header', $arr);
```

The above example will generate variable `$my_name`, `$date` and `$mvc_page` in view.

### Load MVC or HMVC view file
#### Load MVC view file :

```
$this->load_view(null, 'filename');
```

#### Load HMVC view file :

```
$this->load_view('module-name', 'filename');
```

#### The PHP superglobals `post` and `get` are used to collect form-data.

```
$this->post('hello');

// Same as $_POST['hello'];
```

```
$this->get('hello');

// Same as $_GET['hello'];
```

#### Check if it's a PUT request :

```
$this->is_request_put();

// output : true or false
```

#### Check if it's a DELETE request :

```
$this->is_request_delete();

// output : true or false
```

#### Check if it's a GET request :

```
$this->is_request_get();

// output : true or false
```

#### Check if it's a POST request :

```
$this->is_request_post();

// output : true or false
```

#### Get request content type :

```
$this->get_content_type();

// output example : application/x-www-form-urlencoded
```

#### Parse array data from request params :

```
$array = $this->get_parsed_array();
```

#### Parse object data from request params :

```
$array = $this->get_parsed_object();
```

#### Get data from request params and parse to json :

```
$this->get_parsed_json();

$this->get_parsed_json($params);
$this->get_parsed_json('keywords');
```

#### Get data from request params and parse to string :

```
$this->get_parsed_string();

$this->get_parsed_string($params);
$this->get_parsed_string('keywords');
```

#### Get data from request params and parse to integer :

```
$this->get_parsed_integer();

$this->get_parsed_integer($params);
$this->get_parsed_integer('keywords');
```

#### Get data from request params and parse to float :

```
$this->get_parsed_float();

$this->get_parsed_float($params);
$this->get_parsed_float('keywords');
```

#### Get data from request params and parse to boolean :

```
$this->get_parsed_boolean();

$this->get_parsed_boolean($params);
$this->get_parsed_boolean('keywords');
```

#### Get data from request params and parse to ip :

```
$this->get_parsed_ip();

$this->get_parsed_ip($params);
$this->get_parsed_ip('keywords');
```

#### Get data from request params and parse to url :

```
$this->get_parsed_url();

$this->get_parsed_url($params);
$this->get_parsed_url('keywords');
```

#### Get data from request params and parse to email :

```
$this->get_parsed_email();

$this->get_parsed_email($params);
$this->get_parsed_email('keywords');
```

### Sequence variable
Create a sequence of the named placeholders, e.g. `:id0`, `:id1`, `:id2`. So the code would be:

```
$this->bind('placeholders')->vars('variable')->sequence()

// $ids = [2,3,4];
// $this->bind(":id")->vars($ids)->sequence()
//
// Will return `print_r()` result
//
// Array
// (
//    [0] => :id0,:id1,:id2
//    [1] => Array
//        (
//            [:id0] => 2
//            [:id1] => 3
//            [:id2] => 4
//        )
// )
```

### Instantiate Model class in the controller
Instantiate the Model class in the controller is useful to make it easier for us to give variables to it.
So there is no need to rewrite the instantiate class in another method.

Just have to write it in the contruct method, like this:

```
public function __construct() {
	// Instantiate Model Crud
	$this->m_crud = new m_crud;
}
```

then `$this->m_crud` is the variable.

---


## The Models

### Primary & Secondary Database Connections
NSY has supported 2 database connections in one running application.

You can see the env in root. There seems to be a configuration like this :

```
# Define Primary Connection
DB_CONNECTION=
DB_HOST=
DB_PORT=
DB_NAME=
DB_USER=
DB_PASS=

# Define Secondary Connection
DB_CONNECTION_SEC=
DB_HOST_SEC=
DB_PORT_SEC=
DB_NAME_SEC=
DB_USER_SEC=
DB_PASS_SEC=
```

Example for define Connection :

```
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_NAME=dev_example
DB_USER=root
DB_PASS=password
```

For example, in the model you want to run an sql query on the first database connection :

```
$q = 'SELECT * FROM blabla';
$this->connect()->query($q);
```

Then, if you want to run an sql query on the second database connection :

```
$q = 'SELECT * FROM blabla';
$this->connect_sec()->query($q);
```

### Getting data out of statement in dozens different formats. fetch_all()
That's most interesting function, with most astonishing features. Mostly thanks to its existence one can call PDO a wrapper, as this function can automate many operations otherwise performed manually.

`fetch_all()` returns an array that consists of all the rows returned by the query. From this fact we can make two conclusions:

This function should not be used, if many rows has been selected. In such a case conventional while loop ave to be used, fetching rows one by one instead of getting them all into array at once. "Many" means more than it is suitable to be shown on the average web page.

This function is mostly useful in a modern web application that never outputs data right away during fetching, but rather passes it to template.
You'd be amazed, in how many different formats this function can return data in (and how little an average PHP user knows of them), all controlled by `FETCH...` variables. Some of them are: `FETCH_NUM, FETCH_ASSOC, FETCH_BOTH, FETCH_CLASS, FETCH_KEY_PAIR, FETCH_UNIQUE, FETCH_GROUP, and FETCH_FUNC`.

#### Getting a plain array.
By default, this function will return just simple enumerated array consists of all the returned rows. Row formatting constants, such as `FETCH_NUM, FETCH_ASSOC, FETCH_COLUMN` etc can change the row format.

```
$q = 'SELECT id, name, username FROM users';
$d = $this->connect()->query($q)->style(FETCH_ASSOC)->fetch_all();

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
$d = $this->connect()->query($q)->style(FETCH_COLUMN)->fetch_all();

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
$d = $this->connect()->query($q)->style(FETCH_KEY_PAIR)->fetch_all();

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
$d = $this->connect()->query($q)->style(FETCH_NUM)->fetch();

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
$d = $this->connect()->query($q)->vars($id)->bind(BINDVAL)->fetch();

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
$d = $this->connect()->query($q)->vars($string)->bind(BINDPAR)->fetch();

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
$d = $this->connect()->query($q)->vars($id)->fetch_column();

return $d;

// output
Nayla Syifa
```

```
// getting number of rows in the table utilizing method chaining
$q = "SELECT count(*) FROM tbl_users";
$d = $this->connect()->query($q)->fetch_column();

return $d;

// output
3 => number of row data
```

### Getting row count
NSY uses PDO. PDO offers a function for returning the number of rows found by the query, `row_count()`, for example:

```
$q = "SELECT * FROM tbl_users";
$d = $this->connect()->query($q)->row_count();

return $d->result;

// output
3 => number of row data
```

However, if you want to get the number of affected rows, here is an example:

```
$id = [ ':id' => 2 ];

$q = "DELETE FROM tbl_users WHERE id = :id";
$deleted_data = $this->connect()->vars($id)->query($q)->row_count();

return deleted_data->result;

// output
1 => number of row data that was deleted
```

### Executes a prepared statement. exec()

#### Update data :

```
$id = [ ':id' => 2 ];

$q = "UPDATE tbl_users SET name = :name WHERE id = :id";
$this->connect()->query($q)->vars($id)->exec();

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
  $this->connect()->query($q)->vars($params)->exec();
}

// Update field user_name to 'nsy_for_kids' from tbl_users where id is 11025 & 11026
```

#### Delete data :

```
$id = [ ':id' => 2 ];

$q = "DELETE FROM tbl_users WHERE id = :id";
$this->connect()->query($q)->vars($id)->exec();

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
  $this->connect()->query($q)->vars($params)->exec();
}

// Delete data from tbl_users where id is 11025 & 11026
```

#### Insert data :

```
$param = [ ':user_name' => 'Harmoni' ];

$q = "INSERT INTO tbl_users (user_name) VALUES (:user_name)";
$this->connect()->query($q)->vars($param)->exec();

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
$this->connect()->query($q)->vars($arr)->multi_insert();
```

### NSY Transaction
Database transactions ensure that a set of data changes will only be made permanent if every statement is successful. Any query or code failure during a transaction can be caught and you then have the option to roll back the attempted changes.

NSY provides simple methods for beginning, committing, and rollbacking back transactions.

#### Begin transaction :

```
$this->begin_trans();
```

#### Commit transaction :

```
$this->end_trans();
```

#### Rollback transaction :

```
$this->null_trans();
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
$this->connect()->begin_trans()->query($q)->vars($arr)->multi_insert()->end_trans();
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
$conn = $this->connect();
$conn->begin_trans();
$conn->query($q);
$conn->vars($arr);
$conn->multi_insert();
$conn->end_trans();
```

`begin_trans()` must be located in each code after we define the connection `$this->connect()`.

And before using a transaction, you must turn on the transaction mode in `config/app.php` => `transaction` to `on` (default is `off`), to turn on the rollback function (The rollback function is enabled by default when `transaction = on`, so there's no need to call the `null_trans()`).

### Emulation mode, set ATTR_EMULATE_PREPARES to FALSE
For more information about this, go to the following URL [Emulation mode](https://phpdelusions.net/pdo#emulation).

```
$this->emulate_prepares_false();
```

### Mysqlnd and buffered queries. Huge datasets.
For more information about this, go to the following URL [Mysqlnd and buffered queries](https://phpdelusions.net/pdo#mysqlnd).

#### set MYSQL_ATTR_USE_BUFFERED_QUERY to FALSE

```
$this->use_buffer_query_false();
```

#### set MYSQL_ATTR_USE_BUFFERED_QUERY to TRUE

```
$this->use_buffer_query_true();
```

### Return type, set ATTR_STRINGIFY_FETCHES to TRUE
For more information about this, go to the following URL [Return type](https://phpdelusions.net/pdo#returntypes).

```
$this->stringify_fetches_true();
```

---

# Razr - The powerful PHP template engine

Razr is a powerful PHP template engine for PHP, whose syntax was inspired by ASP.NET Razor.<br/>
NSY has supported Razr in the View component. In addition NSY also still supports PHP code in the View component. Either using Razr or PHP, they can run together in one View component!

## Syntax

The Razr syntax uses `@` as special character. It is used to indicate a dynamic statement for the template engine. Within the `@()` notation you may use regular PHP. The following statements are supported.

### Echo data

Use the `@()` notation to echo any PHP data with escaping enabled by default.

**Example**

```html
<h1>@( $title )</h1>
@( 23 * 42 )
@( "<Data> is escaped by default." )
```

**Output**

```html
<h1>Some title</h1>
966
&lt;Data&gt; is escaped by default.
```

### Echo raw data

Use the `@raw()` directive to output any PHP data without escaping.

**Example**

```html
@raw("This will <strong>not</strong> be escaped.")
```

**Output**

```html
This will <strong>not</strong> be escaped.
```

### Variables

You can access single variables and nested variables in arrays/objects using the following dot `.` notation.

```php
array(
    'title' => 'I am the walrus',
    'artist' => array(
        'name' => 'The Beatles',
        'homepage' => 'http://www.thebeatles.com',
    )
)
```

**Example**

```html
<h1>@( $title )</h1>
<p>by @( $artist.name ), @( $artist.homepage )</p>
```

**Output**

```html
<h1>I am the walrus</h1>
<p>by The Beatles, http://www.thebeatles.com</p>
```

### Set variable values

**Example**

```html
@set($msg = "Hello World!")
@( $msg )
```

**Output**

```html
Hello World!
```


### Conditional control structures

Use `@if`, `@elseif`, `@else` for conditional control structures. Use any boolean PHP expression.

**Example**

```html
@set($expression = false)
@if( $expression )
    One.
@elseif ( !$expression )
    Two.
@else
    Three.
@endif
```

**Output**

```html
Two.
```


### Loops

You can use loop statements like `foreach` and `while`.

```html
@foreach($values as $key => $value)
    <p>@( $key ) - @( $value )</p>
@endforeach

@foreach([1,2,3] as $number)
    <p>@( $number )</p>
@endforeach

@while(true)
    <p>Infinite loop.</p>
@endwhile
```

### Include

Extract reusable pieces of markup to an external file using partials and the `@include` directive. You can pass an array of arguments as a second parameter.

**Example**

```html
<section>@include('partial.razr', ['param' => 'parameter'])</section>
```

`partial.razr`:

```html
<p>Partial with @( $param )<p>
```

**Output**

```html
<section><p>Partial with parameter<p><section>
```

### Extending templates with blocks

Use the `@block` directive to define blocks inside a template. Other template files can extend those files and define their own content for the defined blocks without changing the rest of the markup.

**Example**

```html
@include('child.razr', ['param' => 'parameter'])
```

`parent.razr`:

```html
<h1>Parent template</h1>

@block('contentblock')
    <p>Parent content.</p>
@endblock

<p>Parent content outside of the block.</p>
```

`child.razr`:

```html
@extend('parent.razr')

@block('contentblock')
    <p>You can extend themes and overwrite content inside blocks. Paremeters are available as well: @( $param ).</p>
@endblock

```

**Output**

```html
<h1>Parent template</h1>

<p>You can extend themes and overwrite content inside blocks. Paremeters are available as well: parameter.</p>

<p>Parent content outside of the block.</p>
```

---

# NSY Migrations

Migration is like version control for your database, allowing your team to easily modify and share application database schemes.

Migration is usually paired with the NSY schema builder to easily build your application's database schema. If you have told teammates to manually add columns to their local database schema, you have experienced problems that were resolved by database migration.

How to use migration on NSY, you only need to create the migration class by typing on the Terminal or CMD:

```
migrate <migration-name>
```

**For example**

```
migrate create_database_and_table_supplier
```

And the result will be a file created from the results of the command earlier in the `system/migrations`.

```
└── migrations
       └── create_database_and_table_supplier.php
```

There are 2 methods in the file, namely `up()` and `down()` methods. If you want to run the method `up()` then the command is,

```
migup=class_name

Example : http://localhost/nsy/migup=create_database_and_table_supplier
```

And for `down()`,

```
migdown=class_name

Example : http://localhost/nsy/migdown=drop_table_supplier
```

Well, in that method, you can fill it with some help methods that have been defined by NSY to support migration like the method below:

### Create database

```
$this->connect()->create_db('example_db');
```

### Delete database

```
$this->connect()->drop_db('example_db');
```

### Create table with several columns (mysql/mariadb/mssql)

```
$this->connect()->create_table('example', function() {
	return $this->cols([
		'id' => 'bigint(20) not null',
		'bundle' => 'bigint(20) not null',
		'reader_id' => 'varchar(20) null',
		'trans_time' => 'datetime null',
		'antenna_id' => 'varchar(100) null',
		'tid' => 'varchar(100) null',
		'user_memory' => 'varchar(100) null'
	]);
});
```

### Create table with primary key & unique key (mysql/mariadb/mssql)

```
$this->connect()->create_table('example', function() {
	return $this->cols([
		'id' => 'bigint not null',
		'bundle' => 'bigint not null',
		'reader_id' => 'varchar(20) null',
		'trans_time' => 'datetime null',
		'antenna_id' => 'varchar(100) null',
		'tid' => 'varchar(100) null',
		'user_memory' => 'varchar(100) null',
		$this->primary('id'),
		$this->unique([
			'reader_id', 'trans_time'
		])
	]);
});
```

### Create table with timestamps column e.g. create_date/update_date/additional_date (mysql/mariadb/mssql)

```
$this->connect()->create_table('example', function() {
	return $this->cols([
		'id' => 'bigint not null',
		'bundle' => 'bigint not null',
		'reader_id' => 'varchar(20) null',
		'trans_time' => 'datetime null',
		'antenna_id' => 'varchar(100) null',
		'tid' => 'varchar(100) null',
		'user_memory' => 'varchar(100) null',
		$this->primary('id'),
		$this->unique([
			'reader_id', 'trans_time'
		])
	], $this->timestamps() );
});
```

### Rename table (mysql/mariadb)

```
$this->connect()->rename_table('example', 'newExample');
```

### Rename table (postgre)

```
$this->connect()->alter_rename_table('example', 'newExample');
```

### Rename table (mssql)

```
$this->connect()->sp_rename_table('example', 'newExample');
```

### Delete table if exist (mysql/mariadb)

```
$this->connect()->drop_exist_table('example');
```

### Delete table

```
$this->connect()->drop_table('example');
```

### Add columns (mysql/mariadb/postgre)

```
$this->connect()->add_cols('example', function() {
	return $this->cols([
		'Column1' => 'varchar(20)',
		'Column2' => 'varchar(20)',
		'Column3' => 'varchar(20)'
	]);
});
```

### Add columns (mssql)

```
$this->connect()->add('example', function() {
	return $this->cols([
		'Column1' => 'varchar(20)',
		'Column2' => 'varchar(20)',
		'Column3' => 'varchar(20)'
	]);
});
```

### Delete column (mysql/mariadb/postgre/mssql)

```
$this->connect()->drop_cols('example', function() {
	return $this->cols([
		'Column1',
		'Column2'
	]);
});
```

### Rename columns (mysql/mariadb)

```
$this->connect()->change_cols('example', function() {
	return $this->cols([
		'Column1' => 'NewColumn1',
		'Column2' => 'NewColumn2',
		'Column3' => 'NewColumn3'
	]);
});
```

### Rename columns (postgre)

```
$this->connect()->rename_cols('example', function() {
	return $this->cols([
		'Column1' => 'NewColumn1',
		'Column2' => 'NewColumn2',
		'Column3' => 'NewColumn3'
	]);
});
```

### Rename columns (mssql)

```
$this->connect()->sp_rename_cols('example', function() {
	return $this->cols([
		'Column1' => 'NewColumn1',
		'Column2' => 'NewColumn2',
		'Column3' => 'NewColumn3'
	]);
});
```

### Modify columns datatype (mysql/mariadb)

```
$this->connect()->modify_cols('example', function() {
	return $this->cols([
		'Column1' => 'bigint(12) not null',
		'Column2' => 'bigint(12) not null',
		'Column3' => 'bigint(12) not null'
	]);
});
```

### Modify columns primary and unique key (mysql/mariadb)

```
$this->connect()->modify_cols('example', function() {
	return $this->cols([
		$this->primary([
			'Column1',
			'Column2'
		]),
		$this->unique([
			'Column3',
			'Column4'
		])
	]);
});
```

### Modify columns datatype (mssql/postgre)

```
$this->connect()->alter_cols('example', function() {
	return $this->cols([
		'Column1' => 'char(12) not null',
		'Column2' => 'varchar(12) not null',
		'Column3' => 'datetime not null'
	]);
});
```

### Modify columns primary and unique key (mssql/postgre)

```
$this->connect()->alter_cols('example', function() {
	return $this->cols([
		$this->primary([
			'Column1',
			'Column2'
		]),
		$this->unique([
			'Column3',
			'Column4'
		])
	]);
});
```

---

## License
The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt)
