Postgres
====================
.. index:: postgres


Ubijanie zapytań
-------------------
.. index:: pg_terminate_backend

.. code-block:: postgresql
   :linenos:

   # Zabije wszystko oprócz nas i siebie ( su - postgres -c psql )
   select pg_terminate_backend(pid) from pg_stat_activity where usename!='postgres';


Diagnostyka 
-------------------
.. index:: postgresql

.. code-block:: postgresql
   :linenos:

   # ilosc polaczen do bazy
   select count(*) from pg_stat_activity;

   # Zapytanie ktore trwaja dluzej niz 5 min
   select * from pg_stat_activity where query_start < now() - interval '5 minutes' and current_query ~ '^SELECT'


Odtworzenie bazy 
-----------------------------------
.. index:: pg_terminate_backend

.. code-block:: bash
   :linenos:

   # Zmiana użytkownika w dupmie
   pg_dump -s baza.dump  | grep -i 'owner to' | sed -e 's/OWNER TO .*;/ OWNER TO leszek;/i'

   # Odtworzenie bazy
   pg_restore -Fc baza.dump -O --role leszek -d mojabaza


Dokładniejsze informacje o kontach
-----------------------------------
.. index:: select

.. code-block:: postgresql
   :linenos:

   SELECT r.rolname, r.rolsuper, r.rolinherit,
				  r.rolcreaterole, r.rolcreatedb, r.rolcanlogin,
				  r.rolconnlimit, r.rolvaliduntil,
				  ARRAY(SELECT b.rolname
				        FROM pg_catalog.pg_auth_members m
				        JOIN pg_catalog.pg_roles b ON (m.roleid = b.oid)
				        WHERE m.member = r.oid) as memberof
				, r.rolreplication
				, r.rolbypassrls
				FROM pg_catalog.pg_roles r
				WHERE r.rolname !~ '^pg_'
				ORDER BY 1;

Wyświetlenie blokowanych zapytan
-----------------------------------
.. index:: deadlocks

.. code-block:: postgresql
   :linenos:
    
    SELECT blocked_locks.pid     AS blocked_pid,
         blocked_activity.usename  AS blocked_user,
         blocking_locks.pid     AS blocking_pid,
         blocking_activity.usename AS blocking_user,
         blocked_activity.query    AS blocked_statement,
         blocking_activity.query   AS current_statement_in_blocking_process
   FROM  pg_catalog.pg_locks         blocked_locks
    JOIN pg_catalog.pg_stat_activity blocked_activity  ON blocked_activity.pid = blocked_locks.pid
    JOIN pg_catalog.pg_locks         blocking_locks 
        ON blocking_locks.locktype = blocked_locks.locktype
        AND blocking_locks.DATABASE IS NOT DISTINCT FROM blocked_locks.DATABASE
        AND blocking_locks.relation IS NOT DISTINCT FROM blocked_locks.relation
        AND blocking_locks.page IS NOT DISTINCT FROM blocked_locks.page
        AND blocking_locks.tuple IS NOT DISTINCT FROM blocked_locks.tuple
        AND blocking_locks.virtualxid IS NOT DISTINCT FROM blocked_locks.virtualxid
        AND blocking_locks.transactionid IS NOT DISTINCT FROM blocked_locks.transactionid
        AND blocking_locks.classid IS NOT DISTINCT FROM blocked_locks.classid
        AND blocking_locks.objid IS NOT DISTINCT FROM blocked_locks.objid
        AND blocking_locks.objsubid IS NOT DISTINCT FROM blocked_locks.objsubid
        AND blocking_locks.pid != blocked_locks.pid
 
    JOIN pg_catalog.pg_stat_activity blocking_activity ON blocking_activity.pid = blocking_locks.pid
   WHERE NOT blocked_locks.GRANTED;

Odświeżenie widoków  
-----------------------------------
.. index:: refresh
.. code-block:: postgresql
   :linenos:

   
   # Wyświetlenie widoków 

   select schemaname as schema_name,
       matviewname as view_name,
       matviewowner as owner,
       ispopulated as is_populated,
       definition
    from pg_matviews
    order by schema_name,
         view_name;

   # Odświeżenie
   REFRESH MATERIALIZED VIEW view_products;


Uprawnienia
-----------------------------------
.. index:: grant,revoke

.. code-block:: postgresql
   :linenos:
    
   # Nadanie / odebranie
    GRANT CONNECT ON DATABASE mojabaza TO username;
    GRANT USAGE ON SCHEMA public TO username;
    GRANT SELECT ON table_name TO username;
    REVOKE ALL PRIVILEGES ON mojabaza from leszek;
   

Zmiana właściciela
-----------------------------------
.. index:: psql
.. code-block:: bash
   :linenos:

    for tbl in `psql -qAt -c "select tablename from pg_tables where schemaname = 'public';" YOUR_DB` ; do  psql -c "alter table \"$tbl\" owner to NEW_OWNER" YOUR_DB ; done
    for tbl in `psql -qAt -c "select sequence_name from information_schema.sequences where sequence_schema = 'public';" YOUR_DB` ; do  psql -c "alter table \"$tbl\" owner to NEW_OWNER" YOUR_DB ; done
    for tbl in `psql -qAt -c "select table_name from information_schema.views where table_schema = 'public';" YOUR_DB` ; do  psql -c "alter table \"$tbl\" owner to NEW_OWNER" YOUR_DB ; done
    for tbl in `psql -qAt -c "select table_name from information_schema.views where table_schema = 'public';" $db` ; do  psql -c "alter function  \"$tbl\" owner to $db" $db ; done


Insert/Update
-----------------------------------
.. index:: update, insert

.. code-block:: bash
   :linenos:
   
   Begin;
   UPDATE films SET kind = 'Dramatic' WHERE kind = 'Drama';
   Commit;
   
