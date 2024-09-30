.. title: Host Discovery with Nmap
.. slug: nmap
.. date: 2024-09-10 14:00
.. tags:
.. category: misc:basics
.. link:
.. description:
.. type: text
.. priority: 6
.. author: Henrik von Coler

Host Discovery with Nmap
------------------------


Nmap can be used to find all active clients in a network. It can be used in many different ways - this set of arguments works best for a local area network with several PIs.


.. code-block:: console

    nmap -sP 10.10.10.1/24

For a network with several PIs connected, the output will look like this:

.. code-block:: console

    Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-09-10 10:24 EDT
    Nmap scan report for 10.10.10.1
    Host is up (0.11s latency).
    Nmap scan report for 10.10.10.83
    Host is up (0.00011s latency).
    Nmap scan report for 10.10.10.101
    Host is up (0.055s latency).
    Nmap scan report for 10.10.10.102
    Host is up (0.055s latency).
    Nmap scan report for 10.10.10.103
    Host is up (0.055s latency).
    Nmap scan report for 10.10.10.104
    Host is up (0.0033s latency).
    Nmap scan report for 10.10.10.105
    Host is up (0.0033s latency).
    Nmap scan report for 10.10.10.106
    Host is up (0.0032s latency).
    Nmap scan report for 10.10.10.107
    Host is up (0.0046s latency).
    Nmap scan report for 10.10.10.108
    Host is up (0.0046s latency).
    Nmap scan report for 10.10.10.109
    Host is up (0.0046s latency).
    Nmap scan report for 10.10.10.112
    Host is up (0.049s latency).
    Nmap done: 256 IP addresses (12 hosts up) scanned in 30.59 seconds
