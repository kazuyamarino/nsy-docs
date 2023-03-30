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

And the result will be a file created from the results of the command earlier in the `System/Migrations`.

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