Varnish
====================
.. index:: varnish


Podstawowe komendy
-----------------------------------

.. code-block:: bash
   :linenos:

   # Usuniecie cachu dla strony snip.uchacz.it/admin/
   varnishadm -S /etc/varnish/secret -T localhost:6082 ban 'req.http.host ~ snip.uchacz.it && req.url == "/admin/"'

   # Wylaczenie backendu
   varnishadm -S /etc/varnish/secret -T localhost:6082 backend.list

   varnishadm -S /etc/varnish/secret -T localhost:6082 backend.set_health snip01 sick

   # Włączenie backendu
   varnishadm -S /etc/varnish/secret -T localhost:6082 backend.set_health snip01 healthy
   