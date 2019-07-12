Quick Start Guide
=================

This guide will help you to set up thing's development environment, then build and run a thing application.

----------------------------------------------------------------

Thing's Development Environment
-------------------------------

The fastest way to use or to develop for KNoT thing is to use the `KNoT Thing Docker container <../thing/thing-docker.html>`_.

Another way is to get the KNoT Thing source code by following all steps listed on `requirements <../thing/thing-requirements.html>`_.

After this set up, it will be possible to use the `KNoT CLI application <../thing/thing.cli.html>`_.

----------------------------------------------------------------

KNoT Thing Hello World
----------------------

Connect and set the target board
''''''''''''''''''''''''''''''''

You may be using one of the two supported boards: DK (nrf52840_pca10056) or Dongle (nrf52840_pca10059).

   - If using the DK:

      - Connect the board to a USB port.
      - Set the DK as the default target board.

      .. code-block:: bash

         $ knot board dk

   - If using the Dongle:

      - Connect the board to a USB port.
      - Press the reset button. The red led will blink.
      - Set the Dongle as the default target board.

      .. code-block:: bash

         $ knot board dongle

Build KNoT Hello App
''''''''''''''''''''

- Go to the KNoT Hello directory.

   .. code-block:: bash

      $ cd $KNOT_BASE/apps/hello

.. note:: If you are using the Dongle go to hello-dongle directory.

- Build and flash apps.

   .. code-block:: bash

      $ knot make --mcuboot

.. note:: The option 'mcuboot' flashes the compiled program and the mcuboot bootloader at the end of building.

Monitor the output
''''''''''''''''''

You can use minicom or any other serial port reader to monitor the app output.

- Install minicom

.. tip:: You can install minicom on debian based systems by using: ``$ sudo apt-get install minicom``

.. code-block:: bash

   $ minicom -D <your-device>

.. tip:: If you are using debian the device usually is something like /dev/ttyACM0.

----------------------------------------------------------------

KNoT Setup App
--------------

Considering the KNoT Gateway is configured.

You may use the `mobile KNoT Setup App <../app-setup/app-setup.html>`_ to configure the thing network.

After a successful thing configuration, **reset the board**.

----------------------------------------------------------------

Connected Thing
---------------

If all the steps were followed correctly, will be possible to see the KNoT Dongle connected on KNoT WebUI.

.. image:: ../../_static/webui_devices.png
   :scale: 100 %
   :alt: WebUI connected devices
   :align: center

----------------------------------------------------------------

KNoT Cloud SDK
--------------

To interact with data from device, utilize KNoT Cloud SDK to construct a User Application.
