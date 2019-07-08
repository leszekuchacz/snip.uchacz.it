Influxdb
====================
.. index:: influxdb
.. contents: Uzyteczne komendy  do influxdb

Podstawowe komendy influx
--------------------------
.. index:: influx
.. code-block:: bash
   :linenos:

   # Komenda influx
     influx
      show databases
      use db
      SHOW MEASUREMENTS
      list series
	
    # Wyczyszczenie całej bazy
      DROP SERIES FROM /.*/
	
    # Wyczyszczenie od danej daty
      DELETE WHERE time < '2019-06-18';
      DELETE WHERE time < now() - 7d
	
    # retecja danych
      show retention policies on collectd_db
      CREATE RETENTION POLICY oneweek on collectd_db DURATION 7d REPLICATION 1;