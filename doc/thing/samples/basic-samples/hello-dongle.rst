hello-dongle
============

Overview
--------

The hello-dongle example for ``dongle`` (nrf52840_pca10059) uses an on-board LED connected blinking every 2 seconds.
This sample is focused on show how to register a LED as a boolean sensor using KNoT Zephyr SDK.

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

.. note:: Before proceeding, make sure the device is in DFU mode.

This sample can be flashed to a board as follows:

- Using the KNoT Zephyr SDK on your machine:

   Follow the steps described on `KNoT CLI section. <../../thing-cli.html#flash-board-when-done>`_

- Using the KNoT Docker:

   Follow the steps described on `KNoT Docker section. <../../thing-docker.html#flashing>`_

----------------------------------------------------------------

Configuring
-----------

After flashing, use the Android KNoT Setup App for configuring the Gateway credentials on your thing.
