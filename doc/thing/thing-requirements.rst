Requirements
============

Linux based OS
--------------

The actual version of KNoT Zephyr SDK is only available for Linux based systems.

For other systems, you may consider using the `KNoT Docker <thing-docker.html>`_ (recommended) or a Virtual Machine running a Linux distribution.

----------------------------------------------------------------

Zephyr
------

Set up a Zephyr development environment.

.. note:: This section is based on `Zephyr instructions <https://docs.zephyrproject.org/1.14.0/getting_started/installation_linux.html>`_ and considers a Linux version based on Debian as host.

Update Your Operating System
''''''''''''''''''''''''''''

- Ensure your host system is up to date.

   .. code-block:: bash

      sudo apt update
      sudo apt upgrade

Install Requirements and Dependencies
'''''''''''''''''''''''''''''''''''''

#. Install Zephyr's dependencies.

   .. code-block:: bash

      sudo apt install --no-install-recommends git ninja-build gperf \
           ccache dfu-util device-tree-compiler wget \
           python3-pip python3-setuptools python3-tk python3-wheel xz-utils file \
           make gcc gcc-multilib

#. Install OpenThread and KNoT Protocol dependencies. These are external packages used by Zephyr and KNoT SDK.

   .. code-block:: bash

      sudo apt install autoconf automake libtool

#. Install CMake v3.13.1.

   .. code-block:: bash

      mkdir -p $HOME/bin/cmake && cd $HOME/bin/cmake && \
           wget https://github.com/Kitware/CMake/releases/download/v3.13.1/cmake-3.13.1-Linux-x86_64.sh && \
           yes | sh cmake-3.13.1-Linux-x86_64.sh | cat && \
           echo "export PATH=$HOME/bin/cmake/cmake-3.13.1-Linux-x86_64/bin:\$PATH" >> $HOME/.zephyrrc

   .. note:: CMake version 3.13.1 or higher is required.

Install the Zephyr SDK
''''''''''''''''''''''

#. Download and run the Zephyr SDK setup file.

   .. code-block:: bash

      wget -O $HOME/Downloads/zephyr-sdk-0.10.0-setup.run https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.10.0/zephyr-sdk-0.10.0-setup.run && \
           chmod +x $HOME/Downloads/zephyr-sdk-0.10.0-setup.run  && \
           $HOME/Downloads/zephyr-sdk-0.10.0-setup.run -- -d ~/zephyr-sdk-0.10.0

#. Program the ``$HOME/.profile`` to always set **ZEPHYR_TOOLCHAIN_VARIANT** and **ZEPHYR_SDK_INSTALL_DIR**.

   .. code-block:: bash

      echo "export ZEPHYR_TOOLCHAIN_VARIANT=zephyr" >> $HOME/.profile
      echo "export ZEPHYR_SDK_INSTALL_DIR=$HOME/zephyr-sdk-0.10.0" >> $HOME/.profile

Set up the Zephyr Environment
'''''''''''''''''''''''''''''

#. If you do not have ``~/.local/bin`` on your PATH environment variable, add it.

   .. code-block:: bash

      echo PATH=\"$HOME/.local/bin:'$PATH'\" >> $HOME/.profile
      source $HOME/.profile

#. Install the west binary and bootstrapper.

   .. code-block:: bash

      pip3 install --user west

#. Clone KNoT Zephyr fork.

   .. code-block:: bash

      git clone -b zephyr-knot-v1.14.0 https://github.com/CESARBR/zephyr.git $HOME/zephyrproject/zephyr/

   .. note:: It will create a folder under $HOME directory and clone zephyr inside it. Make sure to update the path on the following steps if you clone it under another folder.

#. Initialize west.

   .. code-block:: bash

      cd $HOME/zephyrproject/
      west init -l zephyr/
      west update

   .. note:: If the system can't find west, try logging out and in again.

#. Program the ``$HOME/.profile`` to always source zephyr-env.sh when you log in.

   .. code-block:: bash

      echo "source $HOME/zephyrproject/zephyr/zephyr-env.sh" >> $HOME/.profile

   .. note:: If you skip this step, it will be necessary to manually source zephyr-env.sh every time a new terminal is opened.

----------------------------------------------------------------

nRF5x Command Line Tools and Segger JLink
-----------------------------------------

Download and extract cli applications from `nRF5 Command Line Tools <https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF-Command-Line-Tools>`_ or following the step bellow.

#. Download nRF5 Command Line Tools.

   .. code-block:: bash

      wget -O $HOME/Downloads/nRFCommandLineTools1021tar.gz https://www.nordicsemi.com/-/media/Software-and-other-downloads/Desktop-software/nRF-command-line-tools/sw/Versions-10-x-x/nRFCommandLineTools1021Linuxamd64tar.gz

#. Extract nRF5 Command Line Tools.

   .. code-block:: bash

      tar -xvzf $HOME/Downloads/nRFCommandLineTools1021tar.gz -C $HOME/Downloads --one-top-level

#. Install nRF5x Command Line and Segger JLink deb packages.

   .. code-block:: bash

      sudo dpkg -i $HOME/Downloads/nRFCommandLineTools1021tar/nRF-Command-Line-Tools_10_2_1_Linux-amd64.deb
      sudo dpkg -i $HOME/Downloads/nRFCommandLineTools1021tar/JLink_Linux_V644e_x86_64.deb

----------------------------------------------------------------

Set up the KNoT SKD Environment
-------------------------------

#. Download the zephyr-knot-sdk repository.

   .. code-block:: bash

      git clone https://github.com/cesarbr/zephyr-knot-sdk/ $HOME/zephyr-knot-sdk/

   .. note:: The default clone path is the $HOME directory. Make sure to update the path on the following steps if you create it under another folder.

#. Program the ``$HOME/.profile`` to always source knot-env.sh when you log in. The environment configuration file is used to set up **$KNOT_BASE** path.

   .. code-block:: bash

      echo "source $HOME/zephyr-knot-sdk/knot-env.sh" >> $HOME/.profile

   .. note:: If you skip this step, it will be necessary to manually source knot-env.sh every time a new terminal is opened.

----------------------------------------------------------------

Add support to the KNoT command line interface
----------------------------------------------

#. Add cli.py to the path files.

   .. code-block:: bash

      ln -s $HOME/zephyr-knot-sdk/scripts/cli.py $HOME/.local/bin/knot

   .. note:: This will allow you to call the ``knot`` command line interface from any folder.

#. Use pip to install cli requirements.

   .. code-block:: bash

      pip3 install --user -r $HOME/zephyr-knot-sdk/scripts/requirements.txt

----------------------------------------------------------------

Add USB access to your user
---------------------------

- Add your user to the dialout group.

   .. code-block:: bash

      sudo usermod -a -G dialout `whoami`

----------------------------------------------------------------

Apply changes to profile
------------------------

- In order to apply the changes to your user, you must log out and log in again or reboot you system.

   .. code-block:: bash

      reboot
