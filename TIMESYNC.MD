# Time Synchronisation for Lyrics Labels

> *Audacity plays audio with a certain delay.
> This means that the press of the play button
> does not line up with the timing at which
> enter is pressed.  This is how to correct that.*

**TODO:** We still need the option to setup delay.

Audacity has facilities for synchronisation, used
when playing in tracks while Audicity is producing
sound from previously prepared tracks.  The
[Device preferences](https://manual.audacityteam.org/man/devices_preferences.html)
hold Latency Compensation for the combined delay
from playback and recording buffers.  A simple
[Latency Test](https://manual.audacityteam.org/man/latency_test.html)
can be executed to find the value with better
resolution than your ear can detect.

The delay that we need here is the output delay
only.  This would (probably) be the Buffer Length.
This value however, is not derived in the Latency
Test, but a similar procedure can be followed:

 1. Ensure the settings in the Recording and Devices
    tabs are set as for the Latency Test.
 2. Generate the same Rhythm Track as used for the
    Latency Test.
 3. Run `lyrics2audacity` on the `demo/tictactoe.txt`
    file, playing back the Rhythm Track and pressing
    enter on each tick.
 4. Import the timed version of `tictactoe.txt` as a
    Labels Track.
 5. Determine the delay in a similar manner as for
    the Latency Test.
 6. Alternatively, compare the precise timing in the
    Rhythm Track with the timing values recorded in
    the timed version of `tictactoe.txt` and compute
    manually the distance in seconds.  Multiply by
    1000 to infer milliseconds.


## Determining and Removing Output Latency

After loading the labels, find the tick on the
Rhythm Track that aligns with the first beat.

Plece the hair line on the first label, and read
the Audio Position in seconds.  Compare it to the
expected value from the exact beat.  The difference
is the amount of time to remove.

Set the Audion Position to Start and End of Selection.
Select the label track.  You can now drag the hairline
from the rough beginning time of the tick in the
Generated Rhythm track and pull to the label position
(it should magnetise to that position).
Now edit the roughly set Start of Selection and set it to the
accurate generated time.  Use the Cut operation to
remove the excess time.

If you like, you can use the Karaoke View to verify the
label timing.  But you will see it easily in the waveform
display too.


## Manual Correction by Example

An alternative method processes the timing in
`tictactoe.txt` manually.  It is neither more or less
accurate, but it lends itself better to automation.

After running `lyrics2audacity` on `tictactoe.txt`
the file could hold the following timing information:

```
2.864317	3.384444	sync #1
3.384444	3.857369	sync #2
3.857369	4.353579	sync #3
4.353579	4.824730	sync #4
4.824730	5.312683	sync #5
5.312683	5.832461	sync #6
5.832461	6.356016	sync #7
6.356016	6.809485	sync #8
```

(You can probably tell that I am not a percussionist,
certainly not on a keyboard.)

This was recorded with 120 beats per minute, 4 beats
per bar and a high-enough number of bars.  The first
bar was skipped, but because `tictactoe.txt` starts
with an empty line this ends up as an initial pause.

If we add all start times, we should find the total of
4, 5, ..., 11 bars or 60 bars.  At 120 beats per minute,
we would expect 60 bars to span 60 times 0.500000 seconds
or 30.000000 seconds.  In reality, the sum is 36.785599
or 5.785599 seconds too high.  This value stems from
8 measurements, so on average they are 0.848200 seconds
or 848.200 milliseconds later than expected.  (If you
think this computation is odd, then just follow your
own reasoning.  This funny method just averages out
manual timing mistakes.)

**TODO:** This is an absurd amount of delay, measured on
an Apple MacBook Air through its builtin speakers.  It
may need double checking.

**TODO:** Explain the option to use to subtract this time.

**TODO:** We could also use an option to just correct a
particular point to a particular start time.  Complain
when the file does not start with a pause, or one that
is not long enough.

