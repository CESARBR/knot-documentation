Requirements
============

Linux based OS
--------------

The actual version of KNoT Zephyr SDK is only available for Linux based systems.
On other systems, you may consider using the `KNoT Docker <thing-docker.html>`_ (recommended) or a Virtual Machine running a Linux distribution.

----------------------------------------------------------------

Zephyr
------

KNoT uses a fork of Zephyr repository.

- Set up a Zephyr development environment by following these `instructions <https://docs.zephyrproject.org/latest/getting_started/installation_linux.html>`_.

- Program the ``$HOME/.profile`` to always set **ZEPHYR_TOOLCHAIN_VARIANT** and **ZEPHYR_SDK_INSTALL_DIR**.

.. code-block:: bash

   $ echo "export ZEPHYR_TOOLCHAIN_VARIANT=zephyr" >> $HOME/.profile
   $ echo "export ZEPHYR_SDK_INSTALL_DIR=`readlink -f <SDK-INSTALLATION-DIRECTORY>`" >> $HOME/.profile

.. note:: Replace ``<SDK-INSTALLATION-DIRECTORY>`` by the actual Zephyr SDK install path

- Install the west binary and bootstrapper

.. code-block:: bash

   $ pip3 install --user west

- Create an enclosing folder and change directory

.. code-block:: bash

   $ mkdir zephyrproject
   $ cd zephyrproject

- Clone KNoT Zephyr fork

.. code-block:: bash

   $ git clone -b zephyr-knot-v1.14.0 https://github.com/CESARBR/zephyr.git

- Initialize west. Inside zephyrproject directory run:

.. code-block:: bash

   $ west init -l zephyr/
   $ west update

.. note:: If the system can't find west, try logging out and in again.

- Set up zephyr environment variables

.. code-block:: bash

   $ source zephyr/zephyr-env.sh

- Program the ``$HOME/.profile`` to always source zephyr-env.sh when you log in.

.. code-block:: bash

   $ echo "source $ZEPHYR_BASE/zephyr-env.sh" >> $HOME/.profile

.. note:: If you skip this step, it will be necessary to manually source zephyr-env.sh every time a new terminal is opened.

----------------------------------------------------------------

nRF5x Command Line Tools and Segger JLink
-----------------------------------------

- Download and extract cli applications at `nRF5 Command Line Tools <https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF5-Command-Line-Tools>`_.

- Install nRF5x Command Line and Segger JLink deb package:

.. code-block:: bash

   $ dpkg -i nrf5_tools/nRF-Command-Line-Tools_10_2_1_Linux-amd64.deb
   $ dpkg -i nrf5_tools/JLink_Linux_V644e_x86_64.deb

----------------------------------------------------------------

Source KNoT environment configuration file
------------------------------------------

- Download the zephyr-knot-sdk repository to a folder you prefer.

.. code-block:: bash

   $ git clone https://github.com/cesarbr/zephyr-knot-sdk/

- The environment configuration file is used to set up **KNOT_BASE** path.

.. code-block:: bash

   $ source zephyr-knot-sdk/knot-env.sh

- Program the ``$HOME/.profile`` to always source knot-env.sh when you log in.

.. code-block:: bash

   $ echo "source $KNOT_BASE/knot-env.sh" >> $HOME/.profile

----------------------------------------------------------------

Add support to the KNoT command line interface
----------------------------------------------

- Add cli.py to the path files.

.. code-block:: bash

   $ ln -s $KNOT_BASE/scripts/cli.py $HOME/.local/bin/knot

.. note:: This will allow you to call the knot command line interface from any folder.

- Use pip to install cli requirements

.. code-block:: bash

   $ pip3 install --user -r ${KNOT_BASE}/scripts/requirements.txt

.. note:: If you skip this step, it will be necessary to manually source knot-env.sh every time a new terminal is opened.

----------------------------------------------------------------

KNoT protocol
-------------

- Follow the instructions to install the `KNoT protocol library <https://github.com/CESARBR/knot-protocol-source>`_.

----------------------------------------------------------------

Add USB access to your user
---------------------------

- Add your user to the dialout group.

.. code-block:: bash

   $ sudo usermod -a -G dialout `whoami`

----------------------------------------------------------------

Apply changes to profile
------------------------

- In order to apply the changes to your user, you must log out and log in again.
