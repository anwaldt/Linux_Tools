.. title: The Meson build system
.. slug: meson
.. date: 2022-05-06 14:00
.. tags:
.. category: misc:meson-ninja
.. link:
.. description:
.. type: text
.. priority: 1
.. author: Nils Tonnätt

Meson is a modern and fast build system with a lot of features. You can
find its documentation at [mesonbuild.com](https://mesonbuild.com/).
Meson is written in Python. Meson has different backends (Ninja, VS*, Xcode, …).

---

Installing Meson and Ninja
--------------------------

The best maintained backend of Meson is Ninja. Installing both can be done with
your distribution's package manager, with PIP, Homebrew, etc. The version for
your user and your superuser has to be the same.

Fedora

.. code-block:: console

    sudo dnf install meson ninja-build

Debian/Ubuntu

.. code-block:: console

    sudo apt install meson

macOS:

.. code-block:: console

    sudo brew install meson

PIP:

.. code-block:: console

    sudo pip install meson ninja

---

Build
-----

Meson builds in a separate directory. It doesn't touch anything of your project.
This way you can have seperate debug and release build directories for example.

Prepare your build directory:
```bash
meson builddir                                  # defaults to debug build

## Additional build directories
meson --buildtype release build_release         # release build
meson --buildtype debugoptimized build_debug    # optimized debug build
```

Now build with Ninja:
```bash
cd builddir
ninja
```

Install with:
```bash
sudo ninja install
```

---

Configuration
-------------

If you are in a build directory, `meson configure` shows you all available options.

