
# Groove Synthesis 3rd Wave 8M with patch parsing and comparison mode

- Synth must be on at least OS 2.0 (August 2026)
- The 8M is a 2-part synth. The preset might work with the 4-part 24M model, but only for up to 2 parts. To use the 24M change the MODEL_BYTE = 0x02 to 0x01 at the top of the Lua code.
- **IMPORTANT:** In addition to *MIDI param receive* set to CC+NRPN, the preset expects that *MIDI include part in NRPN* is turned on in the global settings.
- The preset is built for the default factory P and U wavetables. Some adjustment would be needed for other wavetables, including wavetable names and adjusting *count* in WT_SEGMENTS.   
- The preset has the single and part 1 nrpn's sent on MIDI channel 1, and the part 2 nrpn's sending on channel 2. Change accordingly.
---
**What's in the preset**
- Automatic parsing of a patch when a new patch is selected.
- The **PATCH SELECT** buttons send a program change message before loading the patch data and mapping to the UI controls. Parsing is not immediate because the sysEx dump is over 5k per patch. 
- Turning the **PATCH NAMES** switch 'on' retrieves all the patch names from all banks. The button should toggle to an 'off' state after all 500 names are read. The patch number fader will then display the patch names when scrolling. This process takes a couple of minutes to complete. The patch names are then stored locally on the E1 and are loaded instantly whenever the E1 loads. If you later change teh saved patches on the 3rd Wave or move the preset to a different E1 slot then repeat the process.
- Only parameters for one part can be viewed and edited a time. Use the **PART VIEW** control to switch between the parsed part 1 and part 2 parameter values. 
- Use the **COMPARE** control to switch between an edited sound and the original patch sound. Very useful! 
- Various buttons and list controls on the first page mimic the selection option buttons on the 3rd Wave's front panel. 
- Controls are hidden when not in use.

----
**What's not in the preset**
- Preset parameters do not update when changed on the 3rd Wave other than a program change. Don't edit on the 3rd Wave or the UI will get out of sync. 
- No wavetable or multi-sample editing or management.
- No sequencer pattern building.
- No global settings are parsed. A couple of global parameters (dark blue) can be changed from the preset. 
- No saving of edited patches from the UI.

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
- If MIDI multitimbral mode is enabled (global setting) then nrpn 0 is not sent in a sysEx program dump since it is not needed. This code assumes that MIDI multitimbral mode is on! It is not robust to the mode being off because the nrpn mapping assumes it is starting at nrpn 1 (1st character of patch name)                                                 
- A program consists of 32 nrpn parameters for patch name, 134 single parameters (assuming MIDI multitimbral mode is on), 275 part 1 parameters, 275 part 2 parameters. If the program has n sequencer patterns then there are are also n x 11 sequencer parameters.

[3rd Wave MIDI CC + SysEx Spec v2.0.xlsx](https://github.com/user-attachments/files/31797211/3rd.Wave.MIDI.CC.%2B.SysEx.Spec.v2.0.xlsx)
[3rd Wave MIDI CC + SysEx Spec v2.0.pdf](https://github.com/user-attachments/files/31797194/3rd.Wave.MIDI.CC.%2B.SysEx.Spec.v2.0.pdf)
[readme_2_0.txt](https://github.com/user-attachments/files/31796956/readme_2_0.txt)
