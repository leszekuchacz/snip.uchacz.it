Apache2.4
====================


Pomocne OneLinery
-----------------------------------

.. code-block:: bash
   :linenos:

   # Włączenie wszystkich dostepnych stron
   $ for i in `ls /etc/apache2/sites-available/`; do echo $i; done;


Włączenie zawieszki 503
-----------------------------------
.. code-block:: bash
   :linenos:

    #1 Włączamy moduł apacha2 rewrite
    $ a2enmod rewrite 

    #2 Dodajemy do konfiguracji strony 
     RewriteEngine on
     RewriteCond %{REQUEST_URI} !=/503.html
     RewriteRule ^(.*)$  - [R=503,L]
     ErrorDocument 503 /503.html

    #3 Tworzymy plik 503.html w DocumentRoot strony
    $ cd /var/www/strona/ && echo "Przerwa techniczna" > 503.html

    #4 Testujemy konfiguracje i restartujemy Apacha2
    $ apache2ctl configtest
    $ service apache2 restart