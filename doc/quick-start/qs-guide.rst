Quick Start Guide
=================

This guide will help you to set up thing's development environment, then build and run a thing application.

----------------------------------------------------------------

Configuring the KNoT Gateway
----------------------------

Flashing the KNoT Gateway
'''''''''''''''''''''''''

Execute the following steps if you have a Raspberry Pi that is not flashed with a KNoT Gateway image.

You will need an SD Card reader to install the image.

#. Download the gateway image (``.img`` file) for your gateway from the `releases webpage <https://knot-devel.cesar.org.br/releases/latest/>`_.

#. Download and install `balenaEtcher <https://www.balena.io/etcher/>`_.

#. Connect an SD card to your computer.

#. Open balenaEtcher and select the downloaded ``.img`` file.

#. Select the target SD card.

#. Flash it.

#. Connect the SD card to your gateway.

You now have a flashed KNoT Gateway! Let's configure it!

.. note:: Experienced users may follow `Raspberry Pi's official installing tutorial <https://www.raspberrypi.org/documentation/installation/installing-images/>`_
          for more flashing options.


Adding Gateway to KNoT Cloud
''''''''''''''''''''''''''''

#. Connect the KNoT Gateway to the same network as your computer (by using an ethernet cable).

#. Access the gateway with `<http://knot.local>`_ and start the setup wizard.

   .. figure:: ../../_static/gateway_setup_wizard.png
      :scale: 70 %
      :alt: Gateway: Setup Wizard
      :align: center

#. Use the default cloud settings and proceed.

   .. figure:: ../../_static/gateway_setup_cloud.png
      :scale: 50 %
      :alt: Gateway: Cloud setup
      :align: center

#. Create your KNoT Cloud user and sign in to it.

   .. figure:: ../../_static/gateway_setup_signin.png
      :scale: 70 %
      :alt: Gateway: Sign in to cloud
      :align: center

#. Create a new gateway at the cloud and name it.

   .. figure:: ../../_static/gateway_setup_name.png
      :scale: 70 %
      :alt: Gateway: Create new gateway
      :align: center

#. Wait for the gateway to reboot.

#. Log in with the email and password you just signed up at `KNoT Cloud <https://knot.cloud>`_.

   .. figure:: ../../_static/gateway_signin.png
      :scale: 70 %
      :alt: Gateway: Sign in
      :align: center

   .. note:: As there are no KNoT Things connected to your gateway, the message `"No nearby devices found."` will be displayed


----------------------------------------------------------------

Thing's Development Environment
-------------------------------
In order to compile and flash applications for the KNoT Thing, it's necessary to set up the development environment.

The fastest way to do it is by using a pre-built Docker image.

#. Download and install `Docker <https://docs.docker.com/install/>`_.

#. In a terminal, get the latest KNoT Thing SDK Docker environment image.

   .. code-block:: bash

      docker pull cesarbr/knot-zephyr-sdk:latest

.. note:: Docker is only available for Linux based systems, macOS 10.11+ and Windows 10 Pro/Enterprise.

----------------------------------------------------------------

Programming the KNoT Thing
--------------------------

Compiling project
'''''''''''''''''

#. Clone the `zephyr-knot-sdk repository <https://github.com/CESARBR/zephyr-knot-sdk>`_ to your home folder.

   .. code-block:: bash

      git clone https://github.com/CESARBR/zephyr-knot-sdk.git ~/zephyr-knot-sdk

#. Navigate to the application project directory.

   .. code-block:: bash

      cd ~/zephyr-knot-sdk/apps/hello-dongle

#. Run environment image.

   .. code-block:: bash

      docker run -ti -v $(pwd)/:/workdir cesarbr/knot-zephyr-sdk:latest

#. From the container, build the project for the target board.

   - If using the `KNoT DK <https://docs.zephyrproject.org/latest/boards/arm/nrf52840_pca10056/doc/index.html>`_:

      .. code-block:: bash

         [user@container] $ knot make --board dk

   - If using the `KNoT Dongle <https://docs.zephyrproject.org/latest/boards/arm/nrf52840_pca10059/doc/index.html>`_:

      .. code-block:: bash

         [user@container] $ knot make --board dongle


