% FIR Low-Pass Filter Design using Rectangular Window
clc;
clear;

% Specifications
fs = 1000;       % Sampling frequency in Hz
fc = 150;        % Cutoff frequency in Hz
N = 51;          % Filter length (odd number for symmetric FIR filter)

% Normalize cutoff frequency
wc = 2 * pi * (fc / fs);  % Digital cutoff frequency (rad/sample)
f_cutoff = fc / (fs / 2); % Normalized cutoff frequency (0 to 1)

% Ideal impulse response (sinc function for LPF)
n = -(N-1)/2:(N-1)/2;     % Symmetric indices
h_ideal = wc/pi * sinc(wc/pi * n);  % Ideal LPF impulse response

% Apply Rectangular Window (No modification to coefficients)
h_rectangular = h_ideal;

% Plot Impulse Response
figure;
stem(n, h_rectangular, 'filled');
title('Impulse Response of FIR LPF (Rectangular Window)');
xlabel('n');
ylabel('h[n]');
grid on;

% Frequency Response
[H, f] = freqz(h_rectangular, 1, 1024, fs);  % Frequency response
figure;
plot(f, abs(H), 'b', 'LineWidth', 1.5);
title('Frequency Response of FIR LPF (Rectangular Window)');
xlabel('Frequency (Hz)');
ylabel('Magnitude');
grid on;

% Normalize and compare cutoff
hold on;
yline(0.707, 'r--', 'LineWidth', 1);  % -3 dB line for cutoff
xline(fc, 'g--', 'LineWidth', 1);    % Ideal cutoff frequency
legend('Magnitude Response', '-3 dB Line', 'Cutoff Frequency');
