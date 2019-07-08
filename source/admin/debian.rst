Debian
====================
.. index:: debian
.. contents: Uzyteczne komendy  do Debiana

Swap
-------------------
.. index:: swap
.. code-block:: bash
   :linenos:

   # Czyszczenie swapa
     swapoff --all && sysctl vm.swappiness=0 && swapon --all

   # Sprawdzenie co siedzi w swapie
     for x in /proc/*/smaps; do awk -- '/Swap:/ { s = s + $2 } END { print ARGV[1] " " s }' $x; done  | sort -nk 2|tail


Proc
-------------------
.. index:: proc
.. code-block:: bash
   :linenos:

   # Force  restart systemu 
     echo 1 > /proc/sys/kernel/sysrq