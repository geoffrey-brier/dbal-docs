Type Support
============

The Fridge DBAL provides a powerfull type support which can be use in two places: Connection (parameters binding) or
Schema (Column type).

All types implements the ``Fridge\DBAL\Type\TypeInterface`` which is able to generate his SQL declaration and convert
database value from/to PHP value. They additionally give the corresponding PDO binding type.

Build-in Types
--------------

This UML diagram shows you the type architecture:

.. image:: /images/uml/type.jpeg
   :alt: UML Schema
   :align: center

The available types are:

* ``Type::TARRAY``: array
* ``Type::BIGINTEGER``: integer
* ``Type::BOOLEAN``: boolean
* ``Type::DATE``: date
* ``Type::DATETIME``: datetime
* ``Type::DECIMAL``: decimal
* ``Type::FLOAT``: float
* ``Type::INTEGER``: integer
* ``Type::OBJECT``: object
* ``Type::SMALINTEGER``: smallinteger
* ``Type::STRING``: string
* ``Type::TEXT``: text
* ``Type::TIME``: time

Flyweight
---------

A single type can be used a lot in a schema. In order to reduce the amount of memory used, all types are managed by the
``Fridge\DBAL\Type\Type`` which follows the `Flyweight pattern`_. That means there is only ever one instance of a type.

To manipulate the managed types, you can use the following API:

.. code-block:: php

    use Fridge\DBAL\Type\Type;

    Type::hasType($typeName);
    $type = Type::getType($typeName);
    Type::addType($typeName, $className);
    Type::overrideType($typeName, $className);
    Type::removeType($typeName);

.. _Flyweight pattern: http://en.wikipedia.org/wiki/Flyweight_pattern
