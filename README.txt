This directory contains files/folders pertaining to the efforts
under the DARPA job using the seL4 micro-kernel, Genode and
TrustZone on ARM base systems, currently I.MX6 platforms.

==================
DIRECTORY OVERVIEW
==================

deps/
	Contains various dependencies needed for the project

genode-zips/
	Contains zips of Genode releases, both official and 
	those of self altered versions

sd-card/
	Files required for SD card creation on SabreLite and
	Wand-Board Quad

==============
PRE-REQUISITES
==============

From apt-get (Ubuntu 18.04 LTS)
===============================
	sudo apt install git
	sudo apt install make
	sudo apt install python
	sudo apt install python-pip
	pip install future
	pip install tempita
	pip install ply
	sudo apt install expect
	sudo apt install tcl
	sudo apt install libxml2-utils
	sudo apt install u-boot-tools
	sudo apt install minicom

From deps/
==========
	cd /
	sudo tar Jxvf [path-to-dir]/deps/genode-toolchain-17.05-x86_64.tar.xz

	If you want to grab your own version of the toolchain:
		wget https://sourceforge.net/projects/genode/files/genode-toolchain/17.05/genode-toolchain-17.05-x86_64.tar.xz/download
		mv download genode-toolchain-17.05-x86_64.tar.xz

Minicom Setup
=============
	Set the port to /dev/ttyUSB0 and Hardware Flow Control
	to OFF.

=============
BUILD PROCESS
=============

SD Card Setup
=============
See "sd-card/README.txt" for details on how to setup the SD-cards
for use on Wandboard Quad.

Genode Setup/Overview
=====================
Preselected Genode versions used/tested are located in genode-zips/. 
To obtain your own Genode zip file head to:
https://sourceforge.net/projects/genode/files/genode/

After unzipping the selected Genode version to where you
like, move into its directory. <genode> will denote the location
that you have unzipped the folder.

If you want a fresh copy of Genode straight from source (non-zipped):
	git clone git://github.com/genodelabs/genode.git

There are a few commands that are helpful to us which we will
cover here:

./tool/ports/list
	This command will list all avalible ports that the current
	Genode version supports. 

./tool/ports/prepare_port [port-name]
	This command will setup Genode to support the given port 
	name. Port names come from the list command (above) and
	will NOT auto-complete in bash.

./tool/create_builddir [build-name]
	This command creates the build/<build-name> directory
	where we can create a version of Genode to run on the
	desired system.

Wandboard Quad
==============
See "wand-board/README.txt" for details on how to setup Genode
for this platform.

SabreLite
=========
See "sabre-lite/README.txt" for details on how to setup Genode
for this platform.
