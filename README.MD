# README for lyrics2time

> *This is a small tool for producing an Audacity labels track
> containing lyrics.  Timing is the essential information added
> during a run of the song, simply by pressing Enter at the
> start/end times of a line of the lyrics.*

Audacity labels are stored in plain text files with format

	START [tab] END [tab] LABELTEXT

Where START and END are floating point numbers marking the number
of seconds since the start of the track or song.

Lyrics are fed into `lyrics2time` as a text file with a line
for each (partial) line of the lyrics.  Relatively short lines
seem to work well, for instance what is being sung between two
breaths.  In this case, one presses Enter to indicate a breathing
pause.

Empty lines have a special function.  They mark a pause.  The
normal assumption is that the lines of lyrics are connected,
but an empty line should be used to mark disconnection.

The program counts down 3 seconds when it is started.  This time
can be used to start the song.  We will probably make this an
option, and allow for other forms of synchronisation as well.
The start time is important, because it times the first sentence,
and functions as the basis for all the others following it.

