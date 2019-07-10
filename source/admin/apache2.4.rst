Apache2.4
====================
.. index:: apache2.4

Pomocne OneLinery
-----------------------------------
.. index:: oneliner

.. code-block:: bash
   :linenos:

   # Włączenie wszystkich dostepnych stron
     for i in `ls /etc/apache2/sites-available/`; do echo $i; done;

   # Wylisotwanie, policzenie wystapien i posortowanie wszystkich adresow ip z logów apacha
     grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}" access.log  | sort -h | uniq -c | sort -h
 


Włączenie zawieszki 503
-----------------------------------
.. index:: 503.html

.. code-block:: bash
   :linenos:

    #1 Włączamy moduł apacha2 rewrite
      a2enmod rewrite 

    #2 Dodajemy do konfiguracji strony 
      RewriteEngine on
      RewriteCond %{REQUEST_URI} !=/503.html
      RewriteRule ^(.*)$  - [R=503,L]
      ErrorDocument 503 /503.html

    #3 Tworzymy plik 503.html w DocumentRoot strony
      cd /var/www/strona/ && echo "Przerwa techniczna" > 503.html

    #4 Testujemy konfiguracje i restartujemy Apacha2
      apache2ctl configtest
      service apache2 restart

Rewrity
-----------------------------------
.. index:: rewrite

.. code-block:: bash
   :linenos:

   # L - last( przerwy przetwarzanie innyc reguł)
   # Strona z kodem 301 wskazaniem na nową lokalizacje
   RewriteRule ^/omnie/                  http://%{HTTP_HOST}/pl/omnie/            [R=301,L]
