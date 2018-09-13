This directory contains the necessary information to build
Genode on the SabreLite board along with seL4.

The SabreLite board used for testing can be found here:
https://www.mouser.com/new/Boundary-Devices/boundarydevices-SABRELite/

================
GENERAL OVERVIEW
================

base/
	Contains files from "<genode>/base". Mainly it is 
	the '.mk' from "base/mk/spec" and a '.h' file from
	"base/include/drivers/defs".
	
base-hw/
	Contains file from "<genode>/base-hw" and its
	various sub-directories.

base-sel4/
	Contains file from "<genode>/base-sel4" and its
	various sub-directories.

contrib/
	Contains a single file pulled from 
	"<genode>/contrib/sel4-<SHA>/src/kernel/sel4/configs/imx6"

tool/
	Files changed from "<genode>/tool" and one other sub-
	directory.

image.elf
	Image file for SabreLite using the seL4 kernel and the log
	module.

good-boot.txt
	Valid output using the 'image.elf' file on SabreLite board.

=============
BUILD PROCESS
=============

The first thing that must be done is to enable the use of
SabreLite for Genode. This requires us to change some of
the defaults around, and add things. This varies based
on our desired kernel. Global changes are located here.

NOTE: Copies of all files changed in this process can be found
in this directory. See "orig-dirs.txt" for details of each
files original location in Genode file structure.

Update Build Script
===================
We must update the build script to include SabreLite for Genode build
process. We will add the board to the list of platforms, and define
configuration and specification variables.

cd <genode>/tool/
vim create_builddir
	+13 sabre_lite
	+152 BUILD_CONF(sabre_lite) := run_kernel_hw run_boot_dir repos
	+236 SPECS(sabre_lite) := sabre_lite

Create Spec Files
=================
We now have to create the necessary files for Genode to build the
directories. The SabreLite board is very similar to the WandBoard
so we will take some liberties and copy and change files as needed.

cd <genode>/repos/base/mk/spec
cp wand_quad.mk sabre_lite.mk
vim sabre_lite.mk
	:%s/wand_quad/sabre_lite/g

cd <genode>/repos/base/include/drivers/defs
cp wand_quad.h sabre_lite.h
vim sabre_lite.h
	:%s/WAND_QUAD/SABRE_LITE/g
	:%s/Wand_quad/Sabre_lite/g
	~30 RAM0_SIZE = 0x40000000
	~36 UART1_1_IRQ = 59
	~37 UART1_MMIO_BASE = 0x021e8000

HW Kernel
=========
See "hw-build.txt" for details.

seL4 Kernel
===========
See "sel4-build.txt" for details.

Loading Image onto SD Card
==========================
An image will be produced for either of the Kernels above.

Simply copy the 'image.elf' file from
<genode>/build/sabre_lite/var/run/<module_name>/boot/
to the SD Card you wish to use.

NOTE: The 'image.elf' file is the combination of the other 
two files in the directory (them being 'genode.elf' and 'sel4').
This is ONLY the case when the kernel selected is seL4.

NOTE: The I.MX6 Sabre Lite has been configured to load the first 
stage boot loader (U-Boot) from SPI flash memory which is located 
on the board itself, which means that there’s no need for the a
card to have U-Boot on it to load the board.

NOTE: The 'image.elf' file found in this directory is one built
for seL4 kernel with the log module using the command:
make run/log KERNEL=sel4

Running SabreLite
=================
Connect SabreLite to your local machine using a Serial-to-USB cable 
and a null modem adapter. To boot up the SabreLite with the image 
apply power and enter the u-boot prompt by distrupting the boot process.

The following commands will boot Genode:
	mmc dev 0
        fatload mmc 0 0x30000000 image.elf
	bootelf 0x30000000

NOTE: 'mmc 0' is the SD Card slot, 'mmc 1' is the microSD Card slot.

NOTE: The file 'good-boot.txt' is a valid output of running Genode on
the SabreLite board with seL4 kernel and log module. The ELF file used
is also included in this directory.

