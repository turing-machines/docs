---
layout: post
title:  "I2C read/write"
menuTitle: "I2C read/write"
weight: 10
date:   2019-10-31
categories: [wiki]
description: ""
thumbnail: "img/placeholder.jpg"
disable_comments: true
authorbox: true
toc: true
mathjax: true
tags: [i2c, turing_pi]
published: true
---

I2C read/write quick tutorial

<!--more-->

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
- ADDRESS is the address on the slave from which to read data (eg. 0x00h)

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

## Reference Links
- [Turing Pi assembly](/turing_pi/children/cluster_assembly/)
