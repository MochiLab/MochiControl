# MochiControl
Mochi Lab uses this flexible National Instruments LabVIEW experiment control application, based on the producer-consumer design pattern, to allow operators real-time control over all experimental settings, including 16 timing channels with a dynamic timing map, 120 digitizer channels, and a settings save and load interface powered by MDSplus.
The hierarchical MDSplus tree stores all experiment settings such as capacitor bank voltages and discharge times together with all data acquired through National Instruments PXI-6133 and NI-5752 digitizer cards, Tektronix TDS-2024B oscilloscopes, and a Princeton Instruments PI-MAX 3 fast framing camera.
The experiment control application can also accesses stored settings through the MDSplus LabVIEW interface which leverages the object oriented and multi-threaded features of MDSplus.
To control the experiment the application switches digital outputs of a PXI-6602 timing card connected through fiber optics to relays in the bias coil and plasma gun capacitor banks to achieve the desired charging voltage.
The application transmits the desired experiment timings to the PXI-6602 cards which use on board clocks to generate optically isolated trigger pulses for the gas puff valves, oscilloscopes, bias coil and plasma gun capacitor banks.
The optical isolation is achieved with TTL-optical transmitter circuits, and DC and fast optical-TTL receiver circuits at the experiment (Carroll 2016).

## Requirements
### Software Dependencies
The following software can be downloaded from the National Instruments website.
* LabVIEW 2015 (or later)
* DAQmx
* NI-Sync
* MathScript
* LabVIEW FPGA module
* FlexRIO drivers
* FlexRIO adapter drivers

* MDSplus  (the directory with the Vis has to be copied to the LabVIEW directory)

### Hardware Setup
This code is designed for this specific hardware.
* PXI-1042Q chassis with
    * PXI-MXI-4 (communication with PC)
    * PXI-6653 (synchronization card)
    * 2x PXI-6602 (Timing cards with 8 channels each)
    * 3x PXI-6133 (Digitizers each 8 channel 2.5 MS/s 14 bit)
* PXIe-1082 chassis with
    * PXIe-8375 (communication with PC)
    * 3x PXIe-7962R with NI-5752 (Digitizers each 32 channel 50MS/s 12 bit)
    * PXIe-6672 (synchronization card)

## Important Files
**Experiment_Control.lvproj** project file this file should be opened with LabVIEW


**Modules/mochifpgacontrol/FPGA bitfiles/MochiFPGAControl_2016-11-29_generic_register_setting_5f6bfda_K10_digital_filters.lvbitx** this bitfile muust be loaded on the FPGAs with NI-MAX

## Setup
* The code is setup to synchronize two chassis (one leader, one follower).
The synchronization cards, one in each chassis should be connected with two coax cables.
One coax cable should connect PFI 0 of the leader to PFI 1 of the leader and the other cable PFI 2 of the leader to PFI 0 of the follower.
The bitfile has to be loaded onto the FPGA, one way to do this is with NI MAX and the update firmware option.

* The bitfile has to be loaded onto the FPGA, one way to do this is with NI MAX and the update firmware option.

* The NI components have to be named in NI-MAX as follows:
PXIe-1082 -> Chassis 1
PXIe-7962R -> RIO[0-2]
PXIe-6672 -> Sync0

PXI-6653 -> Sync
PXI-6602 -> Timing[0-1]
PXI-6133 -> DAQ[0-2]

* an MDSplus tree named 'op_tree' has to be created with the MochiModel software referenced below.

## Adapting the code to new hardware
Adapting this code to new NI components requires significant work.
Woodruff Scientific, Inc. designs and installs Controls, Data Access and Communication (CODAC) systems.
http://www.woodruffscientific.com/codac

## Reference
* Jens von der Linden. (In preparation). Investigating the Dynamics of Canonical Flux Tubes (Doctoral dissertation). Chapter 4. University of Washington.
* Alexander Card. (In preparation). A new measuremnet of electron densities in the MOCHI LabJet experiment using an unequal path length, heterodyne interferometer (Master's thesis). University of Washington
* Alexander Card. (2017). MochiModel. https://doi.org/10.5281/zenodo.495631
* Evan Carroll (2016). Driving Flows in Laboratory Astrophysical Plasma Jets: The Mochi.LabJet Experiment (Master's thesis). University of Washington.

## Acknowledgments
James Stuber and Woodruff Scientific, Inc. provided the lab with our initial NI hardware, code, and ongoing support.

## Contact
Jens von der Linden jensv@uw.edu
Alexander Card card@uw.edu
