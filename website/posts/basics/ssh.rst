.. title: Using SSH for Remote Access
.. slug: using-ssh-for-remote-access
.. date: 2021-04-07 14:00
.. tags:
.. category: linux:basic-tools
.. link:
.. description:
.. type: text
.. priority: 0

SSH (Secure Shell Protocol) is necessary when working with the server but can also be helpful for
configuring the Access Points. For remote machines - like the SPRAWL Server - SSH
can be used for command-line operations and command execution.


Connecting to an SSH Server
===========================

For connecting to a remote machine, it needs to run an SSH server.
On the client side, an SSH connection can be established
without additional installations from the terminal
on Linux and MAC machines and - since version 10 - from Windows.
For older Windows versions, users can use `Putty <https://www.putty.org/>`_.

.. code-block:: console

  $ ssh username@address


X11 Forwarding
==============

With X11 Forwarding, SSH can also be
used to run applications with a GUI, remotely.
Simply add the ``-X`` argument to do so:

.. code-block:: console

  $ ssh -X username@address



Remote Commands
===============

SSH can also be used to send single commands, without starting a remote session. This example launches the ``jack_simple_client``,
which plays a continuing sine tone on the remote machine.

.. code-block:: console

    $ ssh -t username@address 'jack_simple_server'

.. admonition:: Exercise

       Log into the server with SSH.
