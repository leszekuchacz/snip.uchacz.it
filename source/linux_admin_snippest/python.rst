Python
====================
.. index:: python


Pożyteczne rzeczy
-----------------------------------
.. index:: SimpleHTTPServer

.. code-block:: bash
   :linenos:

   #Szybkie udostepnianie plikow
   mkdir ~/tmp && cd tmp && touch plik.txt
   python -m SimpleHTTPServer 8888

   # Sprawdzenie poprawności jsona
   cat json | python -c 'import json,sys;obj=json.load(sys.stdin);print obj;'#

