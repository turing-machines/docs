---
layout: post
title:  "Cluster Management Bus"
menuTitle: "Cluster Management Bus"
weight: 5
date:   2019-10-25
categories: [wiki]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [i2c, cmb, rtc, turing_pi]
published: true
---

Turing Pi cluster management bus configuration, security and internal devices

<!--more-->

### Configure I2C and devices

Add dtoverlay to /boot/config.txt and save

```
dtoverlay=i2c1-bcm2708,sda1_pin=44,scl1_pin=45,pin_func=6
dtoverlay=i2c-rtc,mcp7940x
```
Enable I2C interface in `raspi-config` -> Interfacing Options -> I2C or run `sudo raspi-config nonint do_i2c 1` and reboot 


Check everything is fine with I2C and RTC

```bash
dmesg | grep i2c
[    4.414436] i2c /dev entries driver  # ok

ls /dev/*i2c*
/dev/i2c-1  # ok

dmesg | grep rtc
[    6.489206] rtc-ds1307 1-006f: registered as rtc0

ls /dev/*rtc*
/dev/rtc  /dev/rtc0
```

### I2C tools

Install i2c-tools

```bash
sudo apt-get install i2c-tools
```
Now check our I2C devices on the CMB

```bash
sudo i2cdetect -y 1
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- 04 -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- 57 -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 6f
70: -- -- -- -- -- -- -- --
```

You can see three I2C devices Ethernet Switch (0x04h), I2C expander (0x57h) and RTCC (0x6Fh).

The `i2cget` command is used to read a byte from a specified register on the I2C device. The format for this command is as follows

```
i2cget [-f] [-y] 1 <DEVICE_ADDRESS> <ADDRESS> [MODE]
```

[-f] [-y] Options:

- -f force access to the device even if the device is still busy. However, be careful. This can cause the i2cget command to return an invalid value. We recommend avoiding this option.
- -y disable interactive mode. Using this command will skip the prompt for confirmation from the i2cget command. By default, it will wait for the confirmation from the user before interacting with the I2C device.
- DEVICE_ADDRESS is an I2C bus address (e.g 0x04h)
- ADDRESS is the address on the worker from which to read data (eg. 0x00h)

The optional MODE can be one of the following:

- b – read/write a byte of data, this is the default if left blank
- w – read/write a word of data (two bytes)
- c – write byte/read byte transaction

Example of reading from register 0xF2h where factory default value is 0xFFh

```bash
sudo i2cget -y 1 0x57 0xf2
0xff
```

Use the `i2cset` command to write data to an I2C device. The format of this command as follows

```
i2cset [-m mask] [-f] [-y] 1 <DEVICE_ADDRESS> <ADDRESS> <VALUE> [MODE]
```

Options:

- -f, -y, DEVICE_ADDRESS, ADDRESS as for i2cget
- -m mask the bit mask parameter, if specified, describes which bits of value will be actually written to data-address. Bits set to 1 in the mask are taken from VALUE, while bits set to 0 will be read from ADDRESS and thus preserved by the operation

Example of writing value 0x77h to the first byte of user space SRAM (starts from 0x00h) and then reading

```bash
sudo i2cset -y 1 0x57 0x00 0x77
sudo i2cget -y 1 0x57 0x00
0x77
```

### Security

As a security precaution, system devices are not exposed by default inside Docker
containers. You can expose specific devices to your container using the `--device`
option to docker run, as in

```
docker run --device /dev/i2c-1 app-image
```

or remove all restrictions with the `--privileged` flag

```
docker run --privileged app-image
```

### User space EEPROM

I2C expander and RTCC each have 64 bytes of general purpose user memory, so combined you have 128 bytes of EEPROM.
On device 0x57h user space address from 0x00h to 0x3Fh and on 0x6Fh from 0x20h to 0x5Fh.

### Ethernet Switch

The onboard RTL8370 integrate all the functions of a high-speed switch system; including SRAM for packet
buffering, non-blocking switch fabric, and internal register management into a single CMOS device.

{{% notice note %}}
Device Address: 0x04h
{{% /notice %}}

| Register | Register Description                             | Default Value |
|----------|--------------------------------------------------|---------------|
| 0x00h    | Control Register                                 | 0x1140h       |
| 0x01h    | Status Register                                  | 0x7949h       |
| 0x02h    | PHY Identifier 1                                 | 0x001Ch       |
| 0x03h    | PHY Identifier 2                                 | 0xC980h       |
| 0x04h    | Auto-Negotiation Advertisement Register          | 0x0DE1h       |
| 0x05h    | Auto-Negotiation Link Partner Ability Register   | 0x0000h       |
| 0x06h    | Auto-Negotiation Expansion Register              | 0x0004h       |
| 0x07h    | Auto-Negotiation Page Transmit Register          | 0x2001h       |
| 0x08h    | Auto-Negotiation Link Partner Next Page Register | 0x0000h       |
| 0x09h    | 1000Base-T Control Register                      | 0x0E00h       |
| 0x0Ah    | 1000Base-T Status Register                       | 0x0000h       |

