To understand how the stroboscopic tuner works under the hood, we can break it down into two major pillars: the audio signal processing and pitch detection, and the optical physics of stroboscopy translated into mathematical phase accumulation.
Part 1: The Audio Pipeline & Conditioning
Before any math happens, raw sound from your phone's microphone must be captured, amplified, and filtered.
 * Stream Capture (navigator.mediaDevices.getUserMedia):
   The app requests an audio stream with echo cancellation and noise suppression turned off (ideal: false) so raw, unprocessed acoustic waveforms from your instrument hit the processor.
 * Web Audio Graph Routing:
   
   * GainNode: Acts as a software preamp. Multiplying the input PCM float values by a factor of 0.5\times to 10.0\times boosts weak guitar signals.
   * AnalyserNode: Configured with an fftSize of 2048. Instead of frequency-domain data (FFT), the app pulls time-domain waveform data (getFloatTimeDomainData) into a typed Float32 array. Time-domain analysis is essential for precise time-lag pitch detection algorithms.
 * The Noise Gate:
   Before running heavy math, the app calculates the RMS (Root Mean Square) energy of the buffer:
   
   
   It converts this to decibels: \text{dB} = 20 \log_{10}(\text{RMS}). If the signal falls below your chosen threshold (e.g., -40\text{ dB}), the tuner pauses pitch tracking to prevent background room noise from causing erratic jumps.
Part 2: High-Precision Pitch Detection (NSDF)
Standard zero-crossing counters fail on string instruments because string harmonics (overtones) create multiple zero-crossings per cycle. Instead, this app uses a variant of Autocorrelation called the Normalized Square Difference Function (NSDF), derived from the McLeod Pitch Method.
 * Autocorrelation Concept:
   The algorithm slides a copy of the audio buffer against itself across various time lags (\tau). When the lag matches the exact period of the fundamental note, the waveforms align, and the correlation score spikes.
 * The NSDF Formula:
   Instead of raw multiplication, NSDF normalizes the energy so high-amplitude sections don't skew the results:
   
 * Peak Picking & Parabolic Interpolation:
   The code searches for the highest positive peak in the NSDF curve. Because digital audio is sampled at discrete intervals (e.g., 44.1\text{ kHz}), the true peak often falls between two samples. The app applies parabolic interpolation around the peak to calculate sub-sample accuracy, giving you precise frequency decimal places (e.g., 82.41\text{ Hz} instead of a rounded integer).
Part 3: The Physics of Stroboscopy & Phase Accumulation
This is the heart of why a strobe tuner behaves differently than a digital needle.
How a Mechanical Strobe Works
Imagine a spinning translucent disk divided into alternating dark and light segments, illuminated by a neon lamp flashing at a specific target frequency (f_{\text{target}}).
 * If your guitar string vibrates at exactly f_{\text{target}}, the lamp flashes at the exact moment the disk rotates into position. The pattern appears frozen.
 * If your string is sharp (f_{\text{input}} > f_{\text{target}}), the disk rotates slightly too far between flashes. The pattern appears to drift clockwise.
 * If your string is flat (f_{\text{input}} < f_{\text{target}}), the disk hasn't reached the position yet. The pattern drifts counter-clockwise.
Simulating This in JavaScript (Phase Math)
Instead of rendering a physical disk, the code calculates the phase angle (\phi) frame-by-frame inside the Canvas render loop (requestAnimationFrame):
 * Frequency Difference (\Delta f):
   
 * Phase Velocity (\omega):
   The angular speed at which the strobe pattern rotates is proportional to \Delta f:
   
 * Continuous Phase Accumulation:
   In every animation frame (dt seconds elapsed), the cumulative phase is updated:
   
 * Drawing the Stripes:
   The canvas draws repeating sinusoidal or square wave grating patterns offset by \phi(t). Because \omega approaches zero as you get in tune (\Delta f \to 0), the speed of the stripes slows down smoothly and locks dead-still without any artificial "freezing" deadbands.
Part 4: Instrument Presets & Nearest-Note Snapping
When you select an instrument preset (like Guitar E Standard or Bass 4-String), the tuner changes how it interprets notes:
 * The Frequency Map: Each preset provides an array of target frequencies (e.g., E2 = 82.41\text{ Hz}, A2 = 110.00\text{ Hz}, etc.).
 * Snapping Logic: When a frequency is detected, the app scans the preset's target array and calculates logarithmic distance (in cents) to each target.
 * Avoiding Wrong Octaves: By locking onto the closest valid string in that specific instrument profile, it prevents the tuner from jumping to a wild overtone or an unintended octave, ensuring your tuning pegs adjust the correct string.
Part 5: Cent Calculation
To display how out-of-tune you are on the numerical pill and the needle meter, the app calculates cents (logarithmic musical intervals where 100 cents = 1 semitone):


If \text{cents} = +5, you are 5 cents sharp; if \text{cents} = -12, you are 12 cents flat. This value directly drives the position of the visual needle from -50\text{¢} to +50\text{¢}.
