Schema
======

The Fridge DBAL provides a very powerful database schema abstraction. It can be easily manipulate through a a fluent
API, use with the schema manager to update your database or via any comparator to manage simple migrations.

Representation
--------------

The Fridge DBAL offers an object-oriented representation of a database schema with support for all details about tables,
sequences, views, etc... These schema instances generate a representation that is equal for all the supported platforms.

This UML diagram shows you the Fridge schema architecture.

.. image:: /images/uml/schema.jpeg
   :alt: UML Schema
   :align: center

Schema
^^^^^^

A ``Schema`` represents a database schema. It provides an API to manage tables, views or sequences.

A Schema is described by a name:

.. code-block:: php

    use Fridge\DBAL\Schema\Schema;

    $schema = new Schema('name');

    $name = $schema->getName();
    $schema->setName($name);

To manage your tables, you can use the following methods:

.. code-block:: php

    $schema->hasTables();
    $schema->hasTable($name);

    $tables = $schema->getTables();
    $table = $schema->getTable($name);

    $schema->setTables($tables);
    $schema->addTable($table);

    $table = $schema->createTable($name);
    $schema->renameTable($oldName, $newName);
    $schema->dropTable($name);

To manage your views, you can use the following methods:

.. code-block:: php

    $schema->hasViews();
    $schema->hasView($name);

    $views = $schema->getViews();
    $view = $schema->getView($name);

    $schema->setViews($views);
    $schema->addView($view);

    $view = $schema->createView($name, $sql);
    $schema->renameView($oldName, $newName);
    $schema->dropView($name);

To manage your sequences, you can use the following methods:

.. code-block:: php

    $schema->hasSequences();
    $schema->hasSequence($name);

    $sequences = $schema->getSequences();
    $sequence = $schema->getSequence($name);

    $schema->setSequences($sequences);
    $schema->addSequence($sequence);

    $sequence = $schema->createSequence($name);
    $schema->renameSequence($oldName, $newName);
    $schema->dropSequence($name);

Table
^^^^^

A ``Table`` represents a database table. It can manage columns, primary key, foreign keys, indexes or checks.

Obvisouly, it wraps a name:

.. code-block:: php

    $name = $table->getName();
    $table->setName($name);

To manage your columns, you can use the following methods:

.. code-block:: php

    $table->hasColumns();
    $table->hasColumn($name);

    $columns = $table->getColumns();
    $column = $table->getColumn($name);

    $table->setColumns($columns);
    $table->addColumn($column);

    $column = $table->createColumn($name, $type);
    $table->renameColumn($oldName, $newName);
    $table->dropColumn($name);

To manage your primary key, you can use the following methods:

.. code-block:: php

    $table->hasPrimaryKey();
    $primaryKey = $table->getPrimaryKey();
    $table->setPrimaryKey($primaryKey);
    $primaryKey = $table->createPrimaryKey($columnNames, $name);
    $table->dropPrimaryKey();

To manage your foreign keys, you can use the following methods:

.. code-block:: php

    $table->hasForeignKeys();
    $table->hasForeignKey($name);

    $foreignKeys = $table->getForeignKeys();
    $foreignKey = $table->getForeignKey($name);

    $table->setForeignKeys($foreignKeys);
    $table->addForeignKey($foreignKey);

    $foreignKey = $table->createForeignKey(
        $localColumnNames,
        $foreignTableName,
        $foreignColumnNames,
        $name
    );

    $table->renameForeignKey($oldName, $newName);
    $table->dropForeignKey($name);

To manage your checks, you can use the following methods:

.. code-block:: php

    $table->hasChecks();
    $table->hasCheck($name);

    $checks = $table->getChecks();
    $check = $table->getCheck($name);

    $table->setChecks($checks);
    $table->addCheck($check);

    $check = $table->createCheck();
    $table->renameCheck($oldName, $newName);
    $table->dropCheck($name);

Column
^^^^^^

A ``Column`` represents a database table column. It provides an API to manage all details like type, length, not null,
etc.

The following API allows you to manage your column:

