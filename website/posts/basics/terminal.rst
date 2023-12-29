.. title: Working with the Terminal
.. slug: working_with_the_terminal
.. date: 2021-04-07 14:00
.. tags:
.. category: misc:basics
.. link:
.. description:
.. type: text
.. priority: 0

People developing on MAC or Linux systems are used to doing things from the terminal or console.
Especially when working on remote servers - but also for embedded
devices for audio processing - the terminal is the standard tool.

-----

Directories
-----------

You can maneuver through the system's directories using
the ``cd`` command. Changing to an absolute path ``/foo/bar``
can be done like this:

.. code-block:: console

  $ cd /foo/bar

|

New directories are created with the ``mkdir`` command.
For creating a new directory ``mydir`` in your recent location,
type:

.. code-block:: console

    $ mkdir mydir

|

The content of the recent directory can be listed with the ``ls``
command. The following arguments improve the results:

.. code-block:: console

  $ ls -lah

  drwxrwxr-x  2 username group 4,0K Mar 25 12:25 .
  drwxrwxr-x 16 username group 4,0K Mar 25 12:25 ..
  -rwxrwxr-x  1 username group 9,1M Feb  3 17:47 jacktrip
  -rwxrwxr-x  1 username group 334K Feb  3 17:47 sprawl-compositor


.. admonition:: Exercise

    Create a directory with your name in the student user home directory ``/home/student/students/YOURNAME``.


-----

Create and Edit Files
---------------------

A file can be created by touching it:

.. code-block:: console

  $ touch filename

|

The default editor on most systems is ``nano``. It is a minimal terminal based tool and does not
require X forwarding. To edit an existing file or create a new file, type:

.. code-block:: console

  $ nano filename

|

**Terminal Only**

Inside nano, you have a lot of defined keystrokes for editing, file handling
and other tasks. See the nano cheat sheet for a full list: https://www.nano-editor.org/dist/latest/cheatsheet.html


.. admonition:: Exercise

  Create a text file in your personal directory and fill it with some text.

|

**GUI Based**

When working with X forwarding, simple text editors with GUI features can be used.
On the SPRAWL server, this includes ``mouspad`` or the minimal Python IDE ``idle``.


----

Starting Applications
---------------------

System wide binaries must be located in a directory that is listed in $PATH (see the final section on this page for details).
They can be started by simply typing the name:

.. code-block:: console

  $ foo

|

A local binary named `foo` can be started with the following command:

.. code-block:: console

  $ ./foo

-----

You can terminate your command with an ampersand  (`&`)
to run a process in the background. You can continue to work
in the terminal, afterwards:

.. code-block:: console

  $ ./foo &
  [1] 5459

If you start a command this way, it gives you an id of the background process
in brackets and the actual process ID (PID).

You can get the process back into foreground with the fg command followed by
the background process id:

.. code-block:: console

  $ fg 1

----

Check for Running Applications
------------------------------

At some point, users may want to know whether a process is running
or which processes have been started.
The command ``top`` lets you monitor the system processes with additional
information on CPU and memory usage, updated with a fixed interval:

.. code-block:: console

  $ top

----

``htop`` is  a slightly polished  version, using colored results:

.. code-block:: console

  $ htop

----

You can get a list of all running processes, including auxiliary
ones, by typing:

.. code-block:: console

  $ ps aux


----

Usually, these are way to many results.
If you want to check whether an instance of a specific
program is running, you can use ``grep`` after the ``ps aux``
to filter the results:

.. code-block:: console

  $ ps aux | grep foo



----

Shell Variables
---------------

Sometimes it is convenient to store information in variables for later use.
Some common variables that are used in Unix like operating systems like Linux,
BSD or MacOS are for example PATH and DISPLAY.

Shell variables are usually uppercase. To get the content of a variable it is
prefixed by a dollar sign. The command `echo` is used to print the content:

.. code-block:: console

  $ echo $PATH
  /home/username/.local/bin:/home/username/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin
  $ echo $DISPLAY
  :0

Defining a variable is done with an equal sign. It happens quite often that the
program that should use the variable, opens another environment. To access the variable
in that sub-environment, it has to be exported before:

.. code-block:: console

  $ NAME=username
  $ echo $NAME
  username
  $ bash
  $ echo $NAME

  $ exit
  exit
  $ export NAME
  $ bash
  $ echo $NAME
  username
