dht
===

Overview
--------

The dht example reads ambient temperature and relative humidity measured by a
DHT11 or DHT22 sensor. The purpose of this sample is to show how to use a
sensor that is already covered by Zephyr sensors library.

-------------------------------------------------------------------------------

Requirements
------------

The demo assumes that sensor data pin is connected to the 1.15 pin.
Make sure to use VDD OUT as the positive reference and GND as the negative
reference.
DHT11/22 datasheet recommends the use of a 10k resistor between VCC and data
pin.

-------------------------------------------------------------------------------

.. include:: ../thing-sample-body.rst
