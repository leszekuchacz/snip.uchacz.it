Openssl
====================
.. index:: openssl
.. contents: Uzyteczne komendy  do openssl


Diagnostyka SSL
-----------------
.. index:: openssl
.. code-block:: bash
   :linenos:

   # test połaczenia www SSL
   openssl s_client -connect uchacz.it:443

   # test połaczenia smtp SSL
   openssl s_client -starttls smtp -crlf -connect poczta.wp.pl:465 -showcerts


Sprawdzenie poprawności klucza prywatnego  z wygenerowany certem
-----------------------------------------------------------------
.. index:: openssl,x509,rsa
.. code-block:: bash
   :linenos:

   # Oba wygenerowane sha1 muszą sie zgadzać 
   openssl x509 -in /path/to/yourdomain.crt -noout -modulus | openssl sha1
   
   openssl rsa -in /path/to/your.key -noout -modulus | openssl sha1


Sprawdzenie do kiedy jest ważny certyfikat SSL na stronie www
-----------------------------------------------------------------
.. index:: openssl,x509,rsa
.. code-block:: bash
   :linenos:

   echo | openssl s_client -servername NAME -connect uchacz.it:443 2>/dev/null | openssl x509 -noout -dates


Generowanie klucza prywatnego wraz CSR
---------------------------------------
.. index:: openssl,csr,rsa
.. code-block:: bash
   :linenos:

   # Generowanie klucz prywatnego
   openssl genrsa  -out uchacz.it.key 2048

   # Generowanie CSR na podstawie wygnerowanego klucza
   openssl req -new -key uchacz.it.key -out uchacz.it.csr

   #Country Name (2 letter code) [AU]:PL
   #State or Province Name (full name) [Some-State]:Dolnoslaskie
   #Locality Name (eg, city) []:Wroclaw
   #Organization Name (eg, company) [Internet Widgits Pty Ltd]:Uchacz Corp
   #Organizational Unit Name (eg, section) []:IT
   #Common Name (e.g. server FQDN or YOUR name) []:uchacz.it
   #Email Address []:ilovespam@uchacz.it

   # Sprawdzenie  CSR 
   openssl req -in uchacz.it.csr -noout -text | grep Subject    
   #Subject: C = PL, ST = Dolnoslaskie, L = Wroclaw, O = Uchacz Corp, OU = IT, CN = uchacz.it, emailAddress = ilovespam@uchacz.it