.. code-block:: php

    $name = $column->getName();
    $column->setName($name);

    $type = $column->getType();
    $column->setType($type);

    $length = $column->getLength();
    $column->setLength($length);

    $precision = $column->getPrecision();
    $column->setPrecision($precision);

    $scale = $column->getScale();
    $column->setScale($scale);

    $unsigned = $column->getUnsigned();
    $column->setUnsigned($unsigned);

    $fixed = $column->getFixed();
    $column->setFixed($fixed);

    $notNull = $column->isNotNull();
    $column->setNotNull($notNull);

    $default = $column->getDefault();
    $column->setDefault($default);

    $autoIncrement = $column->isAutoIncrement();
    $column->setAutoIncrement($autoIncrement);

    $comment = $column->getComment();
    $column->setComment($comment);

Constraint
^^^^^^^^^^

A ``Constraint`` represents a database constraint such as primary key, foreign key, index or check. It is represented
by the ``Fridge\DBAL\Schema\ContraintInterface``.

Primary Key
~~~~~~~~~~~

A ``PrimaryKey`` represents a database primary key. The following API allows you to manage it:

.. code-block:: php

    $name = $primaryKey->getName();
    $primaryKey->setName($name);

    $columnNames = $primaryKey->getColumnNames();
    $primaryKey->setColumnNames($columnNames);
    $primaryKey->addColumnName($columnName);

Foreign Key
~~~~~~~~~~~

A ``ForeignKey`` represents a database foreign key. The following API allows you to manage it:

.. code-block:: php

    $name = $foreignKey->getName();
    $foreignKey->setName($name);

    $localColumnNames = $foreignKey->getLocalColumnNames();
    $foreignKey->setLocalColumnNames($localColumnNames);

    $foreignTableName = $foreignKey->getForeignTableName();
    $foreignKey->setForeignTableName($foreignTableName);

    $foreignColumnNames = $foreignKey->getForeignColumnNames();
    $foreignKey->setForeignColumnNames($foreignColumnNames);

    $onDelete = $foreignKey->getOnDelete():
    $foreignKey->setOnDelete($onDelete);

    $onUpdate = $foreignKey->getOnUpdate():
    $foreignKey->setOnUpdate($onUpdate);

The Fridge foreign key supports on delete & on update referential actions. The following constants describes supported
ones.

.. code-block:: php

    \Fridge\DBAL\Schema\ForeignKey::CASCADE;
    \Fridge\DBAL\Schema\ForeignKey::NO_ACTION;
    \Fridge\DBAL\Schema\ForeignKey::RESTRICT;
    \Fridge\DBAL\Schema\ForeignKey::SET_NULL;

Index
~~~~~

An ``Index`` represents a database index. The following API allows you to manage it:

.. code-block:: php

    $name = $index->getName();
    $index->setName($name);

    $columnNames = $index->getColumnNames();
    $index->setColumnNames($columnNames);

    $unique = $index->isUnique();
    $index->setUnique($unique);

Check
~~~~~

A ``Check`` represents a database check constraint. The following API allows you to manage it:

.. code-block:: php

    $name = $check->getName();
    $check->setName($name);

    $definition = $check->getDefinition();
    $check->setDefinition($definition);

Sequence
^^^^^^^^

A ``Sequence`` represents a database sequence. The following API allows you to manage it:

.. code-block:: php

    $name = $sequence->getName();
    $sequence->setName($name);

    $initialValue = $sequence->getInitialValue();
    $sequence->setInitialValue($initialValue);

    $incrementSize = $sequence->getIncrementSize();
    $sequence->setIncrementSize($incrementSize);

View
^^^^

A ``View`` represents a database sequence. The following API allows you to manage it:

.. code-block:: php

    $name = $view->getName();
    $view->setName($name);

    $sql = $view->getSQL();
    $view->setSQL($sql);

Manipulation
------------

To manipulate your database schema, you will need a ``SchemaManager``. To get it, you can use the ``getSchemaManager``
method on your connection.

.. code-block:: php

    $schemaManager = $connection->getSchemaManager();

Schema
^^^^^^

To fetch your entire schema, you can use the ``getSchema`` on your schema manager.

.. code-block:: php

    $schema = $schemaManager->getSchema();

If you want to fetch a different schema of the one define in your connection, you can specify the name as argument.

.. code-block:: php

    $schema = $schemaManager->getSchema($schemaName);

The other schema manipulations are available through this API:

.. code-block:: php

    $schemaManager->createSchema($schema);
    $schemaManager->dropSchema($schema);
    $schemaManager->dropAndCreateSchema($schema);

Table
^^^^^

The schema manager can either fetch tables names, tables or a specific table.

