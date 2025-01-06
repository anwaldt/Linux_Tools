.. title: SuperCollider for the Remote Server
.. slug: superCollider-for-the-remote-server
.. date: 2021-04-07 14:00
.. tags:
.. category: _nsmi:server-config
.. link:
.. description:
.. type: text
.. priority: 2
.. author: NT


SuperCollider is per default built with Qt and X for  GUI elements and the ScIde. This can be a problem when running it
on a remote server without a persistent SSH connection and starting it as a system service. However, for service reasons a version with full GUI support is a useful tool. One solution is to compile and install both versions and make them selectable via symbolic links:


1. **build and standard-install a full version of SuperCollider**
2. **build a headless version of SuperCollider (without system install)**
3. replace the following binaries in `/usr/bin` with symbolic links to the headless version
    - ``scsynth``
    - ``sclang``
    - ``supernova``
4. **create scripts for changing the symlink targets**

This allows you to redirect the symlinks to the GUI version for development and testing whereas they point to the headless version otherwise.

-----

Compiling a Headless SC
-----------------------

The SC Linux build instructions are very detailed: https://github.com/supercollider/supercollider/blob/develop/README_LINUX.md
Compiling it without all graphical components is straightforward. Simply add the flags ``NO_X11=ON`` and ``-DSC_QT=OFF`` for building a headless version of SuperCollider.
