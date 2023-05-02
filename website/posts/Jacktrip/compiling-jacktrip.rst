.. title: Compiling JackTrip
.. slug: compiling-jacktrip
.. date: 2021-04-07 14:00
.. tags:
.. category: _nsmi:jacktrip
.. link:
.. description:
.. type: text
.. priority: 3
.. author: NT

The SPRAWL System needs some additional features that are missing from the main
branch of Jacktrip. To build the correct JackTrip version, the Jacktrip git repository
must be cloned and checked out to the correct branch.

Therefor git must be installed. On MacOS git is often already installed.
Linux users should install git through their package manager.
Windows users download the installer from `git-scm <https://git-scm.com/>`_.

Getting the JackTrip Source Code
================================

Now the JackTrip source code can be downloaded from the official JackTrip
repository.

.. code-block:: console

  git clone https://github.com/jacktrip/jacktrip.git
  git checkout nils

Changes in the remote repository have to get pulled.

.. code-block:: console

  git pull

Afterwards you can follow the `official build instructions <https://jacktrip.github.io/jacktrip/Build/Linux/>`_.


