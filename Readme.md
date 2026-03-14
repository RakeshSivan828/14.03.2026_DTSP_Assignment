# A music streaming platform wants to reduce storage requirements by lowering the sampling rate of high-quality audio before transmission.

## AIM: 

### Task 1:

1. Generate a composite audio signal consisting of three sine waves (500 Hz, 1500 Hz, 3000 Hz).

2. Sample the signal at 16 kHz.

3. Downsample the signal by a factor of 4.

4. Plot

       Original signal

       Downsampled signal

Compare the frequency spectrum of both signals.

### Task 2:

1. Generate an ECG-like signal.

2. Design a low-pass FIR filter.

3. Apply the filter before decimation by factor 

4. Plot:

        Original signal

        Filtered signal

        Decimated signal

## APPARATUS REQUIRED: 

PC installed with SCILAB. 

## PROGRAM: 
### Task 1:
~~~
clc;
clear;
close;


fs = 16000;           // Sampling frequency (16 kHz)
t = 0:1/fs:0.02;      // Time vector (20 ms)

f1 = 500;
f2 = 1500;
f3 = 3000;

x1 = sin(2*%pi*f1*t);
x2 = sin(2*%pi*f2*t);
x3 = sin(2*%pi*f3*t);

x = x1 + x2 + x3;

// Downsample factor
M = 4;

// Downsampled signal
x_down = x(1:M:$);

// Time vector for downsampled signal
t_down = t(1:M:$);

figure(1);
subplot(2,1,1);
plot(t, x);
title("Original Composite Signal");
xlabel("Time (seconds)");
ylabel("Amplitude");

subplot(2,1,2);
plot(t_down, x_down);
title("Downsampled Signal (Factor = 4)");
xlabel("Time (seconds)");
ylabel("Amplitude");

N = length(x);
X = fft(x);
f = (0:N-1)*(fs/N);

N2 = length(x_down);
fs_new = fs/M;
X_down = fft(x_down);
f2 = (0:N2-1)*(fs_new/N2);

figure(2);

subplot(2,1,1);
plot(f, abs(X));
title("Frequency Spectrum of Original Signal");
xlabel("Frequency (Hz)");
ylabel("Magnitude");

subplot(2,1,2);
plot(f2, abs(X_down));
title("Frequency Spectrum of Downsampled Signal");
xlabel("Frequency (Hz)");
ylabel("Magnitude");

~~~

### Task 2:
```
clc;
clear;
close;

// Sampling parameters
fs = 500;              // Sampling frequency (Hz)
t = 0:1/fs:2;          // Time vector (2 seconds)

// Generate ECG-like signal
ecg = 1.2*sin(2*%pi*1.7*t) + 0.25*sin(2*%pi*20*t) + 0.1*rand(1,length(t));

// FIR Filter Design
N = 41;                 // Filter order
fc = 10;                // Cutoff frequency (Hz)
Wc = fc/(fs/2);         // Normalized cutoff

h = wfir("lp", N, Wc, "hm");   // Low pass FIR using Hamming window

// Apply FIR Filter
filtered = conv(ecg, h);

// Adjust length after convolution
filtered = filtered(1:length(ecg));

// Decimation by factor 3
decimation_factor = 3;
decimated = filtered(1:decimation_factor:$);

// Time vectors
t_dec = t(1:decimation_factor:$);

// Plot signals
subplot(3,1,1)
plot(t, ecg)
title("Original ECG-like Signal")
xlabel("Time (s)")
ylabel("Amplitude")

subplot(3,1,2)
plot(t, filtered)
title("Filtered Signal (Low-pass FIR)")
xlabel("Time (s)")
ylabel("Amplitude")

subplot(3,1,3)
plot(t_dec, decimated)
title("Decimated Signal (Factor = 3)")
xlabel("Time (s)")
ylabel("Amplitude")
```
# OUTPUT: 
### Task 1:


### Task 2:


# RESULT: 
Thus we have obtained the output.
