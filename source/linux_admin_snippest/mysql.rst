Mysql
====================
.. index:: mysql


Przydatne 
-------------------
.. index:: alter

.. code-block:: mysql
   :linenos:

    # Wylączenie połączeń na bazie danych
    alter database ecolight connection limit  0;
    # On unlimited
    alter database ecolight connection limit -1;
