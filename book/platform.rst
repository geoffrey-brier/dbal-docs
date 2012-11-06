Platform
========

A Platform abstracts query generation and normalizes the differences of each database vendors.

.. code-block:: php
    :linenos:

    <?php

    $platform = $connection->getPlatform();

Supported Features
------------------

A Platform can not support all features. To know the supported ones, the following API is available.

.. code-block:: php
    :linenos:

    <?php

    $platform->supportSequence();
    $platform->supportView();
    $platform->supportPrimaryKey();
    $platform->supportForeignKey();
    $platform->supportIndex();
    $platform->supportCheck();
    $platform->supportSavepoint();
    $platform->supportAutoIncrement();
    $platform->supportInlineTableColumnComment();

Query Generation
----------------

The main use case of a platform is the query generation. It can either build select queries in order to fetch database
informations or create, drop, alter queries to manipulate the database.

Select
^^^^^^

The ``Select`` query generation is mainly use in the schema manager when you fetch database schema informations.

If you want to get the current database or the available databases, you can use these methods:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSelectDatabaseSQLQuery();
    $query = $platform->getSelectDatabasesSQLQuery();

To get the available sequences, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSelectSequencesSQLQuery($database);

To get the available views, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSelectViewsSQLQuery($database);

To get the available table names, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSelectTableNamesSQLQuery($database);

To get the available table columns, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSelectTableColumnsSQLQuery($table, $database);

To get the available table primary key, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSelectTablePrimaryKeySQLQuery($table, $database);

To get the available table foreign keys, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSelectTableForeignKeysSQLQuery($table, $database);

To get the available table indexes, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSelectTableIndexesSQLQuery($table, $database);

To get the available table checks, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSelectTableChecksSQLQuery($table, $database);

Create
^^^^^^

The ``Create`` query generation is use in the schema manager too when you create database schema entity.

To create a database, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreateDatabaseSQLQueries($database);

To create a sequence, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreateSequenceSQLQueries($sequence);

To create a view, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreateViewSQLQueries($view);

To create a table, you can use this method which accepts as second argument an array of flags. They allows to filter
constraints creation. The available flags are:

* ``primary_key``: TRUE if queries include primary key else FALSE (default: TRUE).
* ``index``: TRUE if queries include indexes else FALSE (default: TRUE).
* ``foreign_key``: TRUE if queries include foreingn keys else FALSE (default: TRUE).
* ``check``: TRUE if queries include checks else FALSE (default: TRUE).

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreateTableSQLQueries($table, $flags);

To create a column, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreateColumnSQLQueries($column, $table);

To create a primary key, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreatePrimaryKeySQLQueries($primaryKey, $table);

To create a foreign key, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreateForeignKeySQLQueries($foreignKey, $table);

To create an index, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreateIndexSQLQueries($index, $table);

To create a check, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreateCheckSQLQueries($check, $table);

To create a constraint, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getCreateConstraintSQLQueries($constraint, $table);

Drop
^^^^

The ``Drop`` query generation is use in the schema manager too when you drop database schema entity.

To drop a database, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropDatabaseSQLQueries($database);

To drop a sequence, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropSequenceSQLQueries($sequence);

To drop a view, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropViewSQLQueries($view);

To drop a table, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropTableSQLQueries($table);

To drop a column, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropColumnSQLQueries($column, $table);

To drop a primary key, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropPrimaryKeySQLQueries($primaryKey, $table);

To drop a foreign key, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropForeignKeySQLQueries($foreignKey, $table);

To drop an index, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropIndexSQLQueries($index, $table);

To drop a check, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropCheckSQLQueries($check, $table);

To drop a constraint, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getDropConstraintSQLQueries($constraint, $table);

Alter / Rename
^^^^^^^^^^^^^^

The ``Alter / Rename`` query generation is use in the schema manager too when you alter database schema entity.

To rename a database, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getRenameDatabaseSQLQueries($schemaDiff);

To rename a table, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getRenameTableSQLQueries($tableDiff);

To alter a column, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $queries = $platform->getAlterColumnSQLQueries($columnDiff, $table);

Savepoint
^^^^^^^^^

The ``Savepoint`` is used by the connection when you process a nested transaction. The following API allows you to get
all possible queries:

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getCreateSavepointSQLQuery($savepointName);
    $query = $platform->getReleaseSavepointSQLQuery($savepointName);
    $query = $platform->getRollbackSavepointSQLQuery($savepointName);

