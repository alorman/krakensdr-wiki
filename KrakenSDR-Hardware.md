# Technical Specifications

* Dimensions: L: 177mm x W: 112.3mm x H: 25.86mm (+4.7mm height for fan finger guard) (See appendix for drawing)
* Weight: 670g
* Typical Power Consumption: 5v, 2.2A (11W)
* Radio Tuner: 5x R820T2
* Radio ADC: 5x RTL2832U
* ADC Bit Depth: 8-bits
* Frequency Range: 24 MHz -1766 GHz
* Maximum Channel Bandwidth: 2.56 MHz
* RX Channels: 5
* Oscillator Stability: 1PPM

# KrakenSDR Hardware Descriptions

![side](https://user-images.githubusercontent.com/78108016/169803278-2ec366e6-40e5-4ac8-a9a0-f91b6deebb16.png)
![TOP](https://user-images.githubusercontent.com/78108016/169803288-50f3b191-4710-47cd-abc8-377bbac2945c.png)

## KrakenSDR Power Port
The KrakenSDR requires DC power from a 5V 2.4A capable USB-C power supply. It is also compatible with ‘PD’ type USB-C power packs that you might find used with laptops.

For use in vehicles, it is possible to use USB cigarette lighter adapters. Make sure that they can support at least 5V 2.4A out. Battery packs can also be used if they support 2.4A or more output current.

Bias Tee Note: The KrakenSDR draws 2.2A under nominal operation. If you intend to use the bias tees to power external devices, please ensure that you use a power pack capable of providing the power required. For example, if you are using a 3A capable power pack, you will have about 800 mA of current margin.

## KrakenSDR Data Port
The KrakenSDR requires a USB-C cable to connect the computing device to the data port. Please note that this data port is not connected to power, so you cannot power the device from the data cable. You must use the data cable AND the power cable together.
Make sure that you use a high-quality USB-C cable, no longer than 1m in length.  
 
## KrakenSDR Cooling
The KrakenSDR is passively cooled by heatsink fins and actively using a cooling fan. Internally the PCB is thermally connected to the cooled enclosure using thermally conductive silicon.

KrakenSDR has been tested to operate normally in ambient temperatures of up to 50C / 122F.

We recommend keeping your KrakenSDR out of direct sunlight and in an area with sufficient air flow.

Large sudden temperature swings may cause issues with phase coherence calibration being lost. 

## SMA Ports
The KrakenSDR has 5 SMA RX IN ports for connecting antennas labelled from CH0 to CH4.

## Bias Tee
The KrakenSDR can provide 4.5V DC via a bias tee on each of its SMA ports. This can be used for powering external RF components such as an LNA. Your power pack must be able to provide sufficient current to support external devices.
 
## Status Lights
The KrakenSDR provides peep holes for several status LED indicators.

**PWR LED:** The white PWR LED to the right of the two USB-C ports indicates that the KrakenSDR is receiving DC power from the POWER USB-C port.

**NOISE LED:** When illuminated the white NOISE LED to the right of the PWR LED indicates that the noise source on the KrakenSDR is active. This LED may flash briefly every few minutes when running the software when calibration monitoring/auto recalibration is turned on.

**CHANNEL LEDS:** There are five blue CHANNEL LEDS next to each of the SMA ports. When illuminated, these LEDs indicate that this channels tuner has been enumerated by the computing device. Please note that these LEDs do not provide status regarding the channel connection to the DSP software.

# KrakenSDR Design

The KrakenSDR coherent design consists of:

* 5x RTL-SDR tuners (with R820T and RTL2832U chips)
* 1x single clock source for all RTL-SDRs
* 1x noise source
* 5x noise / antenna port switches
* 1x USB hub

The KrakenSDR is not a naturally coherent system just by its SDR hardware alone. However, its design with a single clock source and software activatable noise source with switches, allows for phase coherence to be achieved in software through implementing correlation algorithms that synchronize samples and phase between the receivers. 

Once the software has booted, the noise source will be activated, and each channel automatically correlated against the master channel (CH0 by default). Any sample timing and phase differences between the channels will be determined, and each sample’s timing and phase will be automatically adjusted in software. This results in the coherent operation of all five channels.