.. title: Moving Files with SCP
.. slug: moving-files-with-scp
.. date: 2021-04-07 14:00
.. tags:
.. category: misc:basics
.. link:
.. description:
.. type: text
.. priority: 3

SCP (Secure copy protocol) is an SSH-based tool for transferring files between machines in local and wide area networks.
It is a safe and quick way to exchange data.

----

Copying to a Remote Machine
---------------------------

The following command copies the file ``testfile.html`` from the local machine to the home directory of the user student on the
server with the address specified address ``11.22.33``. Instead of the home directory (``~/``), any other target can be specified:

.. code-block:: console

  $ scp testfile.html student@11.22.33:~/

|

Add the ``-r`` flag to copy a directory recursively:

.. code-block:: console

  $ scp -r /foo/bar student@11.22.33:~/


  .. admonition:: Exercise

    Select or create a short WAV file on your local machine and copy it to your personal directory on the server using SCP.

-----

Copying From a Remote Machine
-----------------------------

To copy a file from a remote server, the arguments' order needs to be swapped. The dot ``(.)`` copies the data to the recent directory. Any other path can be used as target.

.. code-block:: console

  $ scp student@85.214.78.6:~/WebAudioFreqGain.html .

.. admonition:: Exercise

   Create a text file in your personal directory on the server. Copy it to your local machine using the SCP command from your local machine.
