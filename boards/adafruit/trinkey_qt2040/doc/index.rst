.. zephyr:board:: adafruit_trinkey_qt2040

Overview
********

The `Adafruit Trinkey QT2040`_ board is based on the RP2040
microcontroller from Raspberry Pi Ltd. The board has a Stemma QT connector
for easy sensor usage, and has a USB type A connector.
The board outline is similar to many Adafruit Stemma QT shields.

Hardware
********

- Microcontroller Raspberry Pi RP2040, with a max frequency of 133 MHz
- Dual ARM Cortex M0+ cores
- 264 kByte SRAM
- 8 Mbyte QSPI flash
- USB type A connector
- Reset and boot buttons
- RGB LED (Neopixel)
- Stemma QT I2C connector


Default Zephyr Peripheral Mapping
=================================

.. rst-class:: rst-columns

    - Boot/User button: GPIO12
    - RGB LED: GPIO27
    - I2C0_SDA : GPIO16
    - I2C0_SCL : GPIO17

Note that no serial port pins (RX or TX) are exposed. By default this board
uses USB for terminal output.

The Boot/User button will pull down the QSPI chip-select line (via a diode) for
entering the built-in USB bootloader at startup.
The devicetree file enables an in-chip pull-up resistor for the Boot/User button so
it can be used during runtime, for example via the :zephyr:code-sample:`input-dump` sample.
However the :zephyr:code-sample:`button` sample is somewhat unreliable, as there might be lots of
interrupts. This can be solved by using a stronger external pull-up via the TP4
test point on the back of the PCB.

See also `pinout`_ and `schematic`_.


Supported Features
==================

.. zephyr:board-supported-hw::


Programming and Debugging
*************************

.. zephyr:board-supported-runners::

The Adafruit Trinkey QT2040 board does not expose
the SWDIO and SWCLK pins, so programming must be done via the USB
port. Press and hold the BOOT button, and then press the RST button,
and the device will appear as a USB mass storage unit.
Building your application will result in a :file:`build/zephyr/zephyr.uf2` file.
Drag and drop the file to the USB mass storage unit, and the board
will be reprogrammed.

For more details on programming RP2040-based boards, see
:ref:`rpi_pico_programming_and_debugging`.


Flashing
========

To build and flash the :zephyr:code-sample:`led-strip` application,
which will blink the on-board RGB LED in different colors:

.. zephyr-app-commands::
   :zephyr-app: samples/drivers/led/led_strip
   :board: adafruit_trinkey_qt2040
   :goals: build flash

Try also the :zephyr:code-sample:`input-dump` and :zephyr:code-sample:`usb-cdc-acm-console` samples.
Note that the latter creates an additional USB serial port endpoint (for
example ``ttyACM1`` on Linux), so make sure to use the correct one when running the sample.


References
**********

.. target-notes::

.. _Adafruit Trinkey QT2040:
    https://learn.adafruit.com/adafruit-trinkey-qt2040

.. _pinout:
    https://learn.adafruit.com/adafruit-trinkey-qt2040/pinouts

.. _schematic:
    https://learn.adafruit.com/adafruit-trinkey-qt2040/downloads
