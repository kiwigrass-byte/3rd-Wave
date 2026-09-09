
# Groove Synthesis 3rd Wave 8M with patch parsing and comparison mode

**Requirements**
- Current public version of preset: 1.5
- Synth must be on at least OS 2.0 (August 2026)
- The 8M is a 2-part synth. The preset might work with the 4-part 24M model, but only for up to 2 parts. To use the 24M change the MODEL_BYTE = 0x02 to 0x01 at the top of the Lua code.
- **IMPORTANT:** In addition to *MIDI param receive* set to CC+NRPN, the preset expects that *MIDI include part in NRPN* is turned on in the global settings.
- The preset is designed for the default factory P and U wavetables. Some adjustment would be needed for other wavetables, including wavetable names and adjusting *count* in WT_SEGMENTS.   
- The preset has the single and part 1 nrpn's sent on MIDI channel 1, and the part 2 nrpn's sending on channel 2. Change accordingly.
- To use the start/stop control for the sequencer set the midi clock source to *in: tempo sync*.
---
**What's in the preset**
- Automatic parsing of a patch when a new patch is selected. The **PATCH SELECT** buttons send a program change message before loading the patch data and mapping to the UI controls. Note that parsing is not immediate because the sysEx dump is over 5k per patch. 
- Turning the **PATCH NAMES** switch 'on' retrieves all the patch names from all banks. The button should toggle to an 'off' state after all 500 names are read. The patch number fader will then display the patch names when scrolling. This process takes a couple of minutes to complete. The patch names are then stored locally on the E1 and are loaded immediately whenever the preset loads. If you later install different patches on the 3rd Wave or move the E1 preset to a different slot on the controller then repeat the process.
- Only parameters for one part can be viewed and edited a time. Use the **PART VIEW** control to switch between the parsed part 1 and part 2 parameter values. 
- Use the **COMPARE** control to switch between an edited sound (and UI) and the original patch sound (and UI). Very useful!
- Thanks to @oldgearguy on the Electra One forum there is a touch screen UI for each of the three 6-stage wavetable-envelopes that makes visualizing and editing much easier and more fun. It should largely mimic the dynamic graphic on the 8M screen except only one envelope is shown at a time.  
- Various button and list controls on the first page mimic the selection buttons on the 3rd Wave's front panel. 
- Controls are hidden when not in use.

----
**What's not in the preset**
- Preset parameters do not update when changed on the 3rd Wave other than a program change. If you edit on the 3rd Wave the UI will get out of sync. 
- No wavetable or multi-sample editing or management.
- No sequencer pattern building.
- No global settings are parsed. A couple of global parameters (dark blue) can be changed from the preset. A sysEx message for global settings is expected.
- No saving of patches.

----

[firmware and manual](https://groovesynthesis.com/support/)

---
 
**OS 2.0 MIDI documentation errors:**
1. For nrpn 165-168 (LFO MIDI note sync) the options of 32 beats, 16, beats, 8 beats, 6 beats are not documented.
2. For nrpn 342 (volume), the scaling is 1.27 not 127
3. For nrpn's 161-164 (LFO frequency) the range is 0-255. Not -127 to +127.
4. There are 0-126 modulation destinations but the documentation refers to less than that: 0-113 for nrpn 35 (Pitch Wheel) and 0-117 elsewhere
5. Doc says that nrpn 345 (fx effect 1 param 4) is not currently used. But it is used for ring mod. nrpn 348 is also used for ring mod in effect 2 param 4

**NRPN Quirks:**
1. Analog waveform display order is "Sawtooth","Square","Triangle","Sine","Super Saw","Pink Noise","Blue Noise". But that requires using nrpn 102-104 values in the order 256, 257, 262, 259, 258, 260, 261
2. nrpn 108-110: osc note reset is not mentioned in manual and not shown in osc display
3. nrpn 424: selected osc button appears to only turn button light on/off
4. nrpn 425: env 3 button appears to only turn button light on/off
5. nrpn 426: env 4 button appears to only turn button light on/off
6. the nrpn values for some FX parameters are not consistent - 0/86/172 for leslie speed, and 0/1, 0/128, 0/255 are used for toggles

**NRPN parameter information:**
- If *MIDI include part in NRPN* is turned on  (global setting) then nrpn 0 is not sent in a sysEx program dump since it is not needed. The nrpn mapping assumes it is starting at nrpn 1 (1st character of patch name)                                                 
- The byte structure of the program sysEx dump is: 9..136 patch name tuples (32), 137..672   single block A, 673..1772  part 1 block, 1773..1788 single block B, 1789..2888 part 2 block

[3rd Wave MIDI CC + SysEx Spec v2.0.xlsx](https://github.com/user-attachments/files/31890242/3rd.Wave.MIDI.CC.%2B.SysEx.Spec.v2.0.xlsx)
[3rd Wave MIDI CC + SysEx Spec v2.0.pdf](https://github.com/user-attachments/files/31797194/3rd.Wave.MIDI.CC.%2B.SysEx.Spec.v2.0.pdf)
[readme_2_0.txt](https://github.com/user-attachments/files/31796956/readme_2_0.txt)
