.. title: The Manual Ring
.. slug: manual-ring
.. date: 2024-09-10 14:00
.. tags:
.. category: _nsmi:jacktrip
.. link:
.. description:
.. type: text
.. priority: 5
.. author: Henrik von Coler


**The Manual Ring** is a group exercise to create a ring topology for an audio network, using JackTrip:

.. figure:: /images/mis/ring_1.png
	:figwidth: 100%
	:width: 400px
	:align: center

	*Four Access Points in a unidirectional circle.*

In this configuration, audio signals are passed into one direction only, thus creating a closed loop. Each of the Access Points [1,2,3,4] will do additional processing before sending the signal to the next AP.


------


Step 1: Launch a Hub Server on each AP
======================================

The JackTrip connections for the ring are all based on the Hub-Mode - make sure to use capital Letter arguments to create Hub instances (**-S** and **-C**).
After starting a Jack server, we can launch a JackTrip Hub Server.
This process will keep running and will wait for clients to connect:


.. code-block:: console

    jacktrip -S


------

Step 2: Launch a Hub Client on each Node
========================================

Oce Hub Servers are running, Hub Clients can connect to individual servers.

- Find the IP address and hostname of your left neighbor and establish a connection.
- Use a single channel connection (-n 1).
- Use arguments **-J** and **-K** to set the Jack client names on your own, respectively the peers machine.

Assuming we are **student1** and the neighbor is **student2** with the IP address **10.10.10.102**, this is the command:


.. code-block:: console

    jacktrip -C 10.10.10.102 -n 1 -J student2 -K student1


*Using the additional arguments for the client names makes the Jack connection graph less cluttered with IP addresses.*



------


Step 2: Boot SuperCollider and Connect
======================================

Processing of the audio signals will happen in SuperCollider. Open the scide to boot the default server by evaluating:


.. code-block:: supercollider

    s.boot

In the default settings, Jack will automatically connect clients to the system's inputs and outputs. We need to remove all connections and set new ones.
The AP need no input from the system, since we will use SC to generate sound on the AP directly.
We want to pass the signal coming our of SuperCollider to our left neighbor - that is **student1** and our own loudspeaker.
**student3** sits right of **student1**. We want to take their signal and send it into SuperCollider for processing.

The complete Jack routing for this AP looks like this now:

.. figure:: /images/mis/jack_graph_1.png
	:figwidth: 100%
	:width: 400px
	:align: center

	*Jack graph with Hub Server, Hub Client and SC server.*





------


Step 3: Create a Processing Node on the SC Server
=================================================


After all APs have performed the previous steps we have a fully connected ring. However, signals will not be passed on, since nothing is happening on the SC server.
We will create a processing node that will delay and attenuate the signal on every Access Point. This turns our ring of APs into a feedback-delay network:


.. code-block:: supercollider

    {
    var input     = SoundIn.ar(0);
    var processed = DelayC.ar(input,2,0.5,0.95);
    Out.ar(0,processed);
    }.play


With this node we are delaying the incoming signal by 0.5 seconds and passing it to the next AP with a gain of 0.95.
We can activate a server meter to see incoming and outgoing signals:


.. code-block:: supercollider

    s.meter

------



Step 4: Send a Signal Into the Ring
===================================


With all APs connected and processing nodes in place, each AP can send a signal into the system.
The following node creates a noise burst and sends it to the next AP as well as the loudspeaker:


.. code-block:: supercollider

    {
    Out.ar(0,EnvGen.ar(Env([0,1,0],[0.1,0.1]),doneAction:Done.freeSelf)*WhiteNoise.ar());
    }.play

------

.. admonition:: Exercise

    Create a GUI to control the delay and gain of the processing node in SuperCollider. Use two sliders or one 2D slider.
    A button can be used to trigger the noise burst.

