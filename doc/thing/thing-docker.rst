Using Docker
============

The Docker image can be used to ease building new apps using a pre-configured
environment.

It supports Docker for Mac, Linux and Windows.

To build or run the image, you have to `install Docker <https://docs.docker.com/install/>`_.

----------------------------------------------------------------

Building image
--------------

Build it by the tag `knot-zephyr-sdk`.

.. code-block:: bash

   $ docker build --tag=knot-zephyr-sdk .

----------------------------------------------------------------

Running the container
---------------------

Run the latest image version at CESAR's Docker Hub and pass the current working
directory as the project folder.
This folder shall contain all your project files.

At your project folder, run:

.. code-block:: bash

   $ docker run -ti -v $(pwd)/:/workdir cesarbr/knot-zephyr-sdk:latest

If you want to run it from an image you built, replace `cesarbr/knot-zephyr-sdk:latest`
by the tag you used.

----------------------------------------------------------------

Compile for your target board
-----------------------------

Inside the docker container, use the KNoT script to compile your project.

.. code-block:: bash

   [user@container] $ sudo -E knot make -b {BOARD}

.. note:: Currently, KNoT support ``dk`` (nrf52840_pca10056) or ``dongle`` (nrf52840_pca10059) board. Replace {BOARD} with one of them.

----------------------------------------------------------------

Flashing
--------

Has two ways to flash the board, using nRF Connect application or Using KNoT CLI application (if on Linux).

First of all, connect the board to a USB port.

Using nRF Connect
'''''''''''''''''

Export the generated files to your project's directory

.. code-block:: bash

   [user@container] $ sudo -E knot export /workdir/output

The generated files can now be flashed to your device by using the
`nRF Connect for Desktop <https://www.nordicsemi.com/?sc_itemid=%7B49D2264D-62FD-4C16-811F-88B477833C5D%7D>`_ and its
`Programmer app <https://infocenter.nordicsemi.com/topic/ug_nc_programmer/UG/nrf_connect_programmer/ncp_introduction.html>`_.

On Programmer App:

   1 - Select the board.

   2 - On Add HEX file, include ``boot_sgn_apps.hex`` file.

   3 - Click on Write to flash the board.

Using KNoT CLI on Linux
'''''''''''''''''''''''

If using a Linux host with the necessary drivers for flashing the boards,
you may give USB access to the container.

Before proceeding, make sure that you added your user to the dialout group.

.. code-block:: bash

   $ sudo usermod -a -G dialout `whoami`

You can now access the container using the host `/dev` directory.

.. code-block:: bash

   $ docker run -ti --privileged -v /dev:/dev -v $(pwd)/:/workdir cesarbr/knot-zephyr-sdk:latest

This will allow you to use the `--flash` flag to flash after building the project.

.. code-block:: bash

   [user@container] $ sudo -E knot make -b {BOARD} --mcuboot

.. note:: Currently, KNoT support ``dk`` (nrf52840_pca10056) or ``dongle`` (nrf52840_pca10059) board. Replace {BOARD} with one of them.

----------------------------------------------------------------

Using other knot commands
----------------------------

When inside the Docker container, you may use any KNoT command from the command line interface.

To get a list of all available commands, run:

.. code-block:: bash

   [user@container] $ knot --help

More info is available at the `Thing CLI doc section <thing-cli.html>`_.
