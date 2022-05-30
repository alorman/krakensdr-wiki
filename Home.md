![image](https://user-images.githubusercontent.com/78108016/170861942-ca473872-7b85-4c8c-ab87-9bebba5c9f95.png)
![image](https://user-images.githubusercontent.com/78108016/170861840-a85f09fb-d66c-44b6-b5de-b3771c6ed7af.png)

A coherent radio allows for very interesting applications, such as radio direction finding, passive radar, and beamforming. Some use cases include:

* Physically locating an unknown transmitter of interest (e.g. illegal or interfering broadcasts, noise transmissions, or just as a curiosity)
* HAM radio experiments such as radio fox hunts or monitoring repeater abuse
* Tracking assets, wildlife, or domestic animals outside of network coverage through the use of low power beacons
* Locating emergency beacons for search-and-rescue teams
* Locating lost ships via VHF radio
* Passive radar detection of aircraft, boats, and drones
* Traffic-density monitoring via passive radar
* Beamforming
* Interferometry for radio astronomy

# KrakenSDR vs KerberosSDR
KrakenSDR is the upgraded version of KerberosSDR. The main new feature is that with KrakenSDR calibration is entirely automatic. Unlike with the KerberosSDR where calibration requires that the antennas be disconnected manually each time.

KrakenSDR also has 5-channels vs 4-channel on the KerberosSDR. The additional channel improves bearing accuracy.

The entire design is also improved with USB-C used, an improved low noise design, bias tees, improved cooling and improved ESD protection.

# KrakenSDR Software
This Wiki details the use of our software stack. Our software consists of the core DAQ and DSP software which is designed to run on a Raspberry Pi 4 or similar single board computer that is connected to the KrakenSDR. The second layer of software is an Android App which is used to plot and map the bearing data produced by the core system.

The KrakenSDR software is also compatible with KerberosSDR units. Users will only need to change the configuration file. However, KerberosSDR users will still need to manually disconnect antennas during a calibration cycle (or purchase a third party switch upgrade).


# Videos

**KrakenSDR Direction Finding in a Vehicle:** https://www.youtube.com/watch?v=OY16y1Rl86g

**KrakenSDR Passive Radar Demonstration:** https://www.youtube.com/watch?v=GZAbPsT3oRM