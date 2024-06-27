# NSY Migrations

---

**Attention :**

* To be able to use the database migration feature on NSY, you must install several supporting applications, [see information here](https://github.com/kazuyamarino/nsy-docs/blob/master/README.md#the-requirement).
* And don't forget to set `env.php` for the connection that will be used for database migration, [see information here](https://github.com/kazuyamarino/nsy-docs/blob/master/NSY_MODEL.md#primary--secondary-database-connections)

---

Migration is like version control for your database, allowing your team to easily modify and share application database schemes.

Migration is usually paired with the NSY schema builder to easily build your application's database schema. If you have told teammates to manually add columns to their local database schema, you have experienced problems that were resolved by database migration.

How to use migration on NSY, you only need to create the migration class by typing on the Terminal or CMD :

```sh
nsy make:migrate <migration-name>
```

**For example :**

```sh
nsy make:migrate create_database_and_table_supplier
```

And the result will be a file created from the results of the command earlier in the `System/Migrations`.

```text
└── Migrations
       └── create_database_and_table_supplier.php
```

---

## Run The Migration

There are several ways to carry out database migration such as:

### Manual Method (Via URL/Browser)

There are 2 function in the file, namely `up()` and `down()` methods. If you want to run the method `up()` then the command is, `migup=class_name`.

```text
Example : http://localhost/nsy/migup=create_database_and_table_supplier
```

And for `down()`, `migdown=class_name`.

```text
Example : http://localhost/nsy/migdown=drop_table_supplier
```

### Command Line Method (Via NSY CLI)

#### Show list of Migration Class file

```sh
nsy show:migrate
```

#### Executes All Migration Class file

```sh
nsy run:migrate all
```

#### Executes the Selected Migration Class file

```text
nsy run:migrate list

result :
1) crud_table_05062024_163642.php
2) Migration_Test.php
Select a migration class from the above list: 
```

Just type in the number of the migration file you want to run, then press enter key.

```text
result :
1) crud_table_05062024_163642.php
2) Migration_Test.php
Select a migration class from the above list: 1
```

---

Well, in that function, you can fill it with some help methods that have been defined by NSY to support migration like the method below :

**Make 2 databases named `example_db_1` and `example_db_2` (mysql/mariadb) :**

```php
Mig::connect()->create_database(['example_db_1', 'example_db_2']);
```

**Delete databases named `example_db_1` and `example_db_2` (mysql/mariadb) :**

```php
Mig::connect()->drop_database(['example_db_1', 'example_db_2']);
```

**Create a table with several names and columns (mysql/mariadb) :**

```php
Mig::connect()->create_table('example_mysql', [
  Mig::bigint('id', 20)->auto_increment(),
  Mig::text('address')->null(),
  Mig::varchar('name')->null(),
  Mig::varchar('sales_code')->null(),
  Mig::varchar('customer_code')->null(),
  Mig::primary('id')
])->index('BTREE', ['sales_code', 'customer_code']);
    
Mig::connect()->create_table('example_mysql_timestamp', [
  Mig::date('date_field')->not_null(),
  Mig::datetime('datetime_field')->null(),
  Mig::timestamp('timestamp_field', 6)->null(),
  Mig::time('time_field')->null(),
  Mig::year('year_field', 4)->default(0)
]);

Mig::connect()->create_table('example_mysql_blob', [
  Mig::tinyblob('tinyblob_field')->not_null(),
  Mig::blob('blob_field')->null(),
  Mig::mediumblob('mediumblob_field')->default(0)
]);

Mig::connect()->create_table('example_mysql_alphanumeric', [
  Mig::char('char_field')->not_null(),
  Mig::varchar('varchar_field')->null(),
  Mig::tinytext('tinytext_field')->null(),
  Mig::text('text_field')->null(),
  Mig::mediumtext('mediumtext_field')->null(),
  Mig::longtext('longtext_field')->not_null(),
  Mig::binary('binary_field')->not_null(),
  Mig::varbinary('varbinary_field')->default(0)
])->index('BTREE', 'char_field');
```

**Create table with primary key & unique key (mysql/mariadb) :**

```php
Mig::connect()->create_table('example_mysql_numeric', [
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
])->index('BTREE', 'bigint_field');
```

**Rename the table from `example_mysql` to `rename_mysql` (mysql/mariadb) :**

```php
Mig::connect()->rename_table('example_mysql', 'rename_mysql');
```

**Delete some tables if any (mysql/mariadb) :**

```php
Mig::connect()->drop_exist_table([
  'example_mysql',
  'example_mysql_numeric',
  'example_mysql_alphanumeric',
  'example_mysql_timestamp',
  'example_mysql_blob'
]);
```

**Delete tables (mysql/mariadb) :**

```php
Mig::connect()->drop_table([
  'example_mysql',
  'example_mysql_numeric',
  'example_mysql_alphanumeric',
  'example_mysql_timestamp',
  'example_mysql_blob'
]);
```

**Add new columns to the `example_mysql` table (mysql/mariadb) :**

```php
Mig::connect()->add_cols('example_mysql', [
  Mig::char('char_field')->not_null(),
  Mig::varchar('varchar_field')->null(),
  Mig::tinytext('tinytext_field')->null(),
  Mig::text('text_field')->null(),
  Mig::mediumtext('mediumtext_field')->null(),
  Mig::longtext('longtext_field')->not_null(),
  Mig::binary('binary_field')->not_null(),
  Mig::varbinary('varbinary_field')->default(0)
]);
```

**Delete columns from `example_mysql` (mysql/mariadb) :**

```php
Mig::connect()->drop_cols('example_mysql', [
  'char_field',
  'varchar_field',
  'tinytext_field',
  'text_field',
  'mediumtext_field',
  'longtext_field',
  'binary_field',
  'varbinary_field',
]);
```

**Rename columns with datatype (mysql/mariadb) :**

```php
Mig::connect()->change_cols('example_mysql', [
  'char_field' => Mig::char('char_field_new')->not_null(),
  'varchar_field' => Mig::char('varchar_field_new')->not_null(),
  'tinytext_field' => Mig::text('text_field_new')->not_null(),
]);
```

**Rename columns (mysql/mariadb) :**

```php
Mig::connect()->rename_cols('example_mysql', [
  'char_field' => 'char_field_new',
  'varchar_field' => 'varchar_field_new',
  'tinytext_field' => 'tinytext_field_new',
]);
```

**Modify columns datatype (mysql/mariadb) :**

```php
Mig::connect()->modify_cols('example_mysql', [
  Mig::tinyblob('tinyblob_field')->not_null(),
  Mig::blob('blob_field')->null(),
  Mig::mediumblob('mediumblob_field')->default(0)
]);
```

**Modify columns primary and unique key (mysql/mariadb) :**

```php
Mig::connect()->modify_cols('example_mysql', [
  Mig::primary([
    'Column1',
    'Column2'
  ]),
  Mig::unique([
    'Column3',
    'Column4'
  ])
]);
```

## Create indexes in tables (mysql/mariadb)

The statement below is used to create indexes in tables.

Indexes are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.

```php
->index('index_type', 'table_field_name');
 ```

 **Example :**

 ```php
 Mig::connect()->create_table('example_mysql', [
  Mig::bigint('id', 20)->auto_increment(),
  Mig::text('address')->null(),
  Mig::varchar('name')->null(),
  Mig::varchar('sales_code')->null(),
  Mig::varchar('customer_code')->null(),
  Mig::primary('id')
])->index('BTREE', 'sales_code');

or 

Mig::connect()->create_table('example_mysql', [
  Mig::bigint('id', 20)->auto_increment(),
  Mig::text('address')->null(),
  Mig::varchar('name')->null(),
  Mig::varchar('sales_code')->null(),
  Mig::varchar('customer_code')->null(),
  Mig::primary('id')
])->index('BTREE', ['sales_code', 'customer_code']);
```