.. code-block:: php

    $tableNames = $schemaManager->getTableNames();
    $tables = $schemaManager->getTables();
    $table = $schemaManager->getTable($tableName);

If you want to fetch tables from a different schema of the one define in your connection, you can specify the schema
name as argument.

.. code-block:: php

    $tableNames = $schemaManager->getTableNames($schemaName);
    $tables = $schemaManager->getTables($schemaName);
    $table = $schemaManager->getTable($name, $schemaName);

The other table manipulations are available through this API:

.. code-block:: php

    $schemaManager->createTables($tables);
    $schemaManager->createTable($table);

    $schemaManager->dropTables($tables);
    $schemaManager->dropTable($table);

    $schemaManager->dropAndCreateTables($tables);
    $schemaManager->dropAndCreateTable($table);

Column
^^^^^^

The schema manager allows you to fetch columns of a specific table.

.. code-block:: php

    $columns = $schemaManager->getTableColumns($tableName);

If you want to fetch table columns from a different schema of the one define in your connection, you can specify the
schema name as argument.

.. code-block:: php

    $columns = $schemaManager->getTableColumns($tableName, $schemaName);

The other manipulations are available through this API:

.. code-block:: php

    $schemaManager->createColumn($column, $tableName);
    $schemaManager->dropColumn($column, $tableName);
    $schemaManager->dropAndCreateColumn($column, $tableName);

Primary Key
^^^^^^^^^^^

The schema manager can fetch the primary key of a specific table.

.. code-block:: php

    $primaryKey = $schemaManager->getTablePrimaryKey($tableName);

If you want to fetch a table primary key from a different schema of the one define in your connection, you can specify
the schema name as argument.

.. code-block:: php

    $primaryKey = $schemaManager->getTablePrimaryKey($tableName, $schemaName);

The other manipulations are available through this API:

.. code-block:: php

    $schemaManager->createPrimaryKey($primaryKey, $tableName);
    $schemaManager->dropPrimaryKey($primaryKey, $tableName);
    $schemaManager->dropAndCreatePrimaryKey($primaryKey, $tableName);

Foreign Key
^^^^^^^^^^^

The schema manager allows you to fetch the foreign keys of a specific table.

.. code-block:: php

    $foreignKeys = $schemaManager->getTableForeignKeys($tableName);

If you want to fetch table foreign keys from a different schema of the one define in your connection, you can specify
the schema name as argument.

.. code-block:: php

    $foreignKeys = $schemaManager->getTableForeignKeys($tableName, $schemaName);

The other manipulations are available through this API:

.. code-block:: php

    $schemaManager->createForeignKey($foreignKey, $tableName);
    $schemaManager->dropForeignKey($foreignKey, $tableName);
    $schemaManager->dropAndCreateForeignKey($foreignKey, $tableName);

Index
^^^^^

The schema manager can fetch the indexes of a specific table.

.. code-block:: php

    $indexes = $schemaManager->getTableIndexes($tableName);

If you want to fetch table indexes from a different schema of the one define in your connection, you can specify the
schema name as argument.

.. code-block:: php

    $indexes = $schemaManager->getTableIndexes($tableName, $schemaName);

The other manipulations are available through this API:

.. code-block:: php

    $schemaManager->createIndex($index, $tableName);
    $schemaManager->dropIndex($index, $tableName);
    $schemaManager->dropAndCreateIndex($index, $tableName);

Check
^^^^^

The schema manager allows you to fetch the check constraints of a specific table.

.. code-block:: php

    $checks = $schemaManager->getTableChecks($tableName);

If you want to fetch table check constraints from a different schema of the one define in your connection, you can
specify the schema name as argument.

.. code-block:: php

    $checks = $schemaManager->getTableChecks($tableName, $schemaName);

The other manipulations are available through this API:

.. code-block:: php

    $schemaManager->createCheck($check, $tableName);
    $schemaManager->dropCheck($check, $tableName);
    $schemaManager->dropAndCreateCheck($check, $tableName);

Constraint
^^^^^^^^^^

Like explain in the representation section, the ``PrimaryKey``, ``ForeignKey``, ``Index`` & ``Check`` implements the
``ConstraintInterface``. The schema manager allows you to manipulate all these classes like a ``Constraint``.

.. code-block:: php

    $schemaManager->createConstraint($constraint, $tableName);
    $schemaManager->dropConstraint($constraint, $tableName);
    $schemaManager->dropAndCreateConstraint($constraint, $tableName);

