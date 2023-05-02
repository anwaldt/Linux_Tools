.. title: Managing Jack Connections
.. slug: managing-jack-connections
.. date: 2021-04-07 14:00
.. tags:
.. category: _nsmi:server-config
.. link:
.. description:
.. type: text
.. priority: 7
.. author: NT

When JackTrip clients connect corresponding jack clients are created on the
server side that may have a name defined by the connecting client.
In the SPRAWL system every client connects with a remote name that
starts with `AP_`  followed by the user's name.
Those jack clients must be connected to the right inputs and outputs of the sprawl
system.
There are several solution to do this automatically. With `aj-snapshot` you
can create a snapshot of all current jack connections and reconnect that state later.
You can even running aj-snapshot as a daemon to constantly watch that all connections
of a snapshot are set.

In the sprawl system we don't know the full name of connecting jacktrip clients.
With `jack-matchmaker` we are able to write pattern files that use regular
expressions to connect jack clients:

.. code-block:: console

	#
	# Direct Input

	/AP_.*_1:receive_1/
	   SPRAWL_Server:in_1
	/AP_.*_1:receive_2/
	   SPRAWL_Server:in_2
	/AP_.*_2:receive_1/
	   SPRAWL_Server:in_3
	/AP_.*_2:receive_2/
	   SPRAWL_Server:in_4

Those regexes in slashes are conforming `python's regex syntax <https://docs.python.org/3/library/re.html>'_.
Jack-Matchmaker can show you all current connections:

.. code-block:: console

	$ jack-matchmaker -c
	AP_Nils_1:receive_1
	    SPRAWL_Server:in_1

	SPRAWL_Server:out_1
	    AP_Nils_1:send_1

	SPRAWL_Server:out_2
	    AP_Nils_1:send_2

	SPRAWL_Server:out_33
	    AP_Nils_1:send_1

	SPRAWL_Server:out_34
	    AP_Nils_1:send_2

As you see I'm sending one audio channel to the server that connects to the first
input of the SPRAWL_Server SuperCollider application.
The next two connections are the direct outputs to my receiving channels.
The last two connections are the binaural rendered spatialised mix.

Jack-Matchmaker user service
----------------------------

Right now the jack-matchmaker user service loads the pattern file
located in `/home/student/SPRAWL/matchmaker/sprawl_server_stereo.pattern`.
This might be changed in the future with a template instantiated service.

