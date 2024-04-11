# Getting Started with the Teensy 4.0+

This guide will walk you through the process of setting up a development environment for programming the [Teensy 4.0/4.1](https://www.pjrc.com/teensy/).

## Prerequisites

1. Follow the instructions laid out [here](https://www.pjrc.com/teensy/first_use.html) to ensure your board is in working order.
2. If you plan to use the [Arduino IDE](https://www.arduino.cc/en/software), follow the guide [here](https://www.pjrc.com/teensy/td_download.html) to install Teensyduino.
3. There is also a CLI `teensy_loader_cli` that can be used to compile and upload programs to the teensy. For more information see below.

### Teensy Loader CLI

#### Linux

The easiest method for installing `teensy_loader_cli` is to use your distro's package manager. This guide was written using Ubuntu 22.04.

```bash
sudo apt-get install libusb-dev
sudo apt-get install teensy-loader-cli
```

#### Windows

#### Usage and Command Line Options

For more information see the [official documentation](https://www.pjrc.com/teensy/loader_cli.html).

In Unix based systems you can view the options with the `man` command.
```bash
man teensy_loader_cli
```


#### Makefile Integration
It is recommended that developers integrate `teensy_loader_cli` into their Makefile.


## Arduino CLI

For information on how to install the `arduino-cli` see the [official documentation](https://arduino.github.io/arduino-cli/0.35/).

It is recommended to create the [command line completion](https://arduino.github.io/arduino-cli/0.35/command-line-completion/) script for ease of use.


### Create a configuration file

```bash
arduino-cli config init
```


### Install the Teensy AVR core

```bash
arduino-cli core install teensy:avr
```


### Creating a new Sketch

```bash
arduino-cli sketch new MySketch
```

### Attaching the Board

To have the [Arduino Language Server](https://github.com/arduino/arduino-language-server) understand the project, we must create a configuration file.

```bash
arduino-cli board attach -p /dev/ttyS0 -b teensy:avr:teensy40 MySketch
```

This will create a `sketch.yaml` file that looks something like this:

```yaml
default_port: /dev/ttyS0
default_fqbn: teensy:avr:teensy40
```

For more information about configuration files, see [here](https://arduino.github.io/arduino-cli/0.35/sketch-project-file/).


### Compiling and Uploading a Sketch

To compile a sketch to the teensy you can use the following command:
```bash
arduino-cli compile --fqbn teensy:avr:teensy40 blink
```

To upload a sketch:
```bash
arduino-cli upload -p /dev/ttys0 --fqbn teensy:avr:teensy40 blink
```

To simplify the process, it is possible to combine both commands into a single command string:
```bash
arduino-cli compile --fqbn teensy:avr:teensy40 blink && arduino-cli upload -p /dev/ttys0 --fqbn teensy:avr:teensy40 blink
```

### Adding Libraries

You can search for libraries available in the Arduino ecosystem with the following command:
```bash
arduino-cli lib search MY_LIB
```

Libraries can be installed via the following command:
```bash
arduino-cli lib install MY_LIB
```

