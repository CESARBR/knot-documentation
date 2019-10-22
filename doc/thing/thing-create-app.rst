Create an Application
=====================

A general application for a KNoT Thing has the following structure:

.. code-block:: bash

   <app-name>/
    ├── CMakeLists.txt
    ├── prj.conf
    ├── setup.conf
    ├── <board>.overlay (optional)
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
   CONFIG_LOG_PRINTK=y

Change the name of your device (``line 2``) and the maximum number of sensors you are using (``line 3``).

.. note:: The CONFIG_PRINTK option may not work as expected on `KNoT Dongle
          <supported-boards/knot-dongle.html>`_. You still can use the
          CONFIG_LOG_PRINTK with all `supported boards
          <thing-supported-boards.html>`_.

----------------------------------------------------------------

setup.conf
----------

setup.conf is a configuration file tha contains information about bluetooth configuration.

.. code-block::
   :linenos:

   CONFIG_BT_DEVICE_NAME="BLE device name"

Change the name of bluetooth advertise name (``line 1``).

----------------------------------------------------------------

<board>.overlay (optional)
--------------------------

It is possible to use a DTS overlay file on the project by adding a file named
<board>.overlay and placing it on the application main directory.

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

Use ``loop()`` function to include your application logic.

.. warning::

    ``loop()`` function must NOT be blocking.

Use ``setup()`` to register your sensors/actuators using
`knot_data_register() <thing-api.html#knot-data-register>`_ and configure
which events should send data to cloud with `knot_data_config()
<thing-api.html#knot-data-config>`_.

For each registered sensor/actuator you may want to create a ``write_cb`` or
``read_cb`` function, which will be passed as callbacks on
`register <thing-api.html#knot-data-register>`_ function.

**Example** (`blink <samples/basic-samples/blink.html>`_):

.. code-block:: c
   :linenos:

   void setup(void)
   {
      /* Peripherals control */
      gpio_led = device_get_binding(LED_PORT);
      gpio_pin_configure(gpio_led, LED_PIN, GPIO_DIR_OUT);

      /* KNoT config */
      knot_data_register(0, "LED", KNOT_TYPE_ID_SWITCH,
               KNOT_VALUE_TYPE_BOOL, KNOT_UNIT_NOT_APPLICABLE,
               &led, sizeof(led),
               write_led, read_led);

      knot_data_config(0, KNOT_EVT_FLAG_CHANGE, NULL);

   }

In this example a LED Sensor is registered with:

   - id = 0;
   - name = LED;
   - type_id = KNOT_TYPE_ID_SWITCH;
   - value_type = KNOT_VALUE_TYPE_BOOL;
   - unit = KNOT_UNIT_NOT_APPLICABLE;
   - variable_address = &led;
   - variable_size = sizeof(led);
   - write_cb = write_led;
   - read_cb = NULL;

And it is configured to send message to Cloud every time the value changes.

 - ``write_cb``: This function is used to write in the actuator the value of
   the associated variable. It is executed after the variable value is updated
   remotely.
 - ``read_cb``: This function is used to write the value read from the sensor
   into the variable. It is executed in polling.

.. code-block:: c
   :linenos:

   int write_led(int id)
   {
      gpio_pin_write(gpio_led, LED_PIN, !led); /* Led is On at LOW */

      return KNOT_CALLBACK_SUCCESS;
   }
