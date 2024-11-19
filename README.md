# 6Sens: inSitu Seismic System for Slope Stability Sensing


## Desciption
The goal is to develop a warning system on the analysis of the evolution of the micro-seismic activity generated before the instability is triggered. The method uses a multitude of low-cost seismic sensors deployed in-situ in a network over the possibly unstable zone. The goal is to characterize the temporal evolution of seismic signals detected simultaneously by several sensors (i .e., co-detection). This method uses to its advantage the heterogeneity of the materials and the attenuation of the waves during their propagation in the material.

The design of these sensors is subject to certain technical constraints essential to good
operation of the project:

    - Be autonomous in energy, over a period of several months (so as not to have to return to site, often dangerous).
    - Be robust, reliable and adapted to extreme climatic conditions (cold, hot, humidity).
    - All sensors in the network must be synchronized precisely enough to perform the analysis (about 1/10 second).
    - Be able to communicate information in real time – or near – measurements to a gateway that will retransmit the data to a dedicated website.
    - Be produced at low cost (to install a large-scale network, and have the possibility of to install sensors in hazardous areas with the possibility of losing them).

## Hardware description
### Geophone sensor
The choice fell on omni geometric sensors from Geospace Technologies such Omni-X-LT or GS-ONE. Seismic geophone is a type of sensor that converts ground movement or a kind vibration into voltage, which could be acquired by an acquisition system. The deviation of this mesured voltage from the base line is called the geophone response and is analysed and for monitoring vibration generated by nature in our case.

The frequency response of the geophone is a kind of harmonic oscillator, which is deternined by corner frequency, around 15Hz for the chosen sensors and damping (typically 0.7 for our case).
Our application require the full wave to be sued and the three-component 3C geophones is used (Omni-X-LT or GS-ONE).
For more information, please to refer to : https://www.geospace.com/products/sensors/

### Amplification/Filtering board
The specifications inform us about the bandwidth of the filtering to be carried out: from 20Hz at 100Hz. So we have to build a band-pass filter having an amplification almost constant on this band and rejects frequencies outside this band. Moreover, the signal will have to be amplified in order to obtain a complete dynamic range between 0 and 3.3V without saturation. Below are listed the
parameters of the different filters that will make up the amplification and filtering card :

    - Filter 1 : active bandpass filter, gain : 33dB, low frequency : 7Hz, high frequency : 154Hz
    - Filter 2 : passive low-pass filter, no gain, cut frequency : 106Hz
    - Filter 3 : active low-pass filter, gain : 6dB, cut frequency : 234Hz

### CPU/Radio board for test
The choice fell on Cicerone MKR main board. Move-X Cicerone LoRa/GNSS Board is a high-performance, low-power, Arduino MKR-compatible development board based on the MAMWLE LoRa Module and the u-blox MAX-M10S GNSS Module. The Cicerone Board delivers best-in-class GNSS, long-range wireless connection, and high-performance MCU processing in a low-power solution for optimal battery life. The Cicerone Board allows users to build tracking applications worldwide with meter-level accuracy and to communicate long-range, low-power data via LoRaWAN. The integrated Li-Po charging circuit enables the Cicerone Board to manage battery charging through the USB port.

### CPU/Radio board for POC
The choice was made to manufacture our own PCB. It has three parts: the MAMWLE-01 radio chipset to transmit LoRaWAN packets (based on an STM32WLE5jx), a UWB chipset DW1000 to measure distance between two sensors and an analog part to supply radio chipset (solar panel or/and Li-Po battery). Connectors (Arduino MKR-compatible) have also been added to insert the seismic sensor amplification/filtering board.

## Firmware description
For this project, the use of Zephyr RTOS has been retained. To see what is Zephyr RTOS and how to install it on your computer, go to https://docs.zephyrproject.org/latest/develop/getting_started/index.html (it supports Linux OS, Windows OS and macOS).