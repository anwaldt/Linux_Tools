.. title: Working with Images
.. slug: working-with-images
.. date: 2021-04-07 14:00
.. tags:
.. category: misc:basics
.. link:
.. description:
.. type: text
.. priority: 5
.. author: Nils Tonnätt

Getting the sprawl access point image
=====================================

`Download <http://hvc.berlin/download/sprawl_pi_image_20200628_shrinked.img.xz>`_ the operating system image for the sprawl access points!
According to its postfix .xz the image is compressed with the XZ compression algorithm.
Before writing the image to the sd card it has to be decompressed.

On Ubuntu/Debian you can install xz-utils and use unxz:

.. code-block:: console

  $ sudo apt-get install xz-utils
  unxz sprawl_pi_image_20200628_shrinked.img.xz

On MacOS try the unarchiver.
On Windows try the usual way to decompress files or `download xz-utils <https://tukaani.org/xz/>`_.

Writing images on sd card
=========================

MacOS
-----

.. code-block:: console

	➜  ~ diskutil list
	/dev/disk0 (internal, physical):
	   #:                       TYPE NAME                    SIZE       IDENTIFIER
	   0:      GUID_partition_scheme                        *1.0 TB     disk0
	   1:                        EFI EFI                     209.7 MB   disk0s1
	   2:                 Apple_APFS Container disk1         1000.0 GB  disk0s2

	/dev/disk1 (synthesized):
	   #:                       TYPE NAME                    SIZE       IDENTIFIER
	   0:      APFS Container Scheme -                      +1000.0 GB  disk1
		                         Physical Store disk0s2
	   1:                APFS Volume OWC Aura Pro SSD - Data 520.8 GB   disk1s1
	   2:                APFS Volume Preboot                 82.6 MB    disk1s2
	   3:                APFS Volume Recovery                525.8 MB   disk1s3
	   4:                APFS Volume VM                      2.1 GB     disk1s4
	   5:                APFS Volume OWC Aura Pro SSD        11.2 GB    disk1s5

	/dev/disk2 (internal, physical):
	   #:                       TYPE NAME                    SIZE       IDENTIFIER
	   0:     FDisk_partition_scheme                        *63.9 GB    disk2
	   1:             Windows_FAT_32 boot                    268.4 MB   disk2s1
	   2:                      Linux                         63.6 GB    disk2s2


disk2 seems to be the sd card with 64 GB. To access the raw device /dev/rdisk2
is used. To write to this device you have to be root (administrator).
Unmount the device before using dd.

.. code-block:: console

  diskutil unmountDisk /dev/disk2
  sudo dd if=rpi.img of=/dev/rdisk2 bs=4M

Linux
-----

.. code-block:: console

	$ sudo dd if=rpi.img of=/dev/disk/by-id/
	ata-PLDS_DVD-RW_DS8A8SH_S45N7592Z1ZKBE0758TK
	ata-SAMSUNG_MZMPA016HMCD-000L1_S11BNEACC10413
	ata-SAMSUNG_MZMPA016HMCD-000L1_S11BNEACC10413-part1
	ata-SAMSUNG_MZMPA016HMCD-000L1_S11BNEACC10413-part2
	ata-SAMSUNG_MZMPA016HMCD-000L1_S11BNEACC10413-part3
	ata-SanDisk_SSD_PLUS_240GB_184302A00387
	ata-SanDisk_SSD_PLUS_240GB_184302A00387-part1
	ata-SanDisk_SSD_PLUS_240GB_184302A00387-part2
	ata-SanDisk_SSD_PLUS_240GB_184302A00387-part3
	ata-SanDisk_SSD_PLUS_240GB_184302A00387-part4
	ata-SanDisk_SSD_PLUS_240GB_184302A00387-part5
	mmc-SDC_0x000000e2
	mmc-SDC_0x000000e2-part1
	wwn-0x5001b448b9edd143
	wwn-0x5001b448b9edd143-part1
	wwn-0x5001b448b9edd143-part2
	wwn-0x5001b448b9edd143-part3
	wwn-0x5001b448b9edd143-part4
	wwn-0x5001b448b9edd143-part5
	$ sudo dd if=rpi.img of=/dev/disk/by-id/mmc-SDC_0x000000e2 bs=4M status=progress

Windows
-------

On Windows the easiest way to write an image to a sd card is to use
a dedicated application like `Balena Etcher <https://www.balena.io/etcher/>`_.
