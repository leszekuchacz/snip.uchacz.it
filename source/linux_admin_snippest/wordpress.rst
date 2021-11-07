Wordpress
====================
.. index:: wordpress




Dodanie użtkownika przez MySql w Wordpresie
--------------------------------------------
.. index:: mysql
.. code-block:: mysql
   :linenos:
   
   # Dodanie nowego użtkownika jako administrator
     INSERT INTO `databasename`.`wp_users` (`ID`, `user_login`, `user_pass`, `user_nicename`, `user_email`, `user_url`, `user_registered`, `user_activation_key`, `user_status`, `display_name`) VALUES ('4', 'demo', MD5('demo'), 'Leszek Uchacz', 'test@yourdomain.com', 'http://www.test.com/', '2011-06-07 00:00:00', '', '0', 'Your Name');

     INSERT INTO `databasename`.`wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`) VALUES (NULL, '4', 'wp_capabilities', 'a:1:{s:13:"administrator";s:1:"1";}');

     INSERT INTO `databasename`.`wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`) VALUES (NULL, '4', 'wp_user_level', '10');


Podmiana ścieżek absolutnych w Wordpresie
------------------------------------------
.. index:: mysql
.. code-block:: mysql
   :linenos:

   UPDATE wp_posts SET guid = replace(guid, '/var/www/stare/','/var/www/nowe/');

   UPDATE wp_posts SET post_content = replace(post_content, '/var/www/stare/','/var/www/nowe/');

   UPDATE wp_postmeta SET meta_value = replace(meta_value,'/var/www/stare/','/var/www/nowe/');

   UPDATE wp_options SET option_value = replace(option_value,'/var/www/stary','/var/www/nowy');



Podmiana ścieżek absolutnych w Wordpresie na dumpie od bazy
------------------------------------------------------------
.. index:: mysqldump, sed
.. code-block:: bash
   :linenos:

   mysqldump wordpress > w.sql
   sed -i w.sql -e 's#/var/www/stary/#/var/www/nowy/#g'
