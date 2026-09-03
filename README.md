MIDI documentation errors:
1. For nrpn 165-168 (LFO MIDI note sync) the options of 32 beats, 16, beats, 8 beats, 6 beats are not documented (it is mentioned in the OS 2.0 release notes).
2. For nrpn 342 (volume), the scaling is 1.27 not 127
3. For nrpn's 161-164 (LFO frequency) the range is 0..255. Not -127..+127.
[readme_2_0.txt](https://github.com/user-attachments/files/31796923/readme_2_0.txt)

Quirks:
1. Analog waveform display order is "Sawtooth","Square","Triangle","Sine","Super Saw","Pink Noise","Blue Noise". But that requires using nrpn value order of 256, 257, 262, 259, 258, 260, 261 

NRPN parameters:
- If MIDI multitimbral mode is enabled (global setting) then nrpn 0 is not sent in a sysEx program dump since it is not needed. This code assumes that MIDI multitimbral mode is on! It is not robust to the mode being off because the nrpn mapping assumes it is starting at nrpn 1 (1st character of patch name)                                                        
- A program consists of 32 nrpn parameters for patch name, 134 single parameters (assuming MIDI multitimbral mode is on), 275 part 1 parameters, 275 part 2 parameters. If the program has n sequencer patterns then there are are also n x 11 sequencer parameters.

