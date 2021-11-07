Dyski
====================
.. index:: disk

Lvm
-------------------
.. index:: lvm
.. code-block:: bash
   :linenos:

   # Powiekszenie dysku lvm
     tune2fs /dev/bebok-vg/root  -l | grep resize_inode
     lvresize --resizefs --size +9GB /dev/vg/lv_home