Flashing board
''''''''''''''

#. From your project folder, export the generated files to a ``output`` folder.

   .. code-block:: bash

      [user@container] $ knot export output/

#. Install `nRF Connect <https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF-Connect-for-desktop/Download>`_.

#. Open *nRF Connect* and add the *Programmer App*.

   .. figure:: ../../_static/nrfconnect_add_programmer.png
      :scale: 70 %
      :alt: nRF Connect: Add Programmer
      :align: center

#. Launch the *Programmer App*.

   .. figure:: ../../_static/nrfconnect_launch_programmer.png
      :scale: 70 %
      :alt: nRF Connect: Launch Programmer
      :align: center

#. Connect the device to a USB port.

   .. tip:: If using the `KNoT Dongle <https://docs.zephyrproject.org/latest/boards/arm/nrf52840_pca10059/doc/index.html>`_, press the *RESET* button to get into DFU mode.
      The red LED will start to blink.

#. Select the target device.

   .. figure:: ../../_static/nrfconnect_select_device.png
      :scale: 70 %
      :alt: nRF Connect: Select device
      :align: center

#. Define the HEX file to be flashed.

   Click **Add HEX file** and select the ``boot_sgn_apps.hex`` file that was exported to the ``output/`` folder.

   .. figure:: ../../_static/nrfconnect_add_hex.png
      :scale: 70 %
      :alt: nRF Connect: Add HEX file
      :align: center

   .. note:: The path for the hex file should be ``~/zephyr-knot-sdk/apps/hello-dongle/output/boot_sgn_apps.hex``.

#. Flash the project.

   Click **Write** and wait for the board to be flashed. The red LED will stop blinking for the Dongle.

----------------------------------------------------------------

Configuring the Thing network
-----------------------------

In this section we are going to configure the Thing to automatically connect to the Gateway mesh network.

#. Make sure that the device Thing is on the `Setup Mode`, indicated by the alternating LEDs.

   .. figure:: ../../_static/dongle_setup.gif
      :scale: 130 %
      :alt: KNoT Dongle: Setup mode
      :align: center

      KNoT Dongle: Setup mode

   .. figure:: ../../_static/dk_setup.gif
      :scale: 70 %
      :alt: KNoT DK: Setup mode
      :align: center

      KNoT DK: Setup mode

#. Download the `mobile KNoT Setup App <https://knot-devel.cesar.org.br/releases/latest/knot_setup_app.apk>`_ and install it to your smartphone (Android only).

#. Connect your smartphone to the same Wi-Fi network that you connected your Gateway to.

#. Open the KNoT Setup App, and select your gateway under the *Connected* tab

   .. figure:: ../../_static/android_gateways_connected.png
      :scale: 20 %
      :alt: Setup App: Connected Gateways
      :align: center

#. Login with your user credentials

   .. figure:: ../../_static/android_gateway_login.png
      :scale: 20 %
      :alt: Setup App: Gateway login
      :align: center

#. Select the target Thing under the *Unregistered* tab

   .. figure:: ../../_static/android_things_unregistered.png
      :scale: 20 %
      :alt: Setup App: Unregistered Things
      :align: center

#. Wait for the OpenThread configurations to be transferred.

   .. figure:: ../../_static/android_ot_settings.png
      :scale: 20 %
      :alt: Setup App: OpenThread settings
      :align: center

#. Power off and on the KNoT Thing.

----------------------------------------------------------------

See connected Things
--------------------

If all the steps were followed correctly, it will be possible to see that the KNoT Thing is connected to the target Gateway.

To do so:

#. Access the gateway web page with `<http://knot.local>`_.

#. Login with your user credentials.

#. Look for your connected thing and see the value being updated.

.. figure:: ../../_static/webui_devices.png
   :scale: 100 %
   :alt: WebUI connected devices
   :align: center

----------------------------------------------------------------

Representing an Application on KNoT Cloud
-----------------------------------------

#. Log-in to KNoT Cloud.

    .. figure:: ../../_static/cloud_login.png
      :scale: 35 %
      :alt: KNoT Cloud UI login page
      :align: center

#. Go to Apps page and create an application.

    .. figure:: ../../_static/cloud_app_creation.png
      :scale: 25 %
      :alt: KNoT Cloud UI applications page
      :align: center

