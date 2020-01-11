# NSY SYSTEM GUIDE PART 2
NSY is a simple PHP Framework that works well on MVC or HMVC mode.

Site example :
<a href="https://nsy.kazuyamarino.com/" target="_blank">https://nsy.kazuyamarino.com/</a>

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

<hr>

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

<hr>

## License
The code is available under the [MIT license](https://github.com/kazuyamarino/nsy/blob/master/LICENSE.txt)
