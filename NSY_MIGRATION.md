# NSY Migrations

---

Migration is like version control for your database, allowing your team to easily modify and share application database schemes.

Migration is usually paired with the NSY schema builder to easily build your application's database schema. If you have told teammates to manually add columns to their local database schema, you have experienced problems that were resolved by database migration.

How to use migration on NSY, you only need to create the migration class by typing on the Terminal or CMD :

```sh
nsy make:migration <migration-name>
```

**For example :**

```sh
nsy make:migration create_database_and_table_supplier
```

And the result will be a file created from the results of the command earlier in the `System/Migrations`.

```text
└── Migrations
       └── create_database_and_table_supplier.php
```

There are 2 methods in the file, namely `up()` and `down()` methods. If you want to run the method `up()` then the command is, `migup=class_name`.

```text
Example : http://localhost/nsy/migup=create_database_and_table_supplier
```

And for `down()`, `migdown=class_name`.

```text
Example : http://localhost/nsy/migdown=drop_table_supplier
```

Well, in that method, you can fill it with some help methods that have been defined by NSY to support migration like the method below :

## Create database

```php
Mig::connect()->create_db('example_db');
```

## Delete database

```php
Mig::connect()->drop_db('example_db');
```

## Create table with several columns (mysql/mariadb)

```php
Mig::connect()->create_table('example', function() {
  return Mig::cols([
    Mig::bigint('bigint_field')->null(),
    Mig::bit('bit_field')->null(),
    Mig::tinyint('tinyint_field')->null(),
    Mig::smallint('smallint_field')->null(),
    Mig::mediumint('mediumint_field')->null(),
    Mig::int('int_field')->not_null(),
    Mig::integer('integer_field')->not_null(),
    Mig::decimal('decimal_field')->default(0),
    Mig::dec('dec_field')->default(0),
    Mig::numeric('numeric_field')->not_null(),
    Mig::fixed('fixed_field')->not_null(),
    Mig::float('float_field')->not_null(),
    Mig::double('double_field')->default(0),
    Mig::double_precision('double_precision_field')->not_null(),
    Mig::real('real_field')->not_null(),
    Mig::bool('bool_field')->not_null(),
    Mig::boolean('boolean_field')->not_null()
  ]);
});
```

## Create table with primary key & unique key (mysql/mariadb)

```php
Mig::connect()->create_table('example', function() {
  return Mig::cols([
    Mig::bigint('bigint_field', 20)->auto_increment(),
    Mig::bit('bit_field')->null(),
    Mig::tinyint('tinyint_field')->null(),
    Mig::smallint('smallint_field')->null(),
    Mig::mediumint('mediumint_field')->null(),
    Mig::int('int_field')->not_null(),
    Mig::integer('integer_field')->not_null(),
    Mig::decimal('decimal_field')->default(0),
    Mig::dec('dec_field')->default(0),
    Mig::numeric('numeric_field')->not_null(),
    Mig::fixed('fixed_field')->not_null(),
    Mig::float('float_field')->not_null(),
    Mig::double('double_field')->default(0),
    Mig::double_precision('double_precision_field')->not_null(),
    Mig::real('real_field')->not_null(),
    Mig::bool('bool_field')->not_null(),
    Mig::boolean('boolean_field')->not_null(),
    Mig::primary('bigint_field'),
    Mig::unique(['integer_field', 'tinyint_field'])
  ]);
});
```

## Rename table (mysql/mariadb)

```php
Mig::connect()->rename_table('example', 'newExample');
```

## Delete table if exist (mysql/mariadb)

```php
Mig::connect()->drop_exist_table('example');
```

## Delete table

```php
Mig::connect()->drop_table('example');
```

## Add columns (mysql/mariadb)

```php
Mig::connect()->add_cols('example', function() {
 return Mig::cols([
    Mig::char('char_field')->not_null(),
    Mig::varchar('varchar_field')->null(),
    Mig::tinytext('tinytext_field')->null(),
    Mig::text('text_field')->null(),
    Mig::mediumtext('mediumtext_field')->null(),
    Mig::longtext('longtext_field')->not_null(),
    Mig::binary('binary_field')->not_null(),
    Mig::varbinary('varbinary_field')->default(0)
 ], 'disabled');
});
```

## Delete column (mysql/mariadb)

```php
Mig::connect()->drop_cols('example', function() {
  return Mig::cols([
    'Column1',
    'Column2'
  ], 'disabled');
});
```

## Rename columns (optional)

```php
Mig::connect()->change_cols('example', function() {
  return Mig::cols([
    'Column1' => 'NewColumn1',
    'Column2' => 'NewColumn2',
    'Column3' => 'NewColumn3'
  ], 'disabled');
});
```

## Rename columns (mysql/mariadb)

```php
Mig::connect()->rename_cols('example', function() {
  return Mig::cols([
    'Column1' => 'NewColumn1',
    'Column2' => 'NewColumn2',
    'Column3' => 'NewColumn3'
  ], 'disabled');
});
```

## Modify columns datatype (mysql/mariadb)

```php
Mig::connect()->modify_cols('example', function() {
  return Mig::cols([
    Mig::tinyblob('tinyblob_field')->not_null(),
    Mig::blob('blob_field')->null(),
    Mig::mediumblob('mediumblob_field')->default(0)
  ], 'disabled');
});
```

## Modify columns primary and unique key (mysql/mariadb)

```php
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
  ], 'disabled');
});
```

## Create indexes in tables (mysql/mariadb)

The statement below is used to create indexes in tables.

Indexes are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.

```php
 Mig::connect()->index('table_name', 'index_type', 'table_field_name');
 ```

 **Example :**

 ```php
Mig::connect()->index('table_mahasiswa', 'BTREE', 'no_npm');
```
