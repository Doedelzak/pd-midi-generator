# GENERATOR


This patch transforms the computer into a MIDI improviser. However, it only improvises according to the general directions given by a musician. Playing with this program is like telling the improvising computer in real time: "Go faster," "modulate to A minor," "play in the high range," "play more notes," "now fewer notes," "more chaotic!", "more rhythmically structured," "more rhythmically free," etc.

The UI elements are marked by comments on yellow canvases within the patches. They consist of a mouse control (button, switch, slider...) and a "ctlin" object to use an external MIDI controller if available. To match the controls with your MIDI equipment, simply change the argument of the "ctlin" objects to the MIDI CC numbers you use on your controller.

IMPORTANT: 
This program doesn't generate any sound. It only generates MIDI data. Therefore, you need to set up the MIDI output in Pure Data to send it to the MIDI device of your choice.


## PATCH DESCRIPTION


#### generateur.pd:
Main patch wrapping the others.

The "START" switch is an on/off button.

The "MIDI CHANNEL" variable allows you to select the MIDI output channel. If you don't change it, the MIDI channel will be 1 (even if the number displays 0).


#### tempo.pd:
This patch contains two metro objects. The "TEMPO" is the general pulse. The "RESOLUTION" is the maximum rhythmic division of this initial pulse.

The "TEMPO" slider controls the speed of the general pulse.

The horizontal "RESOLUTION" buttons allow you to select the maximum division of this pulse. Note: only binary divisions are available.

CAUTION: On this patch, the polarity of the sliders is inverted. You need to lower the sliders to speed up the tempo or increase the divisions.


#### freqnotes.pd:
This patch filters the impulses from the maximum division.

The "FREQUENCE" slider defines, from the metronome impulses, the density of notes that will actually be played.


#### rythmes_intensites.pd:
"POURCENTAGE ALEATOIRE RYTHME" slider: When this value is at its lowest, all notes will be played to the rhythm of the general pulse. When this value is at its highest, all notes will be played on subdivisions of the pulse (offbeat). The intensities are random but will generally be stronger on the general pulse.


#### modes2.pd :
Each button determines the mode with which the program will play. Available are the 7 traditional modes, the 7 modes of Messiaen, the twelve-tone mode, and a "CUSTOM" mode with empty lists to create your own scale. The modes consist of two lists of MIDI numbers: on the left, a list of pitches constituting the mode, and on the right, a list of pole notes of this mode.

The "FONDAMENTALE" slider allows you to choose the root note on which the mode's scale will be built.


#### notesnew.pd : 
This patch decides the notes that will be played.

The "TESSITURE" slider sets the lowest note of the range.

The "AMBITUS" slider determines the range's amplitude, starting from the lowest note defined by "RANGE."

The "% ALEATOIRE" slider determines the randomness percentage of the notes. Specifically, it determines if a note should be randomly chosen within the range or determined by the average of the last four notes played.


#### durees.pd : 
This patch works similarly to notesnew but decides the duration for which the notes are held.

The "DUREE MINIMUM" slider sets the shortest possible duration.

The "DUREE MAXIMUM" slider sets the longest possible duration.

The "% ALEATOIRE" slider determines the randomness percentage of the durations. Specifically, it determines if a duration should be randomly chosen between "DUREE MIN" and "DUREE MAX", or determined by the average of the last four durations.

freqnotes2.pd, rythme_intensites2.pd, notesnew2.pd, durees2.pd are copies and work exactly the same as their counterparts. The only difference is that the list sent by modes2.pd to notesnew2.pd will consist only of the pole notes of the chosen mode, while notesnew.pd is fed by the complete scale of the mode. This allows for generating two voices: the first one will have a more melodic role, and the second one a more harmonic role.


Have fun!

Benjamin Bouvrot (alias Doedelzak)
