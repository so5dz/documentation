# Modular amateur radio packet ecosystem
Version 1
27 November 2022

## Introduction

This project aims to define software components and the relationships between them suitable to emulate or implement layers 1 and 2 of the OSI model for amateur radio applications.

Viewed as a singular "black box" a full ecosystem built to this specification takes control of an analog radio transceiver, processes audio output coming out of it and exposes a KISS (extended SLIP) interface for use with other applications.

In this view, it is similar to other programs, such as [Direwolf](https://github.com/wb2osz/direwolf) or [minimodem](https://github.com/kamalmostafa/minimodem). The difference lies in strict compartmentalization (that is: complete separation) of the program(s) internals, allowing interoperation of alternative implementations of the defined components.

## Components

There are four components, the first two of which represent the OSI physical layer, the third represents the data link layer and the fourth is transceiver control.

All communication between the components happens over standard network protocols - TCP or UDP. There are no exceptions, even if all components are to be executed on the same host.

### Sound

Component "Sound" is a multi-client server moving audio samples between an audio device and TCP.

A compatible program satisfies the following conditions:

* Multiple clients are served (effectively) simultaneously 
  
* Device input (transceiver output) is broadcast to all connected clients

* Network input is buffered and directed to device output (transceiver input)

* Connected clients do not receive audio sent by each other

* Full duplex operation is permitted
  
* No received network audio is interpreted as silence

* Audio in traffic is represented as signed 16-bit integers in big-endian byte order

* Input/output device sampling rates is specified in configuration

* Network sample transmission/reception rates are identical to the device sampling rates

* ~~Automatic sampling rate conversions are performed in case the configured device sampling rate and network sample transmission/reception rate are different~~

* ~~Basic volume-based squelch is implemented in order to reduce network traffic~~

Documentation for the reference implementation may be found [here](sound.md).

### Modem

Component "Modem" is a multi-client server translating between audio samples and byte-sized symbols. Symbol input/output takes place on port A (or: data port).

Additionally, TX and RX status (Digital Carrier Sense) queries are served on port B (or: extra port). 

A compatible program satisfies the following conditions:

* TODO

Documentation for the reference implementation may be found [here](modem.md).

### Terminal

Documentation for the reference implementation may be found [here](terminal.md).

### Control server

Documentation for the reference implementation may be found [here](control.md).

## Configuration

## Licence note

The programs and documentation in this project are free software: you can redistribute them and/or modify them under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

The programs and documentation in this project are distributed in the hope that it will be useful, but without any warranty; without even the implied warranty of merchantability or fitness for a particular purpose. See the GNU General Public License for more details.

Full text of the GNU GPLv3 Licence is available under <https://www.gnu.org/licenses/>. 