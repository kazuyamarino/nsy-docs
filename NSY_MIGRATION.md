# NSY Migrations

Migration is like version control for your database, allowing your team to easily modify and share application database schemes.

Migration is usually paired with the NSY schema builder to easily build your application's database schema. If you have told teammates to manually add columns to their local database schema, you have experienced problems that were resolved by database migration.

How to use migration on NSY, you only need to create the migration class by typing on the Terminal or CMD:

```
nsy make:migration <migration-name>
```

**For example :**

```
nsy make:migration create_database_and_table_supplier
```

And the result will be a file created from the results of the command earlier in the `System/Migrations`.

```
└── Migrations
       └── create_database_and_table_supplier.php
```

There are 2 methods in the file, namely `up()` and `down()` methods. If you want to run the method `up()` then the command is, `migup=class_name`
```
Example : http://localhost/nsy/migup=create_database_and_table_supplier
```

And for `down()`, `migdown=class_name`
```
Example : http://localhost/nsy/migdown=drop_table_supplier
```

Well, in that method, you can fill it with some help methods that have been defined by NSY to support migration like the method below:

### Create database
```
Mig::connect()->create_db('example_db');
```

### Delete database
```
Mig::connect()->drop_db('example_db');
```

### Create table with several columns (mysql/mariadb/mssql)
```
Mig::connect()->create_table('example', function() {
	return Mig::cols([
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
Mig::connect()->create_table('example', function() {
	return Mig::cols([
		'id' => 'bigint not null',
		'bundle' => 'bigint not null',
		'reader_id' => 'varchar(20) null',
		'trans_time' => 'datetime null',
		'antenna_id' => 'varchar(100) null',
		'tid' => 'varchar(100) null',
		'user_memory' => 'varchar(100) null',
		Mig::primary('id'),
		Mig::unique([
			'reader_id', 'trans_time'
		])
	]);
});
```

### Create table with timestamps column e.g. create_date/update_date/additional_date (mysql/mariadb/mssql)
```
Mig::connect()->create_table('example', function() {
	return Mig::cols([
		'id' => 'bigint not null',
		'bundle' => 'bigint not null',
		'reader_id' => 'varchar(20) null',
		'trans_time' => 'datetime null',
		'antenna_id' => 'varchar(100) null',
		'tid' => 'varchar(100) null',
		'user_memory' => 'varchar(100) null',
		Mig::primary('id'),
		Mig::unique([
			'reader_id', 'trans_time'
		])
	], Mig::timestamps() );
});
```

### Rename table (mysql/mariadb)
```
Mig::connect()->rename_table('example', 'newExample');
```

### Rename table (postgre)
```
Mig::connect()->alter_rename_table('example', 'newExample');
```

### Rename table (mssql)
```
Mig::connect()->sp_rename_table('example', 'newExample');
```

### Delete table if exist (mysql/mariadb)
```
Mig::connect()->drop_exist_table('example');
```

### Delete table
```
Mig::connect()->drop_table('example');
```

### Add columns (mysql/mariadb/postgre)
```
Mig::connect()->add_cols('example', function() {
	return Mig::cols([
		'Column1' => 'varchar(20)',
		'Column2' => 'varchar(20)',
		'Column3' => 'varchar(20)'
	]);
});
```

### Add columns (mssql)
```
Mig::connect()->add('example', function() {
	return Mig::cols([
		'Column1' => 'varchar(20)',
		'Column2' => 'varchar(20)',
		'Column3' => 'varchar(20)'
	]);
});
```

### Delete column (mysql/mariadb/postgre/mssql)
```
Mig::connect()->drop_cols('example', function() {
	return Mig::cols([
		'Column1',
		'Column2'
	]);
});
```

### Rename columns (mysql/mariadb)
```
Mig::connect()->change_cols('example', function() {
	return Mig::cols([
		'Column1' => 'NewColumn1',
		'Column2' => 'NewColumn2',
		'Column3' => 'NewColumn3'
	]);
});
```

### Rename columns (postgre)
```
Mig::connect()->rename_cols('example', function() {
	return Mig::cols([
		'Column1' => 'NewColumn1',
		'Column2' => 'NewColumn2',
		'Column3' => 'NewColumn3'
	]);
});
```

### Rename columns (mssql)
```
Mig::connect()->sp_rename_cols('example', function() {
	return Mig::cols([
		'Column1' => 'NewColumn1',
		'Column2' => 'NewColumn2',
		'Column3' => 'NewColumn3'
	]);
});
```

### Modify columns datatype (mysql/mariadb)
```
Mig::connect()->modify_cols('example', function() {
	return Mig::cols([
		'Column1' => 'bigint(12) not null',
		'Column2' => 'bigint(12) not null',
		'Column3' => 'bigint(12) not null'
	]);
});
```

### Modify columns primary and unique key (mysql/mariadb)
```
Mig::connect()->modify_cols('example', function() {
	return Mig::cols([
		Mig::primary([
			'Column1',
			'Column2'
		]),
		Mig::unique([
			'Column3',
			'Column4'
		])
	]);
});
```

### Modify columns datatype (mssql/postgre)
```
Mig::connect()->alter_cols('example', function() {
	return Mig::cols([
		'Column1' => 'char(12) not null',
		'Column2' => 'varchar(12) not null',
		'Column3' => 'datetime not null'
	]);
});
```

### Modify columns primary and unique key (mssql/postgre)
```
Mig::connect()->alter_cols('example', function() {
	return Mig::cols([
		Mig::primary([
			'Column1',
			'Column2'
		]),
		Mig::unique([
			'Column3',
			'Column4'
		])
	]);
});
```

### Create indexes in tables (mysql/mariadb/postgre)
The statement below is used to create indexes in tables.

Indexes are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.
```
 Mig::connect()->index('table_name', 'index_type', 'table_field_name');
 ```

 **Example :**
 ```
Mig::connect()->index('table_mahasiswa', 'BTREE', 'no_npm');
```

Index statement is also available for `PostgreSQL`, just a little modification in its functionality to :
```
Mig::connect()->index_pg('table_mahasiswa', 'BTREE', 'no_npm');
```