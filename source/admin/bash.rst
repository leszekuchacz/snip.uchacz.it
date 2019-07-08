Bash
====================
.. index:: bash

Liczby  zmienoprzecinkowe w bashu
-----------------------------------
.. index:: bc

.. code-block:: bash
   :linenos:

   # float w bc
     echo "scale=4; 1/8" | bc



Operacje na plikach
----------------------
.. index:: split,wc
.. code-block:: bash
   :linenos:

   # Dzielenie pliku na pol
     wc -l access.log | awk '{ print int($1/2)+1 }' | xargs  split access.log -l