#. Set a name to your application.

    .. figure:: ../../_static/cloud_app_creation_modal.png
      :scale: 28 %
      :alt: KNoT Cloud UI applications modal
      :align: center

#. Download the application credentials.

    .. figure:: ../../_static/cloud_app_credentials.png
      :scale: 35 %
      :alt: KNoT Cloud UI download app credentials
      :align: center

#. The application credentials should look like:

    .. code-block:: json

      {
        "type": "knot:app",
        "metadata": {
          "name": "Hello Application"
        },
        "knot": {
          "id": "3c92790f-f265-46c9-bbf8-e440f0447587",
          "isThingManager": false
        },
        "token": "826faa7d545e39c8b2a198c74d0da54f95dfea55"
      }

----------------------------------------------------------------

Interacting with an Application through KNoT Cloud SDK
------------------------------------------------------

#. Download and install `NodeJS and NPM <https://nodejs.org/en/download/>`_.

#. Create a new directory and start a NodeJS application on it.

    .. code-block:: bash

      mkdir my_knot_app
      cd my_knot_app
      npm init -y

#. Install the KNoT Cloud SDK for JavaScript.

    .. code-block:: bash

      npm i -s @cesarbr/knot-cloud-sdk-js

#. Create an ``index.js`` file and import the ``knot-cloud-sdk-js`` library.

    .. code-block:: javascript

      const { Client } = require('@cesarbr/knot-cloud-sdk-js');

#. Create a client connection instance with the KNoT Cloud WebSocket server.

    .. code-block:: javascript

      const client = new Client({
        hostname: 'ws.knot.cloud',
        protocol: 'wss',
        port: 443,
        pathname: '/ws',
        id: '3c92790f-f265-46c9-bbf8-e440f0447587', // APP ID
        token: '826faa7d545e39c8b2a198c74d0da54f95dfea55', // APP TOKEN
      });

    .. warning:: Update the ``id`` and ``token`` fields with the application credentials that you have received.

#. Get the KNoT Thing's ID from the gateway interface.

    .. figure:: ../../_static/webui_devices_id.png
      :scale: 100 %
      :alt: KNoT Thing ID
      :align: center

#. Send ``setData`` command to turn off the KNoT Thing's LED when the connection is established.

    .. code-block:: javascript

      const data = [
        {
          sensorId: 0, // LED's sensorID
          value: false, // New LED's value
        },
      ];

      client.on('ready', () => {
        client.setData('2828b4c983f2d9d1', data); // Send setData command, passing to it the KNoT Thing's ID and the data.
      });

      client.on('sent', () => {
        client.close(); // close the connection after command is sent
      });

      client.on('error', (err) => {
        console.log(err);
        console.log('Connection refused');
      });

      client.connect();

    .. note:: Use the KNoT Thing's ID in lowercase like: ``2828b4c983f2d9d1``.

#. Listen to data events sent by the KNoT Thing. These events can be listened to by registering a handler with ``on('data')``.

    .. code-block:: javascript

      client.on('ready', () => {});

      client.on('data', (data) => {
        if (data.from === '2828b4c983f2d9d1') {
          console.log(JSON.stringify(data, null, 2));
        }
      })

      client.on('error', (err) => {
        console.log(err);
        console.log('Connection refused');
      });

      client.connect();

    .. note::
      This event listener will receive every data events sent by all things
      associated with your user. To filter them, you just need to compare the
      ``from`` field with the KNoT Thing ID you want to listen.

#. The expected incoming data should look like:

    .. code-block:: json

      {
        "from": "2828b4c983f2d9d1",
        "payload": {
          "sensorId": 0,
          "value": false,
        }
      }

#. Run the example.

    .. code-block:: bash

      NODE_TLS_REJECT_UNAUTHORIZED=0 node index.js

    .. note::
      The environment variable `NODE_TLS_REJECT_UNAUTHORIZED
      <https://nodejs.org/api/cli.html#cli_node_tls_reject_unauthorized_value>`_
      need to be set to '0' in order to disable the TLS certificate
      verification, since you are connecting to a WebSocket Secure server.
      It should be used only on development.
