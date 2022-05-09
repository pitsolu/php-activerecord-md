## SQLBuilder

This guide will show you how to use the php-activerecord SQL builder.

The first steps are to get the database connection and setup the SQL builder.

```php
$conn = ActiveRecord\ConnectionManager::get_connection("development");                                                                                                                         
$builder = new ActiveRecord\SQLBuilder($conn, "authors"); 
```

### [SELECT queries](#select)

We are now ready to generate a simple SELECT query:

```php
$builder->where("name = ?", "Hemingway");
echo $builder; /* => SELECT * FROM authors WHERE name = ? */
print_r($builder->get_where_values()); /* => array("Hemingway") */
```

You can also pass a hash to the `where()` method:

```php
$builder = new ActiveRecord\SQLBuilder($conn, "authors");                                                                                                            
$builder->where(array("name" => "Hemingway",                                                                                                                         
                      "country" => "USA"));
echo $builder; /* => SELECT * FROM authors WHERE `name`=? AND `country`=? */
print_r($builder->get_where_values()); /* => array('Hemingway', 'USA'); */

```

You can add ordering information:

```php
$builder = new ActiveRecord\SQLBuilder($conn, "authors");
$builder->order('id DESC');
echo $builder."\n"; /* => SELECT * FROM authors ORDER BY id DESC */
```
 Cool