#### Network Speed

```bash
# 0x2040: Bitmask
# 0x2000: 1000Mbps
# 0x0040: 100Mbps
# 0x0000: 10Mbps

# Set network speed to 1000Mbps
sudo i2cset -m 0x2040 -y 0x04 0x00 0x2000 w
```

#### Power Up/Down

```bash
# 0x0800: Bitmask
# 0x0800: Power down
# 0x0000: Normal operation

# Power down
sudo i2cset -m 0x0800 -y 0x04 0x00 0x0800 w

# Power up
sudo i2cset -m 0x0800 -y 0x04 0x00 0x0000 w
```

### I2C expander

I2C expander offers users a digitally programmable alternative to hardware
jumpers and mechanical switches that are being used to control power on compute nodes.

{{% notice note %}}
Device Address: 0x57h
{{% /notice %}}

| Register       | Register Description                             | Default Value |
|----------------|--------------------------------------------------|---------------|
| 0x00h to 3Fh   | 64 bytes of general-purpose user EEPROM          | 0x00h         |
| 0xF2h          | Control Register                                 | 0xFFh         |
| 0xF8h          | Status Register                                  | --            |
| 0xFAh to 0xFFh | 6 bytes of general-purpose user SRAM             | --            |

#### Power Management

On/off compute module through register 0xF2h

```bash
# Bits  : 76543210
# Slots : 5674321x

# Power off worker nodes 2,3,4,5,6,7
sudo i2cset -m 0xfc -y 1 0x57 0xf2 0x00

# Power on worker nodes
sudo i2cset -m 0xfc -y 1 0x57 0xf2 0xff
```

On/off compute module by node number

```bash
# 0x02 : Node #1 (Master)
# 0x04 : Node #2 (Worker 1)
# 0x08 : Node #3 (Worker 2)
# 0x10 : Node #4 (Worker 3)
# 0x80 : Node #5 (Worker 4)
# 0x40 : Node #6 (Worker 5)
# 0x20 : Node #7 (Worker 6)

# Power off node #3
sudo i2cset -m 0x08 -y 1 0x57 0xf2 0x00

# Power on node #7
sudo i2cset -m 0x20 -y 1 0x57 0xf2 0xff

```

Read on/off status

```bash
sudo i2cget -y 1 0x57 0xf2
0xff
```

#### Compute Module status

Read compute module status through register 0xF8h

- 1 = Installed in slot AND switched on
- 0 = Not installed in slot OR switched off

```bash
# Bits  : 76543210
# Slots : 5674321x

sudo i2cget -y 1 0x57 0xf8
0x0e  # register 0xf2 = 0xff, all slots are power up but installed only three
```

### Real-Time Clock/Calendar

Real-Time Clock/Calendar (RTCC) tracks time using internal
counters for hours, minutes, seconds, days, months, years, and day of week.
Alarms can be configured on all counters up to and including months.

SRAM and timekeeping circuitry are powered from the back-up supply when main
power is lost, allowing the device to maintain accurate time and the SRAM
contents. The times when the device switches over to the back-up supply and
when primary power returns are both logged by the power-fail time-stamp.

{{% notice note %}}
Device Address: 0x6Fh
{{% /notice %}}

| Register       | Register Description                             | Default Value |
|----------------|--------------------------------------------------|---------------|
| 0x00h to 0x06h | Time & Date                                      | --            |
| 0x07h to 0x09h | Configuration and Trimming                       | --            |
| 0x0Ah to 0x10h | Alarm 0                                          | --            |
| 0x11h to 0x17h | Alarm 1                                          | --            |
| 0x18h to 0x1Fh | Power-Fail/Power-Up Time-Stamps                  | --            |
| 0x20h to 0x5Fh | 64 bytes of general-purpose user SRAM            | --            |

#### Time & Date

Show time from hardware RTC

```bash
sudo hwclock --show
2019-10-26 20:21:03.005326+01:00
```

### External I2C port

Pinouts

```
|  1  |  2  |  3  |  4  |
| GND | VCC | SCL | SDA |
```

## Reference Links
- [I2C tools](/turing_pi/children/i2c_read_write/)
- [I2C expander datasheet](https://datasheets.maximintegrated.com/en/ds/DS4520.pdf)
- [RTC datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/MCP7940N-Battery-Backed-I2C-RTCC-with-SRAM-20005010G.pdf)
