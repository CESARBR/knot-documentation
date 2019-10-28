CLI
===

KNoT Cloud CLI makes it easy to manage things and operate on them.

------------------------------------------------------------------

Installation and usage
----------------------

Download
''''''''

The provided stacks and CLI contained in this repository aren't yet published
in any package manager, hence it is necessary that you clone the repository or
download the ``.zip`` containing all the files.

   .. code-block:: bash

        git clone https://github.com/CESARBR/knot-cloud.git

The following instructions always assume you are in the directory created
after cloning the repository. If you downloaded the ``.zip``, navigate to
the appropriate folder.

Build and install CLI tool
''''''''''''''''''''''''''

   .. code-block:: bash

        npm install
        npm run build
        npm link

Depending on npm configurations, it might be necessary to run ``npm link``
with superuser privileges.

   .. code-block:: bash

        sudo npm link

Help
''''

Executing ``knot-cloud`` without any arguments will output help with all available commands and general options:

   .. code-block:: text

        Commands:
        knot-cloud init [path]                    Initialize stack at [path]
        knot-cloud create-gateway <name>          Create a gateway
        <active>
        knot-cloud create-session-token <id>      Create session token to device <id>
        knot-cloud create-thing <id> <name>       Create a thing
        knot-cloud delete-device <id>             Delete device <id>
        knot-cloud get-data <thing-id>            Requests the current value of
        <sensor-id>                               <sensor-id> from <thing-id>
        knot-cloud list-devices                   List devices
        knot-cloud listen-data                    Listen to data events
        knot-cloud publish-data <sensor-id>       Publish <value> as a <sensor-id>
        <value>
        knot-cloud set-data <thing-id>            Set data to a thing
        <sensor-id> <value>
        knot-cloud login                          Sign-in as a user
        knot-cloud update-schema [sensor-id]      Update a thing schema
        [value-type] [unit] [type-id] [name]

        Options:
        --version           Show version number                              [boolean]
        --credentials-file  Path to JSON config file
        --schema-file       Path to JSON config file
        -h, --help          Show help                                        [boolean]

----------------------------------------------------------------


User
----

Login
'''''

You can use the user's e-mail and password to use the CLI in an easier way.  The credentials will be saved in the ``$HOME/.knot`` directory.

   .. code-block:: bash

      knot-cloud login

   .. code-block:: text

      Enter your e-mail: cli@knot.com
      Enter your password:
      You have been successfully logged in.
      Credentials saved in /Users/jneto/.knot/credentials.json

   .. note::
      You can use the option ``--credentials-file`` to specify the credentials of another device you want to operate as.

Devices
-------

Create Gateway
''''''''''''''
   .. code-block:: bash

      knot-cloud create-gateway <name> <active>


   .. code-block:: text

      knot-cloud create-gateway gw1 false
      {
         "type": "knot:gateway",
         "metadata": {
            "name": "gw1"
         },
         "knot": {
            "active": false,
            "id": "1cb0b19a-f7bd-4a61-9f8d-f944746c039d"
         },
         "token": "ec587af2b5dd8f53adc0ddfb81cbfb38f1016685"
      }

Create Thing
''''''''''''

   .. code-block:: bash

      knot-cloud create-thing <id> <name>


   .. code-block:: text

      knot-cloud create-thing f693054d669bf89c cli-thing

         {
            "type": "knot:thing",
            "metadata": {
               "name": "cli-thing"
            },
            "knot": {
               "gateways": [],
               "id": "f693054d669bf89c"
            },
            "token": "f2b374271be693a692261739437201be300bb7b4"
         }

Delete Device
'''''''''''''

   .. code-block:: bash

      knot-cloud delete-device <id>

   .. code-block:: text

      knot-cloud delete-device f693054d669bf89c

Create Session Token
''''''''''''''''''''

   .. code-block:: bash

      knot-cloud create-session-token <id>

   .. code-block:: text

      knot-cloud create-session-token f693054d669bf89c
      { token: 'f257798ac393d19b04dd29ac972b8417ade1f234' }

List Devices
''''''''''''

   .. code-block:: bash

      knot-cloud list-Devices

   .. code-block:: text

      knot-cloud list-Devices
      [
         {
            "type": "knot:thing",
            "metadata": {
               "name": "cli-thing"
            },
            "knot": {
               "gateways": [],
               "id": "f693054d669bf89c"
            }
         },
         {
            "type": "knot:gateway",
            "metadata": {
               "name": "gw1"
            },
            "knot": {
               "active": false,
               "id": "1cb0b19a-f7bd-4a61-9f8d-f944746c039d"
            }
         }
      ]

Update Schema
'''''''''''''

You need to use the thing's credentials to update its credentials. Moreover, the CLI will update the schema with a default one if you need
to update it quickly for testing purposes.

   .. code-block:: bash

      knot-cloud update-schema [sensor-id] [value-type] [unit] [type-id] [name] --credentials-file thing.json

   .. code-block:: bash

      knot-cloud update-schema 0 3 0 65521 Gw Thing

Set Data
''''''''

Send a command to update a thing's sensor value.

   .. code-block:: bash

      knot-cloud set-data <thing-id> <sensor-id> <value>

   .. code-block:: text

      knot-cloud set-data f693054d669bf89c 1 true

Get Data
''''''''

Send command to receive the last thing's sensor value.

   .. code-block:: bash

      knot-cloud get-data <thing-id> <sensor-id>

   .. code-block:: text

      knot-cloud get-data f693054d669bf89c 1

   .. note::
      In order to receive this data you can start another terminal session and run the command ``knot-cloud listen-data``, see `Listen Data`_.

Publish Data
''''''''''''

Publish data as a thing's sensor.

   .. code-block:: bash

      knot-cloud publish-data <sensor-id> <value> --credentials-file thing.json

   .. code-block:: text

      knot-cloud publish-data 1 false

Listen Data
'''''''''''

Receive data sent by the things.

   .. code-block:: bash

      knot-cloud listen-data

   .. code-block:: text

      {
         "from": "f693054d669bf89c",
         "payload": {
            "sensorId": 0,
            "value": true
         }
      }
      {
         "from": "f693054d669bf89c",
         "payload": {
            "sensorId": 0,
            "value": false
         }
      }