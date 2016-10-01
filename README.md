Si570
=====

Si570 Driver

Si570 Arduino library supporting 1 Hz tuning.  This code was
originally intended for supporting local efforts to build
the Minima transceiver designed by Farhan Akhtar.  Existing
implementations of this driver used floating point math on the
arduino that resulted in the minimum frequency change being
greater than 1 Hz.

This driver implements 1 Hz tuning using fixed point math in
the calculations for setting the DCO and various register
settings.

This is the updated version of this driver.  My initial 
implementation that I published suffered from a bug that
caused the DCO to be reset on every update when tuning down
in frequency.  While the frequency was set correctly, the bug
was causing the DCO to restart on every frequency change
producing an audible click in the receiver audio.

The error was two-fold.  First, I failed to reserve sufficient
bits for the 3500 ppm calculation.  Secondarily, the Arduino
absolute value implementation was giving me inconsistent
results (probably my error, but I chose to remove the
function to solve the problem) and it was just simpler to
remove the function from my code.

Lastly, I modified the Si570 code to only calculate the 3500
ppm offset whenever the DCO centre frequency was changed
rather than on every frequency change in order to gain a 
slight performance improvement.
