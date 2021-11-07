Ruby
====================
.. index:: ruby
.. contents: Uzyteczne komendy  do Ruby

Zarzadzanie pakietami ruby 
---------------------------
.. index:: gem
.. code-block:: bash
   :linenos:

    # Odinstalowanie wszystkich wersji pakietu rjb
      gem cleanup rjb
      gem uninstall rjb

    # Odinstaluje tylko wersje 1.1.9 
      gem uninstall rjb --version 1.1.9

    # Odinstaluje wesje mniejsze od 1.3.4
      gem uninstall rjb --version '<1.3.4'

    
Znane problemy
---------------------------
.. index:: gem
.. code-block:: bash
   :linenos:

   # bląd require': cannot load such file -- elif
      gem install elif