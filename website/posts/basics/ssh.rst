.. title: Using SSH for Remote Access
.. slug: using-ssh-for-remote-access
.. date: 2021-04-07 14:00
.. tags:
.. category: misc:basics
.. link:
.. description:
.. type: text
.. priority: 2

SSH (Secure Shell Protocol) gives remote access to remote computer. In its basic form it allows
the execution of command lines in a terminal, if the remote machine is running an SSH server.
It can also be used for remote graphical user interfaces.

-----

Connecting to an SSH Server
===========================

For connecting to a remote machine, it needs to run an SSH server.
On the client side, an SSH connection can be established
without additional installations from the terminal
on Linux and MAC machines and - since version 10 - from Windows.
SSH receives the following command, with the remote user's credentials (username and ip-address).
This user needs to be installed on the remote machine.
The remote SSH server will ask for the user's password, if no SSH key has been installed.


.. code-block:: console

  $ ssh username@address


-----

X11 Forwarding
==============

X11, or the X Window System is a  framework for a graphical user interface (GUI) environment, used on Unix systems.
With X11 Forwarding, SSH can also be used to run applications with a GUI, remotely.
When connecting to an SSH server from a Linux machine, simply add the ``-X`` argument to do so:

.. code-block:: console

  $ ssh -X username@address


-----


X11 On Mac
----------

On Mac you need to install `xqwartz <https://www.xquartz.org/>` to enable X11 Forwarding.
Afterwards, the ``-X`` argument will enable X11 Forwarding:

.. code-block:: console

  $ ssh -X username@address


-----

X11 on Windows
--------------

Although SSH will be possible from Windows' builtin Power Shell or Windows Terminal,
X11 Forwarding requires Putty and additional tools:


- install putty

- install vcxsrv

- enable X11 in Putty



-----

Remote Commands
===============

SSH can also be used to send single commands, without starting a remote session. This example launches the ``jack_simple_client``,
which plays a continuing sine tone on the remote machine.

.. code-block:: console

    $ ssh -t username@address 'jack_simple_server'

.. admonition:: Exercise

       Log into the server with SSH.
