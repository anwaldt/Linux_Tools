.. title: Using Shell Scripts
.. slug: Using Shell Scripts
.. date: 2021-04-07 14:00
.. tags:
.. category: misc:basics
.. link:
.. description:
.. type: text
.. priority: 2

Shell scripts can be helpful for organizing sequences
of terminal commands to execute them in a specific order
with a single call.
Shell scripts usually have the extension ``.sh``
and should start with a so called shebang (``#!...``), telling the
interpreter what binary to use.
After that, single commands can be
added as separate lines, just as using them in the terminal.
The following script ``test.sh`` starts the JACK server in the background,
waits for 3 seconds and afterwards launches the simple client, playing
a sine tone.


.. code-block:: console

  #! /bin/bash

  jackd &
  sleep 3
  jack_simple_client

|

The script can be executed from its source location as follows:

.. code-block:: console

  $ bash test.sh


-----

Shell scripts can be made executable with the following command:

.. code-block:: console

  $ chmod +x test.sh

Afterwards, they can be started like binaries,
when including the correct shebang:

.. code-block:: console

    $ ./test.sh


.. admonition:: Exercise

    Create an executable shell script in your personal directory on the server.
    Use the ``echo`` command in that script to print a simple message and run the
    file via SSH.
