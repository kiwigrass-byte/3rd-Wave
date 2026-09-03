MIDI documentation errors:
1. For nrpn 165-168 (LFO MIDI note sync) the options of 32 beats, 16, beats, 8 beats, 6 beats are not documented (it is mentioned in the OS 2.0 release notes).
2. For nrpn 342 (volume), the scaling is 1.27 not 127
3. For nrpn's 161-164 (LFO frequency) the range is 0..255. Not -127..+127.

Quirks:
1. Analog waveform display order is "Sawtooth","Square","Triangle","Sine","Super Saw","Pink Noise","Blue Noise". But that requires using nrpn value order of 256, 257, 262, 259, 258, 260, 261 

NRPN parameters:
- If MIDI multitimbral mode is enabled (global setting) then nrpn 0 is not sent in a sysEx program dump since it is not needed. This code assumes that MIDI multitimbral mode is on! It is not robust to the mode being off because the nrpn mapping assumes it is starting at nrpn 1 (1st character of patch name)                                                        
- A program consists of 32 nrpn parameters for patch name, 134 single parameters (assuming MIDI multitimbral mode is on), 275 part 1 parameters, 275 part 2 parameters. If the program has n sequencer patterns then there are are also n x 11 sequencer parameters.

[readme_2_0.txt](https://github.com/user-attachments/files/31796956/readme_2_0.txt)
3rd Wave OS version 2.0

new in verison 2.0a:
 - New Shimmer Reverb added to the list of effects for Effect 2
    * - The new shimmer reverb is quite heavy on the Third Wave's CPU. For the 24-voice models, while effects are allowed across all four parts, parts 1 and 3 share one effect core, and parts 2 and 4 share another. Consequently, you can only use the shimmer reverb on one part per pair. For example, if shimmer is active on part 1, it cannot be used on part 3. 
    * - Additionally, you cannot run any other reverb or heavy effect (such as the Echoplex or Leslie speaker) on a core that is currently running the shimmer effect. If you attempt to do so, a message will appear in the effects window indicating that your effect options are limited to a smaller, available selection. The 8M is not affected by this limit due to the fact that it only has two parts.
 - Improved Make Waves functionality - automatic wavetable maker has been noticeably improved, including the addition of a new spectral mode that analyzes the audio from start to end in the frequency domain
 - Expanded MIDI CC mappings for 24voice module and 8M. See MIDI implementation spec for more info
 - New MIDI SysEx functionality for importing and exporting wavetables.
 - New MIDI SysEx functionality for importing and exporting multisamples
 - New option for Envelope Retrigger Mode in MISC settings, “reset from 0 (fast click)”, which will reset envelopes to 0 with smoothing disabled, so it will reset quickly and might have an audible click
 - New GLOBAL option “MIDI include part in nrpn”, when set on the 3rd Wave will add an offset for each part so that per part settings have unique nrpns instead of relying on nrpn 0. See MIDI implementation spec for more info
 - Various bug fixes for controlling synth via MIDI nrpn
 - Bug fix for mono and free running LFO modes to ensure they are resynchronized appropriately when switched back and forth.
 - Bug fix for issues reading .wav audio files with troublesome meta-data included in the header
 - Bug fix for mute control on the internal sequencer
 - Bug fix for sequencer transpose mode with keyboard splits
 - Bug fix for issues found on the 8M in audio quality routing audio input through synth engine
 - Bug fix for 8M UI issues to make transition from one waveform to the next smooth in the wavetable display.


new in version 1.9c:
 - improvements to multitimbral playback to remove clicking sound when voices are stolen from a different part.
 - improvements to make the effects processing faster to prevent new cpu overages on patches with many effects active.
 - new option for ring mod effect to choose when the note tracking resets (on note off or after release).
 - improvements to prevent screen from jumping back and forth when you change two paramters at the same time.
 - added midi CC 7 for volume on the 8M

new in version 1.9b:
 - adjusted threshold in function test for manufacturer to find defects in audio dac hardware
 - improvement to playing multiple parts with unison enabled in multitimbral mode, so part release stage is not cutoff by a different part
 - fix for midi nrpn transmission when hold latch mode is set to specify which part is being updated.

new in version 1.9a:
 - new unified program data import and export to simplify importing presets with their associated data, like samples and wavetables. This will include all data used by the preset in a single file.
 - added sample start modulation destination.
 - added MONO LFO reset mode so LFOs for all voices will stay in sync.
 - added support for MIDI expression and MIDI breath controller mod sources.
 - added global setting to disable automatic usb drive mounting.
 - added option to set latch mode to chord when HOLD is on. Previously this was only available if the arp was enabled. See latch tab in HOLD screen.
 - added option to set output routing globally and not per preset. See global button in output routing screen.
 - added button shortcut, double press GLOBAL will return to home screen.
 - GLOBAL and MISC menus will now have the last selected row enabled instead of reseting to the top row.
 - added shortcut for mod destinations for LFOs on desktop module. Press an LFO button while you hold down the mod destination button.
 - improvements to make encoder scanning more robust and reliable.
 - improvements to voice allocation in multitimbral mode, especially if multiple parts use unison.
 - improvements for MIDI nrpn handling so button LEDs stay in sync with parameter changes.
 - remapped MIDI CC numbers 65, 66, 67 to remove conflict with commonly used MIDI CCs in DAWs.
 - added option for filter velocity to envelope setting to have velocity add to the env instead of multiply/scale.
 - added lfo fine amount parameter.
 - changed triangle LFO to start at 0 after delay instead of -1.
 - changed sustain pedal midi CC on value to 127 instead of 64.
 - bug fix for midi SysEx bank export/import where bank was erroneously being reset.
 - bug fix to prevent crash when wave maker is armed for recording and synth receives midi control data.
 - bug fix for filter in stereo delay effect.

new in version 1.8f:
 - Fix for issue introduced in 1.8e where filter env, env 3, env 4 can lag behind amp envelope for stolen voices.
 - Fix for Serum wavetable import when table only has 4 waveforms making it the same size as our P wavetables + improvements to better handle different table sizes.

new in version 1.8e
 - Sequencer updates: updates to sequencer to always treat the four parts independently like separate tracks. Previously independent tracks were only available if you had one part active at one time. Also reordered the buttons to prevent accidently clearing the sequence and added new button to clear only the notes in sequence and keep the parameter automation. Improved logic if you record over the same note in a sequence.
 - A new setting for multisample volume allowing you to boost the volume of the samples.
 - You can now modulate the amounts of the first 8 modulation slots in the mod matrix. I.e. mod amount 1-8 are new modulation destinations.
 - Added new option for MIDI clock mode called "in-tempo-sync" to synchronize with tempo only, not syncing to the downbeat of the midi clock.
 - Added new MIDI CCs for desktop module that allow you to control the settings for each oscillator independently. See MIDI spec document from our support page for details.
 - Added MIDI SysEx option to request program without sequencer data.
 - Further fixes for random clicking that would occur when switching wavetables or programs, when voices play with new settings for the first time.
 - Fixes to address clipping and distortion in effects processing.
 - Fix for ADSR envelope repeat, to prevent discontinuity clicking at the end of decay stage if sustain is not set to 0.
 - Fix for conflict with Samsung Magician software on Windows that would cause the synth to crash if Samsung Magician is running when USB is connected to synth.
 - Fix for MIDI sync error introduced in version 1.8 in a botched attempt to improve stability of MIDI clock. Now it is working as intended. It was most noticeable when arpeggiator was used with external MIDI clock.
 - Fix for desktop module tempo encoder to not jump to previous value after tap tempo input.
 - Fix to set version number in MIDI SysEx Device Inquiry.

new in version 1.8d release (version 1.8b and 1.8c were never officially released and were only used for internal testing):
 - Swapped the labels for sample loop crossfade modes "equal power" and "equal volume". We originally had this backwards and corrected it so that the linear crossfading option is now called equal volume and the sinusoidal crossfading option is now called equal power. This will not change any of the settings of your samples, it just corrects the name of the mode that is displayed.
 - Fix for random clicking distortion noises that were recently reported to us, most noticeable when playing a sine wave.
 - Improvements to envelope smoothing to prevent audible zipper noise when params are changed or modulated.
 - Midi cc bug fix: fix for issue with cc numbers mapped to encoders where parameters were not updating depending on current state of the encoder.
 - Fix so that the wavetable waveform viewer is not shown when a sample slot is selected. It would erroneously come up when you change the wave offset under certain conditions.

new in version 1.8a release:
 - Sample loop on/off button replaced with loop select, which selects between 3 options: off, on when note on, always on.
 - Added a new confirmation prompt to ask if you are sure when clearing all the sample memory.
 - Reduced volume of sample playback to be more inline with playing sample with one voice of the synth engine.
 - Replaced label in button from "add multi" to "add to multi".
 - Bug fix for viewing arp settings with COMPARE button + ARP button. Previously this would stop arp notes from playing.
 - Bug fix for transmitting midi params in multitimbral mode when editing multiple parts at one time. Previously midi could be sent to incorrect channels depending on how channels were configured.
 - Bug fix for transmitting midi nrpn in multitimbral mode when editing multiple parts at one time. Now the midi nrpn parameter and value bytes are transmitted together on each channel before moving to the next channel.

new in version 1.8 release:
 - New sampling capabilities: 3rd Wave now supports sample recording, import, and playback. Find out more in our manual or instructional video
 - Added audio gain control for setting input level for recording directly into the synth, both for samples and also for the wave maker to create wavetables
 - New global param "MIDI ignore CC param display update" to turn off display updates on midi cc changes
 - New global param "Encoder acceleration" you can use to turn off the encoder acceleration if you spin the encoder knobs quickly
 - New global param "Return home if inactive" to return to the main home screen after inactivity
 - Added MIDI SysEx request to query counts of wavetables loaded on the machine
 - Bug fix for using sustain pedal of opposite polarity at the same time you use sustain pedal via midi CC
 - Bug fix for stuck note issue when using a keyboard split where one side of the keyboard has unison legato enabled
 - Bug fix for setting resonance compensation independently per part when running in multitimbral mode
 - Bug fix to reset lpf envelope in multitimbral mode so you do not here filter adjust when voice switches to a different part
 - Bug fix for bulk import on MacOS where it would import the same file multiple times due to MacOs writing data to the drive while the import was in progress
 - Bug fix for hold/sustain turning off voices when turned off even when key is pressed, would happen when transpose was set to non zero
 - Bug fix for mod destination shortcut to set svf env amount, was incorrectly mapped to lpf env amount
 - Bug fix for unison chord mode to only add notes to the chord if the notes are part of the corresponding patch with unison enabled when you have a keyboard split enabled
 - Bug fix to turn off sequencer when you hit compare button
 - Bug fix to map envelope repeat on/off parameter to midi nrpn, was not getting saved if you were using midi sysex to dump the patch
 
changes since version 1.0:
 - fix for midi program change via midi din
 - fix for mod source and destination button hold
 - fix for elusive stuck notes
 - fix for tempo drifts in sequencer and arp
 - fixes for midi clock sync + song position pointer
 - improvements to volume potentiometer to have smooth fade out
 - improvements to analog waveforms on low notes
 - part clear in sequencer
 - envelope repeat
 - improvements to velocity precision for 3rd Wave keyboard - velocity curve still needs work
 - improvements to sawtooth analog model
 - improvements to potentiometer precision
 - synthplex update: slightly wider dead zone for detent pots + fix for usb drive not mounting on latest Mac OS on certain hubs
 - unison + arp settings now editable per part
 - global setting MIDI multitimbral mode to control parts on separate MIDI channels
 - reverse mode for osc key to waves setting, to replicate ppg behavior
 - improvements to Circuit Drift: envs, filters, fine tuning follow a set of repeatable changes + other suggestions
 - fixes for multitimbral playback in sequencer
 - fix to spatial panning wraparound to always get movement
 - fix for arp start with midi sync
 - fix for setting mod destinations per part
 - fix for note hang when disconnecting sustain pedal in certain configs
 - fix for midi active sensing message, Yamaha Montage issue
 - fix for issue in analog waveforms recently introduced, especially in A04, supersaw waveform
 - fix for envelope sustain modulation
 - fixes for curcuit drift, analog filter cutoff and resonance per part
 - fix for sawtooth pulse width
 - new velocity and pressure curve/settings
 - fix for amp env + velocity settings
 - fixes for wavetable maker crashing bug after making multiple tables
 - added tenths place decimal for tempo
 - unison chord mode, will not erroneously activate for 1 note + ui update to show part for unison settings
 - Noise input setting honored for wave maker
 - LPF velocity ui now says velocity to cutoff or velocity to env depending on the velo to env setting in LPF misc
 - More unison key assign options for no retriggering + added legato setting
 - Display error messages if failure to read the wav file for wavemaker
 - New ARP latch option for HOLD. With HOLD on and this setting set to "chord", it will replace the notes of the previous chord instead of adding to arpeggio when you play chords
 - Another bug fix for elusive stuck note issue that you may have encountered
 - Bug fix for midi clock sync that was causing issues with effects clock sync setting, was erroneously setting to very low bpm for an instant at the beginning of playback
 - Added display brightness setting in Global menu
 - Added "pass thru" pot mode setting in the Global menu. With pot mode set to pass thru, you have to move the pot past the current saved value before it triggers an update to the setting.
 - fix for wave env release point issues
 - bug fix for glide in unison legato mode
 - no longer restarting arp timing on a new chord when latch mode is chord and hold is on
 - lfo rate encoder now controls note value when sync is on instead of extra param in misc menu
 - bug fixes for switching between usb midi on/off in global controls (midi in cable and midi out cable settings)
 - no longer allowing all 3 oscillators to be set to supersaw due to cpu limits
 - toned down filter cutoff variation for circuit drift
 - improvements to wavemaker algorithm and ui for pitch on/off and wave sensitivity
 - new multipart button behavior (double-press to edit)
 - wave surfer control goes negative + ui update to indicate upper wavetables
 - unison chord mode is now per part + displays chord in ui under number of voices
 - added arp transpose control
 - fix so release does not play out on new program after switching programs
 - fix for trippy wave offset animation (blue box) in waveform viewer screen caused by screensaver
 - pressing keyboard key now deactivates screensaver
 - fix for unison screen to work with show mode (hold COMPARE button)
 - fix for sequencer count-in to enable when controlling sequencer with midi sync and DAW
 - fix for negative LFO amounts
 - fix for pan mod + effect param mods per part
 - fix for midi clock sync arp timing when clock is constantly provided without start, stop commands from external controller
 - fix for usb midi off setting
 - fix for unison legato mode to smooth out key velocity changes to prevent clicky sound
 - update wavemaker ui to say pitch instead of noise in encoder description
 - Serum wavetable compatibilty with wave maker
 - Fix for USB connectivity timing issue that affected majority of ports on Mac Studio and some usb extenders
 - Fix for echoplex audio corruption, crash issue observed by scrolling through programs in bank 2
 - Fixes for midi NRPN transmission
 - Fix for clearing polyaftertouch values when switching between polyaftertouch and non-polyaftertouch controller
 - Fix for 3rd Wave keyboard issue causing super short double-trigger notes when keys are played quickly and are not let up fully
 - New legato slide mode in unison, where notes glide only on overlapping notes
 - Update to filename for exporting programs to USB drive, now using bank and program number instead of file counter.
 - editable favorite lists for improved preset navigation. total of 10 lists, each with max 50 presets. Hit the favs button from the main program screen and add the current program to one of the lists
 - hold lfo or env buttons to set destination, similar to mod matrix UI
 - audio input now routed through both filters + amp envelope, see audio in mix param in misc settings
 - global param "Midi send arp notes" to enable midi transmission of arpeggios
 - turning off HOLD will no longer turn off notes being held down, for smoother arp playing when sustain pedal is set to pressed hold on/off mode
 - fix for random midi transmission dropout via midi din
 - adjustments for noisy key switches observed by customers, would cause high velocity note ons when key held down between off and on, or released slowly
 - fix for pop/click/noise phase shift observed at beginning of voice on, most noticeable on sine oscillator with unison on
 - fix for key to waves with reverse set to ON, "Use upper wavetable" must be on for replication of PPG patches
 - master volume now affects volume of wavemaker audio playback
 - many fixes for midi multimbral mode CC, with midi local control off
 - adjustment to reverb output to address distortion
 - fix for midi sustain pedal when controlling with pedal with reversed polarity
 - displaying the osc you are viewing in wave envelope UI
 - support for MIDI MPE controllers - enable MPE from the GLOBAL menu and explore the new modulation sources at the end of the list. Pitch bend range can be set in the MISC menu
 - option for free running analog oscillators in the MISC menu which is settable per patch - In the analog waveform mode, which you are using when you select the Axx waveforms like Saw and Square, now has the option to make the waveforms not reset when you start a new note. In this mode, the oscillators will continue to drift from each other as they do on some fully analog synthesizers. There are two side effects if you are using free running for the analog waveforms:
     1. When two or more oscillators are running at the same time, the phase of the waveforms will not be reset and could start at any position. As a result, there will be phase cancellation compared to having the oscillators always start at the same point. What you will hear is that the notes will change volume level slightly as the oscillators start and also drift in and out of phase with each other.
     2. In the normal mode the oscillator always starts at zero. Now it could start at any point in its phase position. That means when you hit a note, a single oscillator could be at 0, +1.0, -1.0, or anywhere in between. If it starts at or close to +1.0 ot -1.0, you are going from no sound to fully on immediately. This can cause a click at the beginning of the note depending on the phase. It is noticeable mostly when using a sine wave, and not too noticeable with something like a saw or square. If you want to use this free running mode, turn the attack time up to +20 or higher to quickly fade in and avoid the potential click.
 - new poly unison mode - set the polyphony count in the second page of the UNISON menu. It will split the voices up automatically to use max voices per note
 - new shortcut buttons to easily set output routing per part
 - new option in GLOBAL menu to send midi program change messages
 - now saving UNISON chord mode settings with program
 - now pitch wheel, mod wheel, pressure are independent per part when controlling in midi multitimbral mode + pitch wheel destination is settable per part
 - slight adjustments to circuit drift envelope sustain variance - gets rid of jumps when going from decay to sustain in the envelope
 - new options for longer LFO sync times
 - improvements to LED brightness settings
 - added smoothing to pan position changes to avoid audible stepping
 - bug fix for triangle wave phase discontinuities - Gets rid of clicks if you are pitch bending
 - bug fix for LFO frequency wraparound when used as mod destination
 - bug fix for COMPARE button, fix for machine freeze up if pressed on initial program that loads at bootup before changing a program + remembers which part you are editing
 - bug fix for multimbral and keyboard split playing, to reset filter settings so no audible change when voice steals between parts
 - bug fix for timing and synchronization issues when receiving MIDI SysEx data while synth is playing
 - bug fix so metronome does not continue to play if stop sequencer before count in
 - bug fix for midi out clock drift, when 3rd Wave is master clock, caused by rounding error
 - bug fix for unison/voice steal clicking from filter envelope reset on new note
 - bug fix for sustain pedal with MIDI local control off
 - bug fix for arp timing with midi sync, allowing more buffer time for midi note to trigger at same time as midi clock pulse
 - added master tuning global params
 - added sequencer play mode for transposing sequence with the keyboard. Hit the right arrow on the sequencer display and set play mode to transpose. Hit a key when sequence is playing to transpose the notes, middle C is the reference with no transposition
 - ui changes for global, misc, and make waves buttons, leds stay lit and press button again to deselect and return to previous screen
 - changes to init program
 - bug fixes for free running oscillators that fixed zipper noise when pitch is shifted
 - bug fix for sustain pedal voice stealing, now will steal voices that are sustained but not held down before stealing voices with keys held down
 - bug fix for poly unison mode when sustain pedal is active, when hit same note that is already sustained
 - ui bug fix to load correct fx param encoder vals to prevent jumping when encoder changes
 - bug fix for setting midi local control off and midi send arp notes on
 - initial version for first batch of desktop modules
 - You can now load PPG style wavetables with the wavemaker by loading in wav files with 8192 samples as input (see link on support page for instructions) - Prophet VS wavetable files included with release
 - Improvements to virtual analog engine for sawtooth and square waveforms. This compensates for the PPG hardware chain and makes the shape more well defined. It also yields improved high frequency response
 - Added new way to toggle multi-part editing. You can now toggle which part or parts are being edited by holding the multipart MODE button down while pressing any active, (lit), multi-part buttons. You can still double-press the buttons to select the part or parts being edited like in earlier versions. So, you now have two methods to select which part(s) are being edited
 - New MISC setting per part Envelope retrigger mode to choose between env restarting from 0 or starting from the last value it reached when voice is retriggered. Use the latter for notes with super short gates. This gives you the method of re-trigger in many, (but not all), older analog synthesizers
 - The HOLD setting is now per part. You can now hold an arpeggio on one part while you play a separate part over it
 - Added text to wave envelope graph display to show the position and time values you are editing
 - New GLOBAL setting Accessibility light sensitivity for users sensitive to blinking lights
 - New accessibility MIDI SysEx messages to query screen data for users with visual impairment
 - Improvement so multiple parts can use the same MIDI channel when MIDI multitimbral mode is on
 - Improvement to ARP chord hold mode so you can keep adding notes in the chord as long as you keep the keys pressed
 - New GLOBAL setting to have the metronome only play in headphone output instead of in the main outputs
 - Per part settings for volume, pan, and tuning from the multi-part settings are now recordable with the sequencer
 - Improvements to bootup sequence to prevent boot issues where units occasionally fail to boot and remain on the screen startup with logo requiring a reboot
 - Fix to handle erroneous MIDI status bytes that we observed from the Expressive E Osmose when sending large amounts of MPE data via MIDI din. These message would cause random midi havoc like random control changes, stuck notes, and even program changes
 - Improvement to midi sync processing when looping is enabled in DAW to handle note offs efficiently when a loop restarts.
 - Slight tweak to MIDI cc numbers to prevent conflicts with pro tools + fix to prevent issues when receiving midi messages that are not supported by 3rd Wave
 - Optimizations to improve processing time for our most processor heavy presets with super saw, like B1-P025 2PWAVE SUPER + and B1-P039 Osaka Massive
 - Various bug fixes for the desktop module to make sure encoder ranges and values are updated appropriately when data is reloaded and to prevent jumps when control changes (lfo sync note value, effect params, oscillator wave offset, sequencer quantization)
 - Bug fix for the desktop module volume when pot mode is set to pass thru
 - Bug fix for bulk import operations where the same file would be imported multiple times due to MacOS writing hidden files to the USB drive during the import process. ***This bug was not totally fixed in version 1.7, but it has been addressed and will be part of the next update version 1.8. In the meantime it will work reliably if you eject the USB drive after copying the files, before you start the bulk import operation on the synth.***
 - Bug fix to make sure the correct part is displayed when a new keyboard split is added
 
TO LOAD A NEW OS:
1. Download the new OS from the Support page of the Groove Synthesis website. The file type is "ldr" for the OS.
2. Connect the 3rd Wave to your computer using the USB connector on the back of the synth.
3. Once connected, the 3rd Wave will show up on your computer desktop as an external drive.
4. Copy the "ldr" file into the firmware folder on the 3rd Wave.
5. Once the file has finished copying, press the global button on the 3rd Wave, then use Soft Knob 1 to locate the "Firmware Update" command.
6. Use Soft Knob 2 to select go.
7. Press Soft Button 1 (refresh). The screen displays the name of the OS file that you copied to the firmware folder.
8. Eject the 3rd Wave drive from your computer desktop.
9. Disconnect the USB cable from the back of the 3rd Wave.
10. Press Soft Button 4 (ok) or Soft Button 6 on the 8M model. The display will alert you when the OS has finished updating.
11. Once the display indicates that it is finished, turn off the synthesizer briefly then turn it back on again. The updated OS version appears in the upper right corner of the display.
