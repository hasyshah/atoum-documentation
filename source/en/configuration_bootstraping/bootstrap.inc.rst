
.. _bootstrap_file:

Bootstrap file
**************

atoum allows the definition of a ``bootstrap`` file, which will be run before each test method and which therefore allows to initialize the test execution environment.

The default name of the file is ``.bootstrap.atoum.php``, atoum will load it automatically if this file is located in the current directory. You can define it through the cli with ``-bf`` or ``--bootstrap-file``.

This makes possible to define, for example, the reading of a configuration file or perform any other operation necessary for the proper execution of the tests.

The definition of this bootstrap file can be done in two different ways, either in command line, or via a configuration file.

.. code-block:: shell

   $ ./bin/atoum -bf path/to/bootstrap/file

.. note::
   A bootstrap file is not a :ref:`configuration file<fichier-de-configuration>` file and therefore does not have the same opportunities.

In a configuration file, atoum is configurable via the ``$runner`` variable, which is not defined in a ``bootstrap`` file.

Moreover, they are not included at the same time, since the configurations file is included by atoum before the tests run but after tests launch, while the ``bootstrap``, if it's define, is the first file included by atoum itself. Finally, the ``bootstrap`` file can allow to not have to systematically include the ``scripts/runner.php`` file or atoum PHAR archive in test classes.
However, in this case, it will not be possible to directly execute a test file directly from the PHP executable in command line.
To do this, simply include in the ``bootstrap`` the file ``scripts/runner.php`` or PHAR archive of atoum and systematically execute tests by command line via ``scripts/runner.php`` or PHAR archive.

Therefore, the ``bootstrap`` file must at least contain this:

.. code-block:: php

   <?php

   // if the PHAR archive is used:
   require_once path/to/atoum.phar;

   // or if sources is used and you want to load the $runner
   // require_once path/atoum/scripts/runner.php
