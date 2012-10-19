Expression Builder
==================

An expression builder allows you to easily build an expression which can be used in the ``where`` or ``having`` query
builder clause or in the check constraint definition. It can build either a ``Fridge\DBAL\Query\Expression\Expression``
or a simple string expression.

To get a ``Fridge\DBAL\Query\Expression\ExpressionBuilder``, you need to call the ``getExpressionBuilder`` method on
your connection or query builder.

.. code-block:: php

    $expressionBuilder = $connection->getExpressionBuilder();
    $expressionBuilder = $queryBuilder->getExpressionBuilder();

Expression
----------

The Fridge DBAL provides a way to define SQL expression as a PHP Object. An SQL expression is represented by the
``Fridge\DBAL\Query\Expression\Expression`` which provides a fluent API allowing you to easily manipulate your
expression.

And Expression
^^^^^^^^^^^^^^

To build an ``AND`` expression, you need to call the ``andX`` method and then specify your expression parts as an array.

.. code-block:: php

    $expression = $expressionBuilder->andX(array('foo = ?', 'bar = ?'));

    /* foo = ? AND bar = ? */

Or Expression
^^^^^^^^^^^^^

To build an ``OR`` expression, you need to call the ``orX`` method and the specify your expresssion parts as an array.

.. code-block:: php

    $expression = $expressionBuilder->orX(array('foo = ?', 'bar = ?'));

    /* foo = ? OR bar = ? */

Composite Expression
^^^^^^^^^^^^^^^^^^^^

A composite expression represents the mix between an ``AND`` expression & an ``OR`` expression. To allow that, an
expression can be made up of expressions herself that means you can build an Or/And expression like that:

.. code-block:: php

    $expression = $expressionBuilder->orX(array(
        'foo = ?',
        'bar = ?',
        $expressionBuilder->andX(array('baz > 0', 'baz < 100')),
    ));

    /* foo = ? OR bar = ? OR (baz > 0 AND baz < 100) */

API
---

The Expression Builder allows to build simple string expression like greater than, like, etc. It can obviously be used
with ``andX`` / ``orX`` methods.

Equal
^^^^^

To build a equal expression, you meed to call the ``equal`` method and then specify the two elements to compare.

.. code-block:: php

    $expression = $expressionBuilder->equal('foo', '?');

    /* foo = ? */

Not Equal
^^^^^^^^^

To build a non equal expression, you meed to call the ``notEqual`` method and then specify the two elements to compare.

.. code-block:: php

    $expression = $expressionBuilder->notEqual('foo', '?');

    /* foo <> ? */

Greater Than
^^^^^^^^^^^^

To build a greater than expression, you meed to call the ``greaterThan`` method and then specify the two elements to
compare.

.. code-block:: php

    $expression = $expressionBuilder->greatedThan('foo', '?');

    /* foo > ? */

Greater Than or Equal
^^^^^^^^^^^^^^^^^^^^^

To build a greater than or equal expression, you meed to call the ``greaterThanOrEqual`` method and then specify the
two elements to compare.

.. code-block:: php

    $expression = $expressionBuilder->greaterThanOrEqual('foo', '?');

    /* foo >= ? */

Lower Than
^^^^^^^^^^

To build a lower than expression, you meed to call the ``lowerThan`` method and then specify the two elements to
compare.

.. code-block:: php

    $expression = $expressionBuilder->lowerThan('foo', '?');

    /* foo < ? */

Lower Than or Equal
^^^^^^^^^^^^^^^^^^^

To build a lower than or equal expression, you meed to call the ``lowerThanOrEqual`` method and then specify the two
elements to compare.

.. code-block:: php

    $expression = $expressionBuilder->lowerThanOrEqual('foo', '?');

    /* foo <= ? */

Like
^^^^

To build a like expression, you meed to call the ``like`` method and then specify the two elements to compare.

.. code-block:: php

    $expression = $expressionBuilder->like('foo', '%?%');

    /* foo LIKE %?M */

Not Like
^^^^^^^^

To build a not like expression, you meed to call the ``notLike`` method and then specify the two elements to compare.

.. code-block:: php

    $expression = $expressionBuilder->notLike('foo', '%?%');

    /* foo NOT LIKE %?% */

Null
^^^^

To build a null expression, you meed to call the ``isNull`` method and then specify the element to compare.

.. code-block:: php

    $equal = $expressionBuilder->isNull('foo');

    /* foo IS NULL */

Not Null
^^^^^^^^

To build a not null expression, you meed to call the ``isNotNull`` method and then specify the element to compare.

.. code-block:: php

    $equal = $expressionBuilder->isNotNull('foo');

    /* foo IS NOT NULL */