Transaction Isolation
^^^^^^^^^^^^^^^^^^^^^

The following method allows you to manage the transaction isolation of your queries.

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSetTransactionIsolationSQLQuery($isolationLevel);

Charset
^^^^^^^

The ``Charset`` allows you to set the charset of your connection.

.. code-block:: php
    :linenos:

    <?php

    $query = $platform->getSetCharsetSQLQuery($charset);

Identifier Quoting
------------------

The Fridge DBAL does not automatically quote identifier. It is not possible to quote identifier efficiently across all
database vendors.

If you want to quote a single identifier, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $identifier = $platform->quotedIdentifer($identifier);

If you want to quote multiple identifiers, you can use this method:

.. code-block:: php
    :linenos:

    <?php

    $identifiers = $platform->quoteIdentifiers($identifiers);

The quote identifier can be retrieve through this method:

.. code-block:: php
    :linenos:

    <?php

    $quote = $platform->getQuoteIdentifier();

Type
----

Declaration
^^^^^^^^^^^

Like it is explain in the :doc:`Fridge Types <type>` documentation, a type is responsible to determine his own SQL
declaration. The following methods allow you to easily generate all of them:

.. code-block:: php
    :linenos:

    <?php

    $bigInteger = $platform->getBigIntegerSQLDeclaration($options);
    $boolean = $platform->getBooleanSQLDeclaration($options);
    $clob = $platform->getClobSQLDeclaration($options);
    $date = $platform->getDateSQLDeclaration($options);
    $dateTime = $platform->getDateTimeSQLDeclaration($options);
    $decimal = $platform->getDecimalSQLDeclaration($options);
    $float = $platform->getFloatSQLDeclaration($options);
    $integer = $platform->getIntegerSQLDeclaration($options);
    $smallInteger = $platform->getSmallIntegerSQLDeclaration($options);
    $time = $platform->getTimeSQLDeclaration($options);
    $varchar = $platform->getVarcharSQLDeclaration($options);

Mapping
^^^^^^^

The platform defines an explicit mapping between database & fridge types. It is used internally in order to process
database reverse ingenering.

.. code-block:: php
    :linenos:

    <?php

    $platform->hasMappedType($databaseType);
    $fridgeType = $platform->getMappedType($databaseType);
    $platform->addMappedtype($databaseType, $fridgeType);
    $platform->overrideMappedType($databaseType, $fridgeType);
    $platform->removeType($databaseType);

By default, the platform uses a stric mapping. That's mean if a mapped type is requested & does not exist, an exception
is throw. You can change this behavior by calling the ``setStrictMappedType`` on your platform. Then, if a mapped type
does not exist, the platform will fallback on the configured one (by default: text).

.. code-block:: php
    :linenos:

    <?php

    $strict = $platform->useStrictMappedType($strict);

    $fallbackType = $platform->getFallbackMappedType();
    $platform->setFallbackMappedType($fallbackType);

Mandatory
^^^^^^^^^

The previous mapping covers most of the use cases but for some types it is not enought. For example, a Fridge Array &
Text type is mapped most of the time to the Text database type. In this case, the process can't determine automatically
the appropriate Fridge Type.

To resolve this issue, a platform defines mandatory types which needs to be identified explicitely. The Fridge DBAL
stores this information in the table column comment following a specific pattern.

The mandatory types can be manipulates through this API:

.. code-block:: php
    :linenos:

    <?php

    $platform->hasMandatoryType($type);
    $platform->addMandatoryType($type);
    $platform->removeMandatoryType($type);

Constant
^^^^^^^^

A platform defines some database contants like default decimal precision, max varchar length, date format, etc.

The following API allows you to deal with default database constants:

.. code-block:: php
    :linenos:

    <?php

    $defaultPrecision = $platform->getDefaultDecimalPrecision();
    $defaultScale = $platform->getDefaultDecimalScale();
    $defaultVarcharLength = $platform->getDefaultVarcharLength();
    $defaultTransactionIsolation = $platform->getDefaultTransactionIsolation();

    $maxVarcharLength = $platform->getMaxVarcharLength();

    $dateFormat = $platform->getDateFormat();
    $timeFormat = $platform->getTimeFormat();
    $dateTimeFormat = $platform->getDateTimeFormat();
