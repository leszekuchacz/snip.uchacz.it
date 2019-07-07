Redis
====================

.. contents: Uzyteczne komendy  do redisa



Podstawowe komendy
-------------------

.. code-block:: bash
   :linenos:

   # Pokazanie wszystkich kluczy w pamięci 
   $ redis-cli KEYS *

   # Pokazanie aktualnej konfiguracji redisa
   $ redis-cli info

   # Usuniecie wszystkich kluczy z pamieci
   $ redis-cli flushall


Łączenie sie do redisa po SSL
-------------------------------
.. code-block:: bash
   :linenos:

   $ ipython
   import redis
   r=redis.StrictRedis(host='adres_hosta', port=6379, password='haslo', ssl=True)
   r.pack_commands('info')


