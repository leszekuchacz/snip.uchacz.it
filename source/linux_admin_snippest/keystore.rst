Keystore
====================
.. index:: keystore
.. contents: Uzyteczne komendy  do keystore



Stworzenie keystore z Let's Encrypt
----------------------------------------
.. index:: letsencrypt,keystore,cat,openssl,pkcs12,x509
.. code-block:: bash
   :linenos:

   cat letsencrypt.ca.pem > fullchain.pem

   cat uchacz.it.pem >> fullchain.pem

   openssl pkcs12 -export -out keystore.pkcs12 -in fullchain.pem -inkey uchacz.it.key  -passout pass:haslo

   /opt/JDK_8u121/bin/keytool -importkeystore -srckeystore keystore.pkcs12 -srcstoretype PKCS12 -destkeystore keystore.jks -srcstorepass haslo -storepass haslo -noprompt


Odczarowanie keystore
----------------------------------------
.. index:: letsencrypt,keystore,openssl,pkcs12,x509
.. code-block:: bash
   :linenos:

    # Konwersja  jks  to p12
    /opt/JDK_8u121/bin/keytool -importkeystore -srckeystore keystore.jks -destkeystore keystore.p12 -deststoretype PKCS12
	
    # Wyświetlenie zawartości
    /opt/JDK_8u121/bin/keytool -deststoretype PKCS12 -keystore keystore.p12 -list
	
    # Wyciągniecie z p12 certyfikatów pem
    openssl pkcs12 -nokeys -in keystore.p12 -out cert.pem
	
    # Wyciągniecie z p12 klucza prywatnego
    openssl pkcs12 -nocerts -nodes -in keystore.p12 -out private.key
