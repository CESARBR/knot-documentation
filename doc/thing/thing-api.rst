API Reference
=============

setup() & loop()
----------------

Similar to Arduino the ``setup()`` function is called once and ``loop()`` is always called at idle state.
Sensors and actuators should be registered at ``setup()`` function.

.. code-block:: c

    void setup(void);
    void loop(void);

.. warning::

    ``loop()`` function must NOT be blocking.

----------------------------------------------------------------

struct knot_proxy
-----------------

``knot_proxy`` is a virtual representation of a Sensor/Actuator.
Contains identifier, data values and configuration values.

.. code-block:: c

   struct knot_proxy;

----------------------------------------------------------------

knot_proxy_register()
---------------------

Creates and tracks device changes a remote device (cloud).

.. code-block:: c

   struct knot_proxy *knot_proxy_register(u8_t id, const char *name,
				       u16_t type_id, u8_t value_type,
				       u8_t unit, knot_callback_t changed_cb,
				       knot_callback_t pool_cb);

:Return:
   Return the virtual representation ``knot_proxy``.

:Parameters:
   - ``id``: Sensor/Actuator ID.
   - ``name``: Sensor/Actuator name.
   - ``type_id``: Type ID of KNoT data semantic.
   - ``value_type``: Value Type KNoT data semantic.
   - ``unit``: Unit of KNoT data semantic.
   - ``changed_cb``: Callback function to write value on Sensor/Actuator.
   - ``pool_cb``: Callback function to read value from Sensor/Actuator.

.. note::
   Check valid combinations of type_id, value_type and unit in this
   `link <unit-type-value.html>`_.

----------------------------------------------------------------

knot_proxy_set_config()
-----------------------

This function configures which events should send proxy value to cloud.

.. code-block:: c

   bool knot_proxy_set_config(u8_t id, ...);

:Return:
   Returns ``True`` if the setting was made correctly. ``False`` otherwise.

:Parameters:
   - ``id``: Sensor/Actuator ID.
   - ``...``: Optional list of event flags.

.. warning::
   This function must end with NULL

The ``event_flag`` parameter define when (or why) you want it to send
information to the cloud.

   - By periods of time (KNOT_EVT_FLAG_TIME).
   - When the value is greater than a threshold (KNOT_EVT_FLAG_LOWER_THRESHOLD).
   - When the value is lower than a threshold (KNOT_EVT_FLAG_UPPER_THRESHOLD).
   - When the value changes (KNOT_EVT_FLAG_CHANGE).
   - Combinations of these (sum).

+-------------------------------+------------+------------------------------------------------+
| Flag Alias                    | | Flag     | Description                                    |
|                               | | Value    |                                                |
+===============================+============+================================================+
| KNOT_EVT_FLAG_TIME            |     1      | | Send data every period of time, in seconds.  |
|                               |            | | Needs a value greater than 0 to be passed    |
|                               |            | | on **time_sec**.                             |
+-------------------------------+------------+------------------------------------------------+
| KNOT_EVT_FLAG_LOWER_THRESHOLD |     2      | | Send data every time that the item is below  |
|                               |            | | a threshold. The value to be compared with   |
|                               |            | | is the one passed on **lower_limit**         |
|                               |            | | (lower_int + lower_dec). If combined with    |
|                               |            | | **KNOT_EVT_FLAG_UPPER_THRESHOLD**,           |
|                               |            | | it is mandatory that **lower_limit** is      |
|                               |            | | smaller than **upper_limit**.                |
+-------------------------------+------------+------------------------------------------------+
| KNOT_EVT_FLAG_UPPER_THRESHOLD |     4      | | Send data every time that the item is above  |
|                               |            | | a threshold. The value to be compared with   |
|                               |            | | is the one passed on **upper_limit**         |
|                               |            | | (upper_int + upper_dec). If combined with    |
|                               |            | | **KNOT_EVT_FLAG_LOWER_THRESHOLD**,           |
|                               |            | | it is mandatory that **lower_limit** is      |
|                               |            | | smaller than **upper_limit**.                |
+-------------------------------+------------+------------------------------------------------+
| KNOT_EVT_FLAG_CHANGE          |     8      | | Send data every time the item changes its    |
|                               |            | | value. Does not require any additional field.|
+-------------------------------+------------+------------------------------------------------+

----------------------------------------------------------------

knot_proxy_value_*()
--------------------

Proxy helpers to set or get sensor data at the remote.


knot_proxy_value_set_basic()
''''''''''''''''''''''''''''

This function is a proxy helper to set a new basic value on a ``knot_proxy``. Basic values are boolean, int or float.

.. code-block:: c

   bool knot_proxy_value_set_basic(struct knot_proxy *proxy,
                   const void *value);

:Return:
   True if the new value is sent. ``False`` otherwise.

:Parameters:
   - ``proxy``: Virtual representation of a Sensor/Actuator.
   - ``value``: Pointer to a boolean, int or float value that will be set.


knot_proxy_value_set_string()
'''''''''''''''''''''''''''''

This function is a proxy helper to set a string value on a ``knot_proxy``.

.. code-block:: c

   bool knot_proxy_value_set_string(struct knot_proxy *proxy,
                   const char *value, int len);

:Return:
   True if the new value is sent. ``False`` otherwise.

:Parameters:
   - ``proxy``: Virtual representation of a Sensor/Actuator.
   - ``value``: Pointer to char (array of char).
   - ``len``: The actual size of the string.


knot_proxy_value_get_basic()
''''''''''''''''''''''''''''

This function is a proxy helper to get a new basic value from a ``knot_proxy``. Basic values are boolean, int or float.

.. code-block:: c

   bool knot_proxy_value_get_basic(struct knot_proxy *proxy,
                   void *value);

:Return:
   True if successful. ``False`` otherwise.

:Parameters:
   - ``proxy``: Virtual representation of a Sensor/Actuator.
   - ``value``: Pointer to a boolean, int or float to put the get value.


knot_proxy_value_get_string()
'''''''''''''''''''''''''''''

This function is a proxy helper to get a new string value from a ``knot_proxy``.

.. code-block:: c

   bool knot_proxy_value_get_string(struct knot_proxy *proxy,
                   char *value, int len, int *olen);

:Return:
   True if successful. ``False`` otherwise.

:Parameters:
   - ``proxy``: Virtual representation of a Sensor/Actuator.
   - ``value``: Pointer to char (array of char).
   - ``len``: The actual size of the string.
   - ``olen``: The address of a variable to save the size of the string.
