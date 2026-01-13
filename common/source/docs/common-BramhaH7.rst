.. _common-BrahmaH7:

==========
BRAHMA H7
==========


.. image:: ../../../images/BRAHMA-H7-PIN-Layout.png       
    :target: ../_images/BRAHMA-H7-PIN-Layout.png                


The BRAHMA H7 is a flight controller designed and manufactured by `Darkmatter <https://thedarkmatter.in/>`_ in India.It is a high‑performance STM32H7‑based flight controller.


Where to Buy
============

- Contact `Darkmatter <https://thedarkmatter.in/>`__ directly for purchase information.

Specifications
==============

-  **Processor**
    - STM32H743VIT6 ARM Cortex‑M7
    - 480 MHz clock speed
    - External 8 MHz crystal
    - 2 MB Flash
    - 1 MB RAM
    - Bootloader reserved flash region

-  **Sensors**
    - Dual Invensense ICM42688 IMUs (SPI)
    - Infineon DPS310 barometer (I2C)
    - External compass supported via I2C


-  **Power**
    - 3–6S LiPo input
    - Dual battery voltage & current sensing
    - 5 V rail: up to 3 A total
    - 9 V rail: up to 3 A (switchable)
    - 2x 4.5 V pads for GPS/COMPASS + RX
    - 3.3 V rail up to 1 A


-  **Interfaces**
    - USB Type‑C (DFU + MAVLink + CAN)
    - MicroSD card (Blackbox logging)
    - 13 PWM outputs (10 motors, 2 servos, 1 LED)
    - 7 UARTs + USB
    - CAN bus
    - 2× I2C
    - SPI Out with breakouts
    - Analog RSSI and airspeed inputs
    - Digital VTX plug‑and‑play port
    - Dual 4in1 ESC plug and play
   
-  **Mechanical**
    - Size: 37 mm × 35.5 mm × 8 mm
    - Mounting: 30.5 mm × 30.5 mm (4 mm holes)
    - Weight: ~9 g


Pinout
======


Refer to the BRAHMA H7 datasheet for the complete pinout, connector layout, and pad labeling.


UART Mapping
============

The UARTs are marked Rn and Tn in the pinouts. The Rn pin is the receive pin for UARTn and Tn is the transmit pin.

| Port | UART    | Default Use   | TX DMA | RX DMA |
|------|---------|---------------|--------|--------|
| 0    | USB     | Console/MAVLink | ✘      | ✘      |
| 1    | UART7   | Telemetry1    | ✔      | ✔      |
| 2    | USART1 | Telemetry2    | ✔      | ✔      |
| 3    | USART2 | GPS1          | ✔      | ✔      |
| 4    | USART3 | GPS2          | ✔      | ✔      |
| 5    | UART8  | User / VTX    | ✔      | ✔      |
| 6    | UART4  | User / Companion | ✔   | ✔      |
| 7    | USART6 | RC Input      | ✘      | ✘      |

UART7 supports hardware flow control (CTS/RTS).

RC Input
========

Primary RC input is provided on **USART6 (SERIAL7)**. This port supports SBUS, CRSF, ELRS, iBUS, FPort, and other ArduPilot‑supported serial RC protocols.

For Herelink SBUS:
- SERIAL7_PROTOCOL = 23
- SERIAL7_OPTIONS = 3 (Swap TX/RX)

Secondary RC Input is provided on **USART1 (SERIAL2)**

Any other UART may also be used for RC input except PPM.

OSD Support
===========

Onboard OSD using the **MAX7456 / AT7456E** driver is supported by default. Fonts are stored in ROMFS and loaded automatically.


VTX Support     iugedui;gfdiuvbidusfiyvasipf///////////////////////////////////////////
===========

The SH1.0-6P connector supports a DJI Air Unit / HD VTX connection. Protocol defaults to DisplayPort. Pin 1 of the connector is 9v so be careful not to connect this to a peripheral requiring 5v.

PWM Output
==========

The BRAHMA H7 supports **13 PWM outputs**:

- Outputs 1–10: Motor outputs
- Outputs 11–12: Servo outputs
- Output 13: WS2812 / NeoPixel LED

All motor outputs support DShot. Output 13 is dedicated to LED control.

Channels sharing the same timer must use the same output protocol and rate.

.. note:: for users migrating from BetaflightX quads, the first four outputs M1-M4 have been configured for use with existing motor wiring using these default parameters:

- :ref:`FRAME_CLASS<FRAME_CLASS>` = 1 (Quad)
- :ref:`FRAME_TYPE<FRAME_TYPE>` = 12 (BetaFlightX) 


Battery Monitoring
==================

The board has a internal voltage sensor and connections on the ESC connector for an external current sensor input.
The voltage sensor can handle up to 6S LiPo batteries.

The default battery parameters are:


   - :ref:`BATT_MONITOR<BATT_MONITOR>` = 4
   - :ref:`BATT_VOLT_PIN<BATT_VOLT_PIN__AP_BattMonitor_Analog>` = 10
   - :ref:`BATT_CURR_PIN<BATT_CURR_PIN__AP_BattMonitor_Analog>` = 11
   - :ref:`BATT_VOLT_MULT<BATT_VOLT_MULT__AP_BattMonitor_Analog>` = 11.01692
   - :ref:`BATT_AMP_PERVLT<BATT_AMP_PERVLT__AP_BattMonitor_Analog>` = 78.43

Compass
=======

No onboard compass is fitted. External compasses are supported on I2C1 and I2C2. Automatic probing is enabled.


Firmware
========

Firmware for this board can be found `here <https://firmware.ardupilot.org>`__ in  sub-folders labeled "BRAHMA H7".

Loading Firmware
================

To flash firmware initially:

1. Press and hold the **BOOT** button
2. Connect USB to the PC
3. Use DFU mode to flash the `with_bl.hex` or firmware‑specific image

Subsequent updates can be applied using `.apj` files (ArduPilot) or the respective configurator tools for PX4, BetaFlight, and iNav.

Warranty and Support
================
The BRAHMA H7 flight controller includes a **6‑month warranty** from the date of purchase, excluding physical or water damage.

Written by Hritam Dey
[copywiki destination="plane,copter,rover,blimp,sub"]