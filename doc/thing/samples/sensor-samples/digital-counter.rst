digital-counter
===============

Overview
--------

The digital-counter example reads a digital sensor and counts how many times the sensor was triggered.
It lights an LED for 1 second when the sensor is triggered.

----------------------------------------------------------------

Requirements
------------

The demo assumes that a digital output is connected to pin 0.10.

----------------------------------------------------------------

Building
--------

This sample can be built for your board in two different ways.

- Using the KNoT Zephyr SDK installed on your machine:

   Follow the steps described on `KNoT CLI section. <../../thing-cli.html#compile-for-your-target-board>`_

- Using the KNoT Docker:

   Follow the steps described on `KNoT Docker section. <../../thing-docker.html#compile-for-your-target-board>`_

----------------------------------------------------------------

Flashing
--------

.. note:: If you are flashing the ``dongle`` (nrf52840_pca10059) board, make sure the device is in DFU mode before proceeding.

This sample can be flashed to a board as follows:

- Using the KNoT Zephyr SDK on your machine:

   Follow the steps described on `KNoT CLI section. <../../thing-cli.html#flash-board-when-done>`_

- Using the KNoT Docker:

   Follow the steps described on `KNoT Docker section. <../../thing-docker.html#flashing>`_

----------------------------------------------------------------

Configuring
-----------

After flashing, use the Android KNoT Setup App for configuring the Gateway credentials on your thing.
