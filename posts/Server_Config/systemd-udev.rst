.. title: Wait for (Audio) Hardware in systemd
.. slug: systemd-udev
.. date: 2022-01-30 22:00
.. tags:
.. category: _nsmi:server-config
.. link:
.. description:
.. type: text
.. priority: 5
.. author: HvC


Wait for (Audio) Hardware
-------------------------

In some cases it can be necessary to wait for a specific device, like a USB interface, before starting a service with systemd. This is the case for the JACK server in some setups.

With system.device
~~~~~~~~~~~~~~~~~~

 ''systemd.device'' makes it possible to let services depend on the state of specific hardware. The following instructions work only for a static hardware setup and can fail if the hardware configuration is changed.

First: Find if systemd has a unit configuration file for the device. The following code lists all devices:

.. code-block:: console

  $ systemctl --all --full -t device

This will be a lot of output. Narrow down the search by grepping for the ALSA name of the device - in this case 'Track':

.. code-block:: console

  $ systemctl --all --full -t device | grep Track

The output looks as follows in this case:

.. code-block:: console

  sys-devices-pci0000:00-0000:00:14.0-usb2-2\x2d2-2\x2d2:1.0-sound-card1.device                               loaded active plugged M-Audio Fast Track

The '.device' identifier can now be used in the UNIT description's parts *After* and *Requires*:

.. code-block:: console

    [Unit]
    Description=Jack audio server
    After=sound.target sys-devices-pci0000:00-0000:00:14.0-usb2-2\x2d2-2\x2d2:1.0-sound-card1.device
    Requires=sys-devices-pci0000:00-0000:00:14.0-usb2-2\x2d2-2\x2d2:1.0-sound-card1.device
