.. title: Network Audio
.. slug: network-audio
.. date: 2021-04-07 14:00
.. tags:
.. category: _nsmi:jacktrip
.. link:
.. description:
.. type: text
.. priority: 0



OSI Model
---------

The OSI Model groups different services, functions and applications of
telecommunication systems into seven hierarchically arranged layers:

.. list-table:: OSI Model
   :widths: 5 15 25
   :header-rows: 1
   :align: center

   * - Layer
     - Name
     - Description

   * - 7
     - Application Layer
     - End user layer, HCI layer
   * - 6
     - Presentation Layer
     - data conversion, syntax
   * - 5
     - Session Layer
     - connection management, sockets
   * - 4
     - Transport Layer
     - end-to-end connections (TCP, UDP)
   * - 3
     - Network Layer
     - packet routing
   * - 2
     - Data Link Layer
     - data formats (bits to frames, MAC addresses)
   * - 1
     - Physical layer
     - bit stream transmission over medium/hardware (Ethernet, WiFi, ...)

|

Network based audio systems can be based on
different layers. This affects their capabilities and application areas.
A comprehensive list can be found here: `comparison on Wikipedia <https://en.wikipedia.org/wiki/Comparison_of_audio_network_protocols>`_

-----

Layer 1 Solutions
=================

Layer 1 solutions only rely on the hardware used in telecommunication systems and use
their own routing mechanisms. As a consequence, they usually need specific routers and
are often  used for direct peer-to-peer connections. The most widespread solution is
the open *AES50* format, which is found in devices by Behringer and Midas.


Layer 2 Solutions
=================

Layer 2 solutions use the standard Ethernet protocol for transmitting data.
Standard routers and hardware can thus be used for routing. Among the well
known formats are *AVB* and *AES51*, as well as several proprietary solutions.


Layer 3 Solutions
=================

Layer 3 solutions feature an IP header in their packages.
Example solutions are *DANTE*, *AES67*, *RAVENNA* and *AVB*.


Layer 4 Solutions
=================

Some solutions are based on Layer 4 protocols like *TCP* or *UDP* [#]_.
Since *UDP* is faster due to the missing handshake and error-correction.
Although this makes it prone to package loss, it is the preferred method
for achieving acceptable latency at the cost of dropouts, depending on the
quality of the connection.

Examples for Layer 4 solutions can be found in the free and open software
community, including *NetJack2* [#]_, *Zita-njbridge* [#]_ and *JackTrip*.

----

.. [#] This needs more references, since it is not unambiguous on which layer they are working.
.. [#] https://github.com/jackaudio/jackaudio.github.com/wiki/WalkThrough_User_NetJack2
.. [#] http://kokkinizita.linuxaudio.org/linuxaudio/index.html
