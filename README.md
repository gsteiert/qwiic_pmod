# qwiic_pmod

## Theory of operation

This board connects a MachXO2 between a Qwiic connector and several PMOD connectors.  There is also a small joystic and LEDs for user I/O. There is also a footprint for an oscillator and a button on the program pin.

### I2C

The MachXO2 has hard I2C and SPI blocks that can be used to program the device and are also available to be used in the application.  You shuold note that there are two sets of I2C pins connected to the Qwiic connector.  One goes to the hard I2C block for programming the device, and the other is intended for the user's application.  The hard I2C block works well for programming, but it has some limitations that make it difficult to use in an application.  I would only ever suggest using the hard I2C controller as a master in a user application.  Using the hard controller as an I2C slave should be avoided at all costs. 

Connecting two ports to the connector also simplifies programming.  Choose two different I2C addresses so you can update the code without switching to a programming mode.  The device will always be listening for updates on one address while your application communicate with the other address.

### SPI

The PMOD connector opposite the Qwiic connector is wired up to the MachXO2 SPI programming lines as a peripheral PMOD if you wish to load the part through SPI

### JTAG

The JTAG pins are brought to a tag-connect footprint if needed for recovery.

### Recovery

User applications can disable or interfere with the I2C programming port.  If the image loaded into the device is preventing programming, you should hold down the program button and erase the device while the button remains pressed.

### Feature Row

The default blank state of the feature row enables programming through I2C and SPI, but it can dissable these ports.  In fact, the defualt settings for these bits in Diamond will dissable them unless you go in and change it from the default in the global settings.  When programming the device through I2C or SPI I suggest to avoid programming the feature row unless absolutely necessary.  My example code for loading the device from CircuitPython or Arduino ignore the feature row in the Jedec file for this reason.  The feature row should not be updated with most program updates, only when necessary.

### Programming Examples

These libraries suppoprt both I2C or SPI

* CircuitPython:  [machXOprog](https://github.com/gsteiert/machXOprog)
* Arduino:  [MachXO_Library](https://github.com/gsteiert/MachXO_Library)
