Jinja2
====================
.. index:: Ansible


If 
-----------------------------------
.. index:: jinja2

.. code-block:: bash
   :linenos:

	{% if inventory_hostname  in  groups['qa-hosts'] or inventory_hostname in  groups['prprod-hosts'] %}
    {% elif .... %}
    {% endif %}