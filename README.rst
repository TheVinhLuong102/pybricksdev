Pybricks tools & interface library
-----------------------------------

This is a package with tools for Pybricks developers. For regular users we
recommend the `Pybricks Code`_ web IDE.

This package contains both command line tools and a library to call equivalent
operations from within a Python script.

Installation
-----------------

Requirements:

- pyenv: Used to locally install another version of Python without touching
  your system Python.
- poetry: Used to download and install all Python dependencies with the right
  versions.

Installation steps:

::

    git clone https://github.com/pybricks/pybricksdev.git
    cd pybricksdev
    pyenv install 3.8.2 # You can skip this if you already have Python >=3.8.2
    poetry install


Flashing Pybricks MicroPython firmware
---------------------------------------
::

    poetry run pybricksdev flash ../pybricks-micropython/bricks/cplushub/build/firmware.zip -d 15

Replace the example path with the path to the firmware archive. Decrease the
delay ``d`` between data packages for faster transfer. Increase the delay if it
fails.

Running Pybricks MicroPython programs
---------------------------------------

This compiles a MicroPython script and sends it to a hub with Pybricks firmware
over Bluetooth Low Energy. It will attempt to send the program to the first
device named ``Pybricks Hub`` that it finds.

::

    poetry run pybricksdev run --help

    # Run a oneliner on a Pybricks hub
    poetry run pybricksdev run 'Pybricks Hub' 'print("Hello!"); print("world!");'

    # Run script on the first device we find called Pybricks hub
    poetry run pybricksdev run 'Pybricks Hub' demo/shortdemo.py

    # Run script on 90:84:2B:4A:2B:75
    poetry run pybricksdev run 90:84:2B:4A:2B:75 demo/shortdemo.py

    # Run script on ev3dev at 192.168.0.102
    poetry run pybricksdev run 192.168.0.102 demo/shortdemo.py

Compiling Pybricks MicroPython programs without running
--------------------------------------------------------

This can be used to compile programs. Instead of also running them as above,
it just prints the output on the screen instead.

::

    poetry run pybricksdev compile demo/shortdemo.py

    poetry run pybricksdev compile 'print("Hello!"); print("world!");'


This is mainly intended for developers who want to quickly inspect the
contents of the ``.mpy`` file. To get the actual file, just use ``mpy-cross``
directly. We have used this tool in the past to test bare minimum MicroPython
ports that have neither a builtin compiler or any form of I/O yet. You can
paste the generated ``const uint8_t script[]`` directly ito your C code.


.. _Pybricks Code: https://www.code.pybricks.com/
