Bash
====================


Ciekawe zajawki
===============

fork bomb
---------
.. code-block:: python
   :linenos:

   :(){ :|:& };:

Liczby  zmienoprzecinkowe w bashu
-----------------------------------
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


bash proxy
------------
.. index:: bash proxy
.. code-block:: bash
   :linenos:

    http_proxy='http://proxyserver'
	HTTP_PROXY=${http_proxy}
	https_proxy=${http_proxy}
	HTTPS_PROXY=${https_proxy}
	no_proxy=localhost,127.0.0.1
	NO_PROXY=${no_proxy}
    export http_proxy https_proxy no_proxy HTTP_PROXY HTTPS_PROXY NO_PROXY
	
