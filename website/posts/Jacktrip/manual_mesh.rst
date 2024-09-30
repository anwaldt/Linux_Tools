.. title: The Manual Mesh
.. slug: manual-mesh
.. date: 2024-09-28 14:00
.. tags:
.. category: _nsmi:jacktrip
.. link:
.. description:
.. type: text
.. priority: 6
.. author: Henrik von Coler


**The Mesh Ring** is a group exercise to create a fully connected mesh audio network, using JackTrip:

.. figure:: /images/mis/mesh_1.png
	:figwidth: 100%
	:width: 400px
	:align: center

	*Four Access Points in a fully connected mesh.*


In this configuration, audio signals can be sent to every node. Each of the Access Points [1,2,3,4]  can manage where to send signals and which signals to receive, including additional processing.


------


Step 1: Launch a Hub Server on each AP
======================================

The JackTrip connections for the ring are all based on the Hub-Mode - make sure to use capital Letter arguments to create Hub instances (**-S** and **-C**).
After starting a Jack server, we can launch a JackTrip Hub Server.
This process will keep running and will wait for clients to connect:


.. code-block:: console

    jacktrip -S



------


Step 2: Launch Hub Clients on each AP
=====================================


If **N** is the total number of Access Points in the system,each PI needs a connection to **N-1** peers. We do that by lauchching an individual number of JackTrip clients on each PI - this avoids duplicate connections. First steps:

- Find the IP addresses and hostnames of all peers.
- Use a single channel connection (-n 1).
- Use arguments **-J** and **-K** to set the Jack client names on your own, respectively the peers machine.


If we start connecting the PIs starting with the first one in the list (e.g. **student1, student2, student3, ...**), each PI needs to establish one connection less than the previous one:
**student1** needs to start JackTrip clients other PIs, resulting in N-1 clients. **student2** does not need to connect to **student1** actively and has to launch **N-2** clients.
The last PI in the list does not need to launch any JackTrip connection.


Port Offset
-----------

Each JackTrip client we start needs an individual UDP port number (servers do not have this issue). The Bind Port Number (the one used on the local machine) can be set with the **-B** flag.
The default port is 4464. It can be chosen "randomly" or incremented by one for each new JackTrip client we launch.



Connection Example
------------------

Assuming we have 12 PIs (stutent1 ... student12), this would be the list of commands to launch all JackTrip clients from **student8**. It is a total of four clients - students 1-7 have already connected to this one one themselves:


.. code-block:: console

    jacktrip -C 10.10.10.101 -n 1 -B 4465 -J student9  -K student8 &
    jacktrip -C 10.10.10.103 -n 1 -B 4466 -J student10 -K student8 &
    jacktrip -C 10.10.10.104 -n 1 -B 4467 -J student11 -K student8 &
    jacktrip -C 10.10.10.105 -n 1 -B 4468 -J student12 -K student8 &
    ...


This first version will make direct connections between hardware inputs/outputs and JackTrip clients. A signal from a single PI is automatically sent to all other Access Points.



.. ------
..
..
.. Step 2: SuperCollider for Routing
.. =================================
..
..
..
.. .. admonition:: Exercise
..
..     Create a SuperCollider script that has connections to all JackTrip clients and is able to set gains to all nodes and apply processing.
..
