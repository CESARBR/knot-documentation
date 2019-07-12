KNoT Gateway
============

Hardware Architecture
---------------------

To have several radio capabilities, the KNoT Gateway must be composed of hardware elements able to handle different
wireless protocol stacks as well as communication peripherals used for communicating with each radio interface. Moreover,
the gateway needs enough computing power to handle protocol stacks and run cloud services implementing message brokering,
data storage, and data processing capabilities.

The main component of the gateway is a board based on an ARM microprocessor, which is the ideal processor for running a
customized version of Embedded Linux. Such a board must be also able to deal with as many communication peripherals as
possible to manage data traffic from the different radios.

Most of the demand required by IoT nodes regards power consumption due to wireless interfaces.
To deal with such an issue, the hardware architecture was envisioned to provide support to networks such as Low-Rate
Personal Area Networks(LR-PANs), Local Area Networks (LANs), and Mesh Local Area Networks (Mesh-LANs), which are common
in the IoT and consumer electronics contexts.

Unlike IoT nodes, which alternate periods of active operation with periods in ultra low power modes, the gateway must be
active at most of its time. In this scenario, a battery-powered gateway would require a large power source or a constant
battery replacement. To avoid such costly drawbacks, the gateway is expected to be constantly plugged to the energy grid.

Software Architecture
---------------------

The KNoT Gateway makes use of Buildroot, an open-source project to cross-compile an embedded Linux system and build a
lightweight embedded Linux distribution. The KNoT Linux distribution was created by selecting some Linux services required
by the gateway to operate, such as networking management services, Web server, and NoSQL database. Besides the use of
existing software packages, it was necessary to develop new services to handle the IoT gateway operation. An important
feature is that all software developed and used by KNoT are open source projects.

This is the essential for the KNoT Gateway to have a good acceptance and adoption as a multi-radio gateway platform. The
KNoT Gateway also encompasses different manager daemons, each one responsible for managing different capabilities alongside
the gateway. Such daemons are described in the following.

   - **PAN Network Manager (nrfd).** The  PAN  Network  Manager is responsible for establishing a Personal Area Network (PAN) with devices using this type of protocol stack. In our reference implementation, the nRF24l01+ radio was used for the  PAN network. The  daemon nrfd has  the  NRF24L01+drivers, PHY, Link, and network layers of this stack.

   - **Mesh Network Manager (inetbrd+wpantund).** The Mesh Network Manager is responsible for creating a Mesh network for devices that use this type of communication. In our reference implementation, we forked the wpantund service from OpenThread, which allows the gateway to act as border router with an IEEE 802.15.4 stack. The inetbrd daemon creates an IP bridge for sending the traffic from local interfaces to the KNoT Device Manager (knotd).

   - **LAN Network Manager (bluetoothd).** The LAN Network Manager handles devices implementing LAN wireless protocol stacks, such as Bluetooth. This daemon is part of the KNoT Gateway architecture, but it is not currently available in our reference implementation.

   - **Other Radio Managers.** The KNoT Gateway architecture was designed with multiple wireless protocol stacks in mind. Therefore, a flexible architecture has been proposed to support other technologies in the future.

   - **KNoT Devices Manager (knotd).** The knotd is a daemon acting as proxy between the network managers and the KNoTFog, thus providing a central point for handling KNoT devices, protocol translation, and message forwarding capabilities.

   - **KNoT Gateway Web UI (knot-web).** The KNoT Gateway UI is a Web interface for managing KNoT devices coming from all networks and also for managing the gateway itself in terms of configuring IP, user credentials, etc.

   - **KNoT Fog.** The KNoT Fog is responsible for providing IoT cloud capabilities in the gateway, such as message brokering, data storage, and data processing, as well as for providing local access to devices when Internet connection is not available. Our reference implementation uses a fork of Meshblu message broker, which allows creating virtual devices, storing their data, and communicating over some transport layer protocols such as HTTP, WebSocket, MQTT, and COAP.

   - **Fog Connector.** The Fog Connector synchronizes device data between the KNoT Fog and other IoT cloud platforms,e.g. AWS IoT, FIWARE or Konker. To implement a fog connector, it is necessary to develop an API for the desired IoT cloud platform with operations for managing devices (add, update, delete), describe devices, send and receive device’s data and configuration. Information is shared among these elements using several communication protocols,such as D-Bus, Unix Socket, and WebSocket.

   - **NetSetup.** The NetSetup is a daemon to setup network interfaces (currently Openthread wpan0 interface) from DBus or Bluetooth interfaces.

   - **KNoT Control.** KNoT Control is a daemon to control the hardware status and configurations.

.. note:: This text is adapted from paper `A Multi-Radio Gateway Architecture and Implementation for Consumer Electronics <https://ieeexplore.ieee.org/abstract/document/8661957>`_
