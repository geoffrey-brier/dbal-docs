Debug your queries
==================

Being able to easily interact with your database is good but having the ability to debug your queries is better.

The Fridge DBAL logs all queries on the configured logger if there is an handler register on the ``DEBUG`` canal. So,
debugging your queries is as simple as pushing an handler:

.. code-block:: php
    :linenos:

    <?php

    use Monolog\Logger,
        Monolog\Handler\FirePHPHandler;

    $connection->getConfiguration()
        ->getLogger()
        ->pushHandler(new FirePHPHandler(), Logger::DEBUG);

Then, each time you call ``executeQuery`` or ``executeUpdate`` on your connection, the query will be logged on the
handler:

.. code-block:: php
    :linenos:

    <?php

    $query = 'SELECT firstname, lastname FROM users';
    $statement = $connection->executeQuery($query);

    $query = 'UPDATE users SET enabled = ? WHERE id = ?';
    $affetctedRows = $connection->executeUpdate($query, array(false, 1));
