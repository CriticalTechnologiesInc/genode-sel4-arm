This directory contains files/folders pertaining to the efforts
under the DARPA job using the seL4 micro-kernel, Genode and
TrustZone on ARM base systems, currently I.MX6 platforms.

More information on this project can be found here:
http://genodl4arm.critical.com

==================
DIRECTORY OVERVIEW
==================

genode-zips/
	Contains zips of Genode releases, both official and 
	those of self altered versions

sabre-lite/
	Files and instructions for SabreLite

sd-card/
	Files required for SD card creation for Wandboard Quad

wand-board/
	Files and instructions for Wandboard Quad

=============
PREREQUISITES
=============

Genode Setup
============
See "genode-setup.txt" for details.

Serial Setup
============
Any serial utility (such as Putty on Windows and Minicom on Linux)
is fine. Just set the 'Port' to a valid COM input and 'Hardware Flow Control' 
to Off/No/None.

SD Card Setup
=============
See "sd-card/sdcard-setup.txt" for details on how to setup the SD-cards
for use on Wandboard Quad.

==================
Board Instructions
==================

The following build documents will walk through how to prepare
Genode and seL4 to be cross compiled. It is recommended to work on
a standalone Linux system or inside a Virtual Machine (VM) as you
will be making major modifications to the Linux installation.

Wandboard Quad
==============
See "wand-board/wandquad-setup.txt" for details on how to setup Genode
for this platform.

SabreLite
=========
See "sabre-lite/sabrelite-setup.txt" for details on how to setup Genode
for this platform.
