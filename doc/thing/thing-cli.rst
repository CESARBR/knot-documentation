Using CLI
=========

.. note:: In order to use the KNoT CLI, it is necessary to fulfill the `requirements <thing-requirements.html>`_.

There are many commands that you can call when using the knot script (cli.py). Some of their functions are:

----------------------------------------------------------------

Set default target board
------------------------
- You can set the default target board with the command:

.. code-block:: bash

   $ knot board {BOARD}

.. note:: Currently, KNoT support ``dk`` (nrf52840_pca10056) or ``dongle`` (nrf52840_pca10059) board. Replace {BOARD} with one of them.

----------------------------------------------------------------

Set external OpenThread path
----------------------------

To avoid downloading the OpenThread repo on every new build, set an external path.

- Clone Openthread Github repository:

.. code-block:: bash

   $ git clone https://github.com/openthread/openthread.git


- Checkout to the compatible hash and set it as default:

.. code-block:: bash

   $ cd openthread
   $ git checkout -b knot_hash f9d757a161fea4775d033a1ce88cf7962fe24a93
   $ knot ot-path `pwd`

----------------------------------------------------------------

Clear project and building
--------------------------

.. warning:: The build command must be run from an application folder.

The user can delete old building files before compiling again.

.. note:: This is especially useful when the project had important changes like different target board or dependency repository.

- Clear old files and compiling:

.. code-block:: bash

   $ knot make --clean

----------------------------------------------------------------

Compile for your target board
-----------------------------

.. warning:: The build command must be run from an application folder.

Currently, KNoT supports ``dk`` (nrf52840_pca10056) or ``dongle`` (nrf52840_pca10059) board. Replace {BOARD} by one of them.

.. code-block:: bash

   $ knot make -b {BOARD}

.. note:: If you already set the default board is not necessary compile with -b option.

----------------------------------------------------------------

Flash board when done
---------------------

.. warning:: The build command must be run from an application folder.

The user can flash the board just after building it.

- Flash board after building:

.. code-block:: bash

   $ knot make --flash

.. note:: This option also flashes the bootloader when targeting the Dongle.

----------------------------------------------------------------

Flash bootloader
----------------

When using the DK, it's possible for the board to be flashed without the bootloader.
To fix that, the user should flash it separately.

- Flash bootloader to board:

.. code-block:: bash

   $ knot mcuboot

.. note:: This option also erases the main app when targeting the Dongle.

----------------------------------------------------------------

Other commands
--------------
These and the other commands are described when using the help command:

.. code-block:: bash

   $ knot --help
