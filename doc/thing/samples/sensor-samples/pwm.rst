pwm
===

Overview
--------

The pwm example blinks a led using pwm. The purpose of this is sample is to
show how to use pwm in Zephyr.

-------------------------------------------------------------------------------

Requirements
------------

The demo assumes that the positive terminal of a led is connected to the pin
specified down below:

- 0.13 pin (for KNoT DK and Dongle)

KNoT DK already has an on board led connected to 0.13 pin.
The negative terminal of the led should be connected to a 220 ohms resistor and
the other resistor terminal should be connected to board GND.

-------------------------------------------------------------------------------

.. include:: ../thing-sample-body.rst
