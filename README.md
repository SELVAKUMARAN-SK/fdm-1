# fdm
# Frequency-Division-Multiplexing---Modulation-and-Demodulation-using-Python:

## Aim:

To generate an FDM signal by multiplexing multiple baseband message signals on different carrier frequencies, transmit (sum) them, optionally add 
channel noise, then recover each message by bandpass filtering and coherent demodulation in Python (Google Colab). Observe time & frequency domain
signals and measure recovery quality.

## Apparatus Required:

Google Colab (or any Python environment)

Python libraries: numpy, matplotlib, scipy (scipy.signal)

## Theory:

FDM places different message signals in separate, non-overlapping frequency bands by modulating each message onto a
distinct carrier frequency. The multiplexed signal is the sum of all modulated channels. At the receiver, bandpass filters (or tuned filters) isolate each channel;
then each isolated carrier is demodulated (coherently multiplied by a synchronized carrier) and low-pass filtered to recover the original baseband.
## Procedure:

1 — Imports and parameters

2 — Create message signals and carriers

3 — Modulate each message (standard AM DSB-SC) and form FDM signal

4 — Frequency domain (spectrum) of FDM signal

5 — (Optional) Add AWGN noise to FDM signal

6 — Receiver: isolate each channel with bandpass filter

7 — Demodulate each isolated channel (coherent) and low-pass filter to recover baseband

## CODE:
```
fs = 10000; 
t=0:1/fs:0.01-1/fs; 
// Frequencies 
f = [300 400 500 600 700]; 
 
// Generate 5 signals 
m1 = sin(2 * %pi * f(1) * t); 
m2 = sin(2 * %pi * f(2) * t); 
m3 = sin(2 * %pi * f(3) * t); 
m4 = sin(2 * %pi * f(4) * t); 
m5 = sin(2 * %pi * f(5) * t); 
 
// Plot message signals 
scf(0); 
subplot(5,1,1); plot(t, m1); title("Message Signal 1"); 
subplot(5,1,2); plot(t, m2); title("Message Signal 2"); 
subplot(5,1,3); plot(t, m3); title("Message Signal 3"); 
subplot(5,1,4); plot(t, m4); title("Message Signal 4"); 
subplot(5,1,5); plot(t, m5); title("Message Signal 5"); 
 
// TDM modulation 
tdm = zeros(1, 5 * length(t)); 
for i = 1:length(t) 
    tdm(5*(i-1)+1) = m1(i); 
    tdm(5*(i-1)+2) = m2(i); 
    tdm(5*(i-1)+3) = m3(i); 
    tdm(5*(i-1)+4) = m4(i); 
    tdm(5*(i-1)+5) = m5(i); 
end 
 
// Time vector for TDM 
tdm_t = 0:1/fs:(length(tdm)-1)/fs; 
 
// Plot TDM 
scf(1); 
plot(tdm_t, tdm, 'm'); 
title("TDM Modulated Signal"); 
xlabel("Time"); 
ylabel("Amplitude"); 
xgrid(); 
 
// Demodulate 
m1_d = tdm(1:5:$); 
m2_d = tdm(2:5:$); 
m3_d = tdm(3:5:$); 
m4_d = tdm(4:5:$); 
m5_d = tdm(5:5:$); 
 
// Plot demodulated 
scf(2); 
subplot(5,1,1); plot(t, m1_d); title("Demodulated Signal 1"); 
subplot(5,1,2); plot(t, m2_d); title("Demodulated Signal 2"); 
subplot(5,1,3); plot(t, m3_d); title("Demodulated Signal 3"); 
subplot(5,1,4); plot(t, m4_d); title("Demodulated Signal 4"); 
subplot(5,1,5); plot(t, m5_d); title("DemodulatedSignal 5");
```
## Output:
<img width="783" height="442" alt="image" src="https://github.com/user-attachments/assets/25b8331d-70d3-4f90-a649-618b037c8261" />

<img width="796" height="547" alt="image" src="https://github.com/user-attachments/assets/1001729e-13fb-41de-9ebe-c5164f0123d9" />
<img width="784" height="428" alt="image" src="https://github.com/user-attachments/assets/a1ed1d5c-1996-478f-8f80-7c78e373b043" />

![WhatsApp Image 2025-12-04 at 12 22 16 PM](https://github.com/user-attachments/assets/8a618df2-7f46-41a9-b0bc-b6a6fc340d3b)

![WhatsApp Image 2025-12-04 at 12 22 29 PM](https://github.com/user-attachments/assets/33236909-206f-4a60-8027-e0dfa9a8ce02)



## Result:

FDM experiment was successfully simulated and verified using Python. The message signals were multiplexed and perfectly recovered.
