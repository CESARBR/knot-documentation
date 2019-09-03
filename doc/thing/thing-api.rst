API Reference
=============

KNoT uses the concept of Data Items to define how a specified variable should be
tracked and/or updated.

The readings and writes to the target variable are done automatically by KNoT and
the fit callback functions are called if specified.

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

Data
----

``Data`` is a representation of a target variable that should be
tracked/updated by KNoT.
Each device can have as many Data items as limited by the setting
``CONFIG_KNOT_THING_DATA_MAX`` in the ``prj.conf`` file.

A Data item is identified by its id and can be only associated to a single
target variable.

----------------------------------------------------------------

knot_data_register()
--------------------

Registers a target variable that should be tracked/updated by KNoT.

.. code-block:: c

   int knot_data_register(u8_t id, const char *name,
                          u16_t type_id, u8_t value_type, u8_t unit,
                          void *target, size_t target_len,
                          knot_callback_t write_cb, knot_callback_t read_cb);

:Return:
   Returns the assigned id. Returns a negative number in case of failure.

:Parameters:
   - ``id``: Sensor/Actuator ID. Limited by CONFIG_KNOT_THING_DATA_MAX.
   - ``name``: Sensor/Actuator name.
   - ``type_id``: Type ID of KNoT data semantic.
   - ``value_type``: Value Type KNoT data semantic.
   - ``unit``: Unit of KNoT data semantic.
   - ``target``: Pointer to the target variable to be read/written by KNoT.
   - ``target_len``: Length of the target variable.
   - ``write_cb``: Optional callback to be called after writing to the target variable. It should be set to ``NULL`` if non-existent.
   - ``read_cb``: Optional callback to be called before reading the target variable. It should be set to ``NULL`` if non-existent.

.. note::
   Check valid combinations of type_id, value_type and unit in this
   `link <unit-type-value.html>`_.

----------------------------------------------------------------

knot_data_config()
------------------

This function defines which events should send the target value to cloud.

.. code-block:: c

   bool knot_data_config(u8_t id, ...);

:Return:
   Returns ``True`` if the setting was made correctly. ``False`` otherwise.

:Parameters:
   - ``id``: Sensor/Actuator ID.
   - ``...``: Optional list of event flags.

.. warning::
   This function must end with NULL

The ``event_flag`` parameter defines when (or why) you want it to send
information to the cloud.

   - By periods of time (KNOT_EVT_FLAG_TIME).
   - When the value is greater than a limit (KNOT_EVT_FLAG_LOWER_THRESHOLD).
   - When the value is lower than a limit (KNOT_EVT_FLAG_UPPER_THRESHOLD).
   - When the value changes (KNOT_EVT_FLAG_CHANGE).
   - Combinations of these.

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

knot_callback_t
---------------

Callbacks can be used to update the target variable before the KNoT Machine reads
it or to handle new changes made to it.

The return codes, ``KNOT_CALLBACK_SUCCESS`` and ``KNOT_CALLBACK_FAIL``, can be used
to sign if the callback was successfully executed.

.. note::
   In case of the Write Callback return failure, the old value will be restored
   to the target variable by the KNoT Machine.

   In case of the Read Callback return failure, the target variable will not be
   read by the KNoT Machine.
