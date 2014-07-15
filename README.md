Hardware traffic generator
==========================

This is a 10 Gbit/s Ethernet FPGA-based traffic generator. It is designed to be both flexible and extensible, and to be able to fill a 10Gb/s link, even with the smallest packets. It is described in ["Flexible, extensible, open-source and affordable FPGA-based traffic generator" in HPPN '13](http://dl.acm.org/citation.cfm?id=2465843).

Environment
-----------

### Hardware

This implementation is tested with the [COMBO-LXT board](http://www.invea-tech.com/products-and-services/combo-fpga-boards/combo-lxt) with a [COMBOI-10G2](http://www.invea-tech.com/products-and-services/combo-fpga-boards/comboi-10g2) interface extension. The board must be plugged in a PCI port of a hosting machine.

As the implementation is made for [the NetCOPE platform](http://www.invea-tech.com/products-and-services/netcope-fpga-platform), it should work with few changes on any board supported by the platform, including the NetFPGA 10G. 

### Software

The VHDL code provided has no dependencies to the NetCOPE platform. You can simulate and synthesize the top `traffic_generator` entity using just Xilinx ISE for example (tested with version 13). To use it on the board, integrate it in a NetCOPE `application.vhd` file.

The C code (communication with the generator) has dependencies to the NetCOPE platform, it must be compiled on a platform with NetCOPE installed. A `Makefile` is provided.

The Python code (GUI) has dependencies to the PyQt library only.

Directory structure
-------------------

This repository is divided into:

* `hw`, which contains the code that goes on the board;
* `sw`, which contains the code to control the board from the computer;
* `samples`, which contains a sample configuration.

The top file of the hardware code is `traffic_generator.vhd` ([see documentation](hw/traffic_generator)). It has to be included in `application.vhd` and connected to a FrameLink bus that comes from DMA and goes to OBUF.

The `config_gui` program ([see documentation](sw/config_gui)) is a Graphical User Interface to generate configuration files for the generator.

The `traffic_generator` program ([see documentation](sw/traffic_generator)) enables to send configuration from a configuration file (generated by the GUI, an example is available in the sample directory).

Development status
------------------

Currently, the generator works and sends traffic at the expected speed. We are actively working on some modifier blocks that will be committed soon. Send us an email if you feel some blocks should be there and are not.

Documentation is at an early stage, so if you have trouble understanding how to use or extend the generator, do not hesitate to send us an email.