Sequence
^^^^^^^^

The schema manager can fetch schema sequences.

.. code-block:: php

    $sequences = $schemaManager->getSequences();

If you want to fetch schema sequences from a different schema of the one define in your connection, you can specify
the schema name as argument.

.. code-block:: php

    $sequences = $schemaManager->getSequences($schemaName);

The other manipulations are available through this API:

.. code-block:: php

    $schemaManager->createSequence($sequence);
    $schemaManager->dropSequence($sequence);
    $schemaManager->dropAndCreateSequence($sequence);

View
^^^^

The schema manager allows you to fetch schema views.

.. code-block:: php

    $views = $schemaManager->getViews();

If you want to fetch schema views from a different schema of the one define in your connection, you can specify the
schema name as argument.

.. code-block:: php

    $views = $schemaManager->getViews($schemaName);

The other manipulations are available through this API:

.. code-block:: php

    $schemaManager->createView($view);
    $schemaManager->dropView($view);
    $schemaManager->dropAndCreateView($view);

Comparison
----------

The Fridge DBAL provides a powerfull schema comparison at different levels. It can compare schemas, tables or columns
and then update your database or simply collect SQL queries to further update your database.

To allows this, each comparator gives you a representation of the difference between your two schema entities. Then,
this representation can be used to update your database through the schema manager or collect SQL queries through
the appropriate SQL collector.

In order to deal with this process, all schema classes are clonable.

.. code-block:: php

    $schema = $schemaManager->getSchema();
    $newSchema = clone $schema;

Schema Comparison
^^^^^^^^^^^^^^^^^

To compare two schemas, you need the ``Fridge\DBAL\Schema\Comparator\SchemaComparator``.

.. code-block:: php

    use Fridge\DBAL\Schema\Comparator\SchemaComparator;

    $oldSchema = $schemaManager->getSchema();
    $newSchema = clone $oldSchema;

    // Update the new schema

    $schemaComparator = new SchemaComparator();
    $schemaDiff = $schemaComparator->compare($oldSchema, $newSchema);

    $schemaManager->alterSchema($schemaDiff);

To collect SQL queries, you need to use the ``Fridge\DBAL\SchemaManager\SQLCollector\AlterSchemaSQLCollector``.

.. code-block:: php

    use Fridge\DBAL\SchemaManager\SQLCollector\AlterSchemaSQLCollector;

    $sqlCollector = new AlterSchemaSQLCollector($platform);
    $sqlCollector->collect($schemaDiff);

    $queries = $sqlCollector->getQueries();

Table Comparison
^^^^^^^^^^^^^^^^

To compare two schemas, you need the ``Fridge\DBAL\Schema\Comparator\TableComparator``.

.. code-block:: php

    use Fridge\DBAL\Schema\Comparator\TableComparator;

    $oldTable = $schemaManager->getTable($tableName);
    $newTable = clone $oldTable;

    // Update the new table

    $tableComparator = new TableComparator();
    $tableDiff = $tableComparator->compare($oldTable, $newTable);

    $schemaManager->alterTable($tableDiff);

To collect SQL queries, you need to use the ``Fridge\DBAL\SchemaManager\SQLCollector\AlterTableSQLCollector``.

.. code-block:: php

    use Fridge\DBAL\SchemaManager\SQLCollector\AlterSchemaSQLCollector;

    $sqlCollector = new AlterSchemaSQLCollector($platform);
    $sqlCollector->collect($schemaDiff);

    $queries = $sqlCollector->getQueries();

Column Comparison
^^^^^^^^^^^^^^^^^

To compare two schemas, you need the ``Fridge\DBAL\Schema\Comparator\ColumnComparator``.

.. code-block:: php

    use Fridge\DBAL\Schema\Comparator\ColumnComparator;

    $oldColumn = $schemaManager->getTable($tableName)->getColumn($columnName);
    $newColumn = clone $oldColumn;

    // Update the new column

    $columnComparator = new ColumnComparator();
    $columnDiff = $columnComparator->compare($oldColumn, $newColumn);

    $schemaManager->alterColumn($columnDiff);

To collect SQL queries, you don't need an SQL collector. You just need to get the alter column SQL queries from the
platform.

.. code-block:: php

    $queries = $connection->getPlatform()->getAlterColumnSQLQueries($columnDiff, $tableName);
