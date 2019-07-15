Create an Application
=====================

A general application for a KNoT Thing has the following structure:

.. code-block:: bash

   <app-name>/
    ├── CMakeLists.txt
    ├── prj.conf
    ├── setup.conf
    └── src/
        └── <app-name>.c

Let's see what each file does.

----------------------------------------------------------------

CMakeLists.txt
--------------

CMakeLists.txt is a configuration file for CMake. It contains a set of directives and instructions describing the project's source files and targets.

Below you can see a CMakeLists.txt from a simple KNoT project.

.. code-block:: text
   :linenos:

   cmake_minimum_required(VERSION 3.8.2)

   if (NOT DEFINED ENV{KNOT_BASE})
      message(FATAL_ERROR "Source the KNoT shell initialize script!")
   endif()

   include($ENV{KNOT_BASE}/core/CMakeLists.txt)
   project(<app-name>)

   FILE(GLOB app_sources src/*.c)
   target_sources(app PRIVATE ${app_sources})

You must change the <app-name> for your project name on ``line 8``.

----------------------------------------------------------------

prj.conf
--------

The prj.conf file is a configuration file that contains information about KNoT Zephyr project.

The name of the Device, the number of sensors/actuators the device has, logging configuration and sensors/actuators configuration are placed in this file. 

Below you can see a prj.conf from a simple KNoT project.

.. code-block::
   :linenos:

   # KNoT
   CONFIG_KNOT_NAME="<device-name>>"
   CONFIG_KNOT_THING_DATA_MAX=1

   # Logging
   CONFIG_LOG=y
   CONFIG_LOG_IMMEDIATE=n
   CONFIG_KNOT_LOG=y
   CONFIG_KNOT_LOG_LEVEL_DEBUG=y
   CONFIG_PRINTK=y

Change the name of your device (``line 2``) and the maximum number of sensors you are using (``line 3``).

----------------------------------------------------------------

setup.conf
----------

setup.conf is a configuration file tha contains information about bluetooth configuration.

.. code-block::
   :linenos:

   CONFIG_BT_DEVICE_NAME="BLE device name"

Change the name of bluetooth advertise name (``line 1``).

----------------------------------------------------------------

src/<app-name>.c
----------------

The <app-name>.c contains the application main code.

It is structured by two basic functions, `setup() and loop() <thing-api.html#setup-loop>`_.

You can see a start code example bellow.

.. code-block:: c
   :linenos:

   #include <zephyr.h>
   #include <net/net_core.h>
   #include <logging/log.h>
   #include <device.h>
   #include <gpio.h>

   #include "knot.h"
   #include <knot/knot_types.h>
   #include <knot/knot_protocol.h>

   void setup(void)
   {

   }

   void loop(void)
   {

   }

On ``loop()`` function you can include your application logic.

.. warning::

    ``loop()`` function must NOT be blocking.

On ``setup()`` you can register your sensors/actuators using `knot_proxy_register() <thing-api.html#knot-proxy-register>`_ and configures which events should send data to cloud with `knot_proxy_set_config() <thing-api.html#knot-proxy-set-config>`_.

For each registered sensor/actuator you may want to create a ``changed_cb`` or ``pool_cb`` function, this function are passed as callback on `register <thing-api.html#knot-proxy-register>`_ function.

**Example** (`hello-dongle <samples/basic-samples/hello-dongle.html>`_):

.. code-block:: c
   :linenos:

   void setup(void)
   {
      /* Peripherals control */
      gpio_led = device_get_binding(LED_PORT);
      gpio_pin_configure(gpio_led, LED_PIN, GPIO_DIR_OUT);

      /* KNoT config */
      knot_proxy_register(0, "LED", KNOT_TYPE_ID_SWITCH,
               KNOT_VALUE_TYPE_BOOL, KNOT_UNIT_NOT_APPLICABLE,
               write_led, read_led);

      knot_proxy_set_config(0, KNOT_EVT_FLAG_CHANGE, NULL);

   }

In this example a LED Sensor is registered with:

   - id = 0;
   - name = LED;
   - type_id = KNOT_TYPE_ID_SWITCH;
   - value_type = KNOT_VALUE_TYPE_BOOL;
   - unit = KNOT_UNIT_NOT_APPLICABLE;
   - changed_cb = write_led;
   - pool_cb = read_led;

And it is configured to send message to Cloud every time the value changes.

 - The ``changed_cb`` function gets a value for a `knot_proxy <thing-api.html#struct-knot-proxy>`_ and it can set on a sensor/actuator.
 - The ``pool_cb`` function sets information of sensor/actuator on a `knot_proxy <thing-api.html#struct-knot-proxy>`_.

.. code-block:: c
   :linenos:

   void write_led(struct knot_proxy *proxy)
   {
      knot_proxy_value_get_basic(proxy, &led);

      gpio_pin_write(gpio_led, LED_PIN, !led); /* Led is On at LOW */
   }

   void read_led(struct knot_proxy *proxy)
   {
      knot_proxy_value_set_basic(proxy, &led);
   }
