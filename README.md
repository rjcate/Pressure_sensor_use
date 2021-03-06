
# Setup

## Install software on Teensy

  1. Install Arduino IDE
      * https://www.arduino.cc/en/Main/Software
  2. Install Teensyduino, dowload and instructions are available here
      * https://www.pjrc.com/teensy/td_download.html
  3. Plug in Teensy and select proper board and port
      * Tools -> Board -> Teensy 3.1/3.2
      * Tools -> Port -> Select Teensy Port
  4. Download pedvide ADC library and add to Arduino
      * Download as .zip from https://github.com/pedvide/ADC
      * In the Arduino IDE: Sketch -> Include Library -> Add .ZIP Library
      * Select downloaded .zip
  5. Download and open appropriate `.ino` file and Click 'Upload'

## Pull data with Python

Use one of the scripts here or write your own to find and pull data from
the serial port. The current recommended firmware is
`dual_diff_read_with_interval_timer.ino`.

Sending `s ####` will set the sampling period to #### us.
We usually operate pulling data every 1 ms (`s 10000`).
Sending `s` or `s 0` will stop sampling.

# Hardware

## Teensy 3.2

The Teensy 3.2 has two ADCs with internal amplifiers that can run in
differential mode. In differential mode each ADC can only use certain pins.

```
A10 - ADC 0 diff +
A11 - ADC 0 diff -
A12 - ADC 1 diff +
A13 - ADC 1 diff -
```

![Teensy 3.2 Rear pinout](/images/teensy3.2_pinout_rear.png)

## Honeywell 24PCFFA6G Pressure Sensor

Sensor details can be found [here](https://sensing.honeywell.com/24PCFFA6G-unamplified-board-mount-pressure-sensors).

Pertinent details from the datasheets:

![24PCFFA6G Drawing](/images/Honeywell_24PCFFA6G_pressure_sensor_diagram.png)
![24PCFFA6G Wiring](/images/wiring_diagram.png)

Note:

  * **Pin 1 is notched** (very slightly, you'll really have to look for it)
  * 2.5-12 V supply voltage, typical is listed at 10 V. Higher
    voltage -> better SNR
  * Our sensors use gague measurement relative to ambient pressure and
    and are rated for 100 PSI
  * Increasing pressure results in increasingly negative differential
    voltage between pins 2 and 4

## Wiring

* Connect the USB output to computer
* Connect sensor pin 1 to V+ (source voltage, 1.5-12V)
* Connect sensor pin 2 to Teensy pin A10 for ADC0 (or A12 for ADC1)
* Connect sensor pin 3 to V- (source ground)
* Connect sensor pin 4 to Teensy Pin A11 for ADC0 (or A13 for ADC1)

# Software

`gui_live.py` provides a fast, simple user interface.

For more details about how embedding the live animation in the PySimleGUI
frontend works, see this article:
  * https://matplotlib.org/3.1.0/gallery/user_interfaces/embedding_in_tk_sgskip.html)
