# microbit-midi-guitar version 2

A MIDI guitar using a BBC micro:bit

## Overview


(TODO: Architecture diagram goes here)


* `tone.py` This monitors the pads on the guitar which decide the tones (but not the plucking gestures) and when it notices changes (i.e. when keys are newly pressed or released), it sends a message via serial port that simply states which keys are currently pressed.

* `artmidi.py` This listens for messages from the microbit monitoring the tone pads, and also monitors the articulation pads (those that decide if you're 'plucking' a string or not) and when it notices changes, it creates MIDI messages representing note on and note off events.  It sends these MIDI messages to the computer via serial, to be processed and to eventually trigger audio events in garageband or whatever other software is listening for MIDI events.

* `chords.py` This is a helper program which generates code currently used in `artmidi.py`.  Note that `chords.py` is not _itself_ installed on any microbit.

## About the message sent from `tone.py` microbit to to `artmidi.py` microbit

Currently, this is a single byte, with each bit in the byte acting as a flag to say whether the corresponding key is down or not.  There are currently 8 keys on the guitar that need to be sensed.  For example, in this byte `10000001` it seems the first and last keys are currently pressed.  

The two programs ensure their microbits set their UART up the same way so as to be compatible, and of course they have to be wired together (currently, pin0 on both).

## Installation

* Load tone.py onto the key-handling microbit
* Load artmidi.py onto the other microbit, and connect this one to the computer.




## TODO

* decide on octave positions based on strings (might make it more like a guitar)
