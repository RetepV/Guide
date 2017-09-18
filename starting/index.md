MyStorm Setup
=============

| Alan Wood, Dan Gorringe


MyStorm BlackIce Board
----------------------

.. figure:: mystorm.jpg

Installation prerequisites for Linux
------------------------------------

You need to install the Yosys tool chain.  All software is free and
open source.

The following steps are for installing software on Ubuntu 16.04 or
later, and cover the building and installation of three tools, which
are required for programming the myStorm board.  You can use these
for a laptop running Linux, or to install the tools on a Raspberry
Pi. Users of other flavors of Linux wil(l need to modify these
instructions slightly for their systems.

Downloading and installing pre-requisites

These are needed for compiling and installing the icestorm,
Arachne-PNR and yosys tools later.

**For Debian-based distributions, use the following command:**

  ```sudo apt-get install build-essential clang bison flex libreadline-dev gawk tcl-dev libffi-dev git mercurial graphviz xdot pkg-config python
  python3 libftdi-dev vim htop screen iverilog```

**For Fedora-based distributions, use the following command:**

  ```nf install @development-tools clang bison flex readline-devel \
  gawk tcl-devel libffi-devel git mercurial graphviz python-xdot \
  pkgconfig python python3 libftdi-devel vim htop screen iverilog```

**Note** that the tools work fine on RaspberryPi.

Installation prerequisites for macOS
------------------------------------

You need to install the Yosys tool chain.  All software is free and
open source.

The following steps are for installing software on macOS
and cover the building and installation of three tools, which
are required for programming the myStorm board.

This guide assumes you have Homebrew (https://brew.sh/) installed.

Enabling xcode command line tools

  ```xcode-select --install```

**Downloading and installing pre-requisites**

These are needed for compiling and installing the icestorm,
Arachne-PNR and yosys tools later.


  ```brew install libftdi0 python3 gawk pkg-config libffi bison mercurial```

Instalation of IceStorm for linux and macOS
-------------------------------------------

**Downloading and installing IceStorm**

Starting in an empty directory:

  ```git clone https://github.com/cliffordwolf/icestorm.git icestorm
  cd icestorm
  make -j8
  sudo make install```

**Downloading and installing arachne-pnr**

Starting in the same directory:

  ```git clone https://github.com/cseed/arachne-pnr.git arachne-pnr
  cd arachne-pnr
  make -j8
  sudo make install```

**Downloading and installing Yosys**

Starting in the same directory:

  ```git clone https://github.com/cliffordwolf/yosys.git yosys
  cd yosys
  make -j8
  sudo make install```

Installation guide for Windows
------------------------------

The following steps are for installing software on windows 10
and cover the installation of APIO, required to compile programs for
the myStorm board.

**Downloading and installing Python**

From the official python website download and install **Python2.7** (https://www.python.org/downloads/release/python-2713)

Then add to your path. With the default install locations open a command
line and type:

  ```set PATH=%PATH%;C:\Python27;C:\Python27\Lib;C:\Python27\DLLs;C:\Python27\Scripts```

**Downloading and installing APIO**

In a command line:

  ```pip install apio```

Then to download all the apio packages:

 ```apio install -a```



Cloning the tutorial code from GitHub
-------------------------------------

You will want to access four repositories:

* The MyStorm tutorial

  ```git clone https://github.com/mystorm-org/Guide.git```

Your first design (Mac/Linux)
-----------------------------

Completed examples are in the ``tutorial`` directory. We'll build the very
simplest of these to drive the red LED on the board.  First change into the
directory with the completed examples::

  cd starting/tutorial/blink

Then ``make`` the Blink example::

  make

This will synthesize the code in ``blink/blink.v`` to a bitstream in
``chip.bin``.

Your first design (Windows)
---------------------------

From ``cheat_sheet``, change to the ``blink`` directory

  ```cd starting\tutorial\blink```

Then synthesize the Blink example with ``apio``::

  ```apio build --size 8k --type hx --pack tq144:4k```

This will synthesize the code in ``blink.v`` to a bitstream in
``hardware.bin``.

Uploading your design (Mac/Linux)
---------------------------------

For Linux:

  ```make SERIAL=/dev/ttyACM0 upload-linux```

For Mac:

  ```make SERIAL=/dev/cu.usbmodem1421 upload-linux```

**MacOS** - Beware that if you have an earlier version of the CH340 driver you may get a [kernel panic](https://tzapu.com/ch340-ch341-serial-adapters-macos-sierra/) restart try updating to a [newer](https://blog.sengotta.net/signed-mac-os-driver-for-winchiphead-ch340-serial-bridge/)

You may need to use a different value for ``SERIAL`` depending on your
machine.

Uploading your design (Windows) (1)
-----------------------------------

Make sure you know which COM port you device is connected to by checking under
```Ports (COM & LPT)``` in Device Manager. If in doubt unplug and plug in the
device to make sure.

Start up *teraterm*

Uploading your design (Windows) (2)
-----------------------------------

* Select the Serial option and the COM port of your device, then go to the
  ``Setup`` > ``Serial port...`` menu item
* Delete the Baud rate option
* Set data as 8 bit, no parity, 1 bit stop and no flow control.
* Ensure new lines are correctly set up by going to ``Setup`` >
  ``Terminal...`` menu item and set ``Receive`` to ``AUTO``
* Then select the ``File`` > ``Send file...`` menu item and navigate to
  directory containing ``hardware.bin``
* Tick the ``Binary`` option box and open

**Note.** If you experience very slow download rates, unplug the device from
your computer.  Then plug it in again and re-check all settings above.

Your first design
-----------------

.. figure:: mystorm-led.jpg
