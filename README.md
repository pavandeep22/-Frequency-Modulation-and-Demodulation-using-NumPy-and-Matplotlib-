# -Frequency-Modulation-and-Demodulation-using-NumPy-and-Matplotlib-

# Aim:
To implement and analyze frequency modulation (FM) using Python's NumPy and Matplotlib libraries.

# Apparatus Required:

1. Software: Python with NumPy and Matplotlib libraries
   
2. Hardware: Personal Computer

 
# Theory:

Frequency Modulation (FM) is a method of transmitting information over a carrier wave by varying its 
frequency in accordance with the amplitude of the input signal (message signal). The frequency of the carrier 
wave is varied according to the instantaneous amplitude of the message signal.

# Algorithm:

1. Initialize Parameters: Set the values for carrier frequency, message frequency, sampling frequency, and 
   frequency deviation.
   
2. Generate Time Axis: Create a time vector for the signal duration.
    
3. Generate Message Signal: Define the message signal as a cosine wave.
    
4. Compute the Integral of the Message Signal: Calculate the integral of the message signal over time.
    
5. Generate FM Signal: Apply the FM modulation formula to obtain the modulated signal.
 
6. Plot the Signals: Use Matplotlib to plot the message signal, carrier signal, and modulated signal.

# Programme:
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import hilbert

# Parameters
Fs = 5000  # Sampling frequency
Fc = 200   # Carrier frequency
f_mod = 20  # Modulating signal frequency
Am = 1.0    # Amplitude of the modulating signal
kf = 50     # Frequency deviation constant
t = np.arange(0, 1, 1/Fs)  # Time vector

# Modulating signal (message signal)
modulating_signal = Am * np.cos(2 * np.pi * f_mod * t)

# FM Modulation
integral_of_message = np.cumsum(modulating_signal) / Fs
carrier = np.cos(2 * np.pi * Fc * t + 2 * np.pi * kf * integral_of_message)

# Plot modulating signal and modulated FM signal
plt.figure(figsize=(10, 8))

plt.subplot(3, 1, 1)
plt.plot(t, modulating_signal)
plt.title('Modulating Signal (Message)')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')

plt.subplot(3, 1, 2)
plt.plot(t, carrier)
plt.title('FM Modulated Signal')
plt.xlabel('Time (s)')
plt.ylabel('Amplitude')

# FM Demodulation using Hilbert Transform to extract the instantaneous frequency
analytic_signal = hilbert(carrier)
instantaneous_phase = np.unwrap(np.angle(analytic_signal))
instantaneous_frequency = np.diff(instantaneous_phase) * Fs / (2 * np.pi)

# Since diff reduces the array length by 1, we'll adjust the time array for plotting
t_demod = t[1:]

plt.subplot(3, 1, 3)
plt.plot(t_demod, instantaneous_frequency - Fc)  # Subtract carrier frequency
plt.title('Demodulated Signal (Recovered Message)')
plt.xlabel('Time (s)')
plt.ylabel('Frequency (Hz)')

plt.tight_layout()
plt.show()
```
# Output:
<img width="989" height="790" alt="ac 8" src="https://github.com/user-attachments/assets/65af0f6f-b385-46fd-b12b-f8cf4a1e6603" />

![WhatsApp Image 2025-11-26 at 21 46 57_30dd2fb3](https://github.com/user-attachments/assets/6d391074-024e-4b50-ac6e-5b74bf006a33)


# Result:
Thus the Frequency Modulation and Demodulation using NumPy and Matplotlib is verified successfully.
