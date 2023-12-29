.. title: Using JackTrip in the HUB Mode
.. slug: jacktrip-in-hub-mode
.. date: 2021-04-07 14:00
.. tags:
.. category: _nsmi:jacktrip
.. link:
.. description:
.. type: text
.. priority: 2
.. author: Nils Tonnaett

About JackTrip
--------------

In this class we will use JackTrip for audio over network connections but there
were some successful tests with the `Zita-njbridge <http://kokkinizita.linuxaudio.org/linuxaudio/index.html>`_.
JackTrip can be used for peer-to-peer connections and for server-client setups.
For the latter, JackTrip was extended with the so called *HUB Mode* for the `SPRAWL System </projects/sprawl_system/>`_ and the EOC in 2019-20.

---

Basics
======

For connecting to a server or hosting your own instance, the machine needs to
be connected to a router directly via Ethernet. WiFi will not result in
a robust connection and leads to significant dropouts.
JackTrip needs the following ports for communication. If a machine is behind
a firewall, these need to be added as an exception:


.. list-table:: JackTrip Ports
   :widths: 5 5 15
   :header-rows: 1
   :align: center

   * - Port
     - Protocol
     - Purpose

   * - 4464
     - TCP/UDP
     - audio packages

   * - 61002-62000
     - UDP
     - establish connection (server only)



----

The Nils Branch
===============

Due to the increasing interest, caused by the pandemic, and the endless list
of feature requests, the Jacktrip project has been growing rapidly in since early 2020
and the `repository <https://github.com/jacktrip/jacktrip>`_ has many branches.
In this class we are using the ``nils`` branch, which implements some unique features we need for the
flexible routing system. Please check the instructions for compiling and installing a specific branch: `Compiling JackTrip </Jacktrip/compiling-jacktrip/>`_

----

Starting JackTrip
-----------------

JACK Parameters
===============


Before starting JackTrip on the server or the clients, a JACK server needs to be booted on the system.
Read the chapter `Using JACK Audio </Linux/using-jack-audio/>`_ from the `Computer Music Basics </teaching/computer-music-basics/>`_ class for getting started with JACK. A purely remote server,
as used in this class, does not have or need an audio interface and can thus be booted with the dummy client:

.. code:: console

    $ jackd -d dummy [additional parameters]


To this point, the version of JackTrip used with the SPRAWL system requires all participants
to run their JACK server at the same sample rate and buffer size.
Recent changes to JackTrip ``dev`` branch allow the mixing of different buffer sizes
but have not been tested with this setup.
The overall system's buffer size is defined by the weakest link, respectively the
client with the worst connection.
Although tests between two sites have shown to work with down to $16$ samples,
a buffer size of $128$ or $256$ samples usually works for a group.
Experience has shown that about a tenth of all participants has an insufficient
internet connection for participating without significant dropouts.

----

JackTrip Parameters
===================

As with most command line programs, JackTrip gives you a list of all available
parameters with the help flag: ``$ jacktrip -h``
A single instance is launched on the SPRAWL Server with the following
arguments:

.. code:: console

  $ jacktrip -S -p 5 -D --udprt

|

The following arguments are needed for starting a JackTrip client instance
and connecting to the SPRAWL server (the server.address can be found in the private data area):

.. code:: console

  $ jacktrip -C server.address -n 2 -K AP_
