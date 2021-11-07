Sieci
====================
.. index:: network

Dignostyka ruchu sieciowego
-----------------------------------
.. index:: hping3
.. code-block:: bash
   :linenos:

   # Podszywanie sie pod adres 192.168.80.40 w celu sprawdzenia ruchu do 10.0.0.1
     hping3 -I eth0 -a 192.168.80.40 -s 3137 -p 1433 -S 10.0.0.1
