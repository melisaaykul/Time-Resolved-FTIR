# Time-Resolved-FTIR
Analysis of Time Resolved FTIR with respect to different selected time values and difference spectra of these values.
import pandas as pd
import matplotlib.pyplot as plt

file_path_10micro = '/Users/melisaaykul/Desktop/10micro.csv'
file_path_300micro = '/Users/melisaaykul/Desktop/300micro.csv'
file_path_5ms = '/Users/melisaaykul/Desktop/5ms.csv'

data_10micro = pd.read_csv(file_path_10micro)
data_300micro = pd.read_csv(file_path_300micro)
data_5ms = pd.read_csv(file_path_5ms)

wavenumber_10micro = data_10micro.iloc[:, 0]
absorbance_10micro = data_10micro.iloc[:, 1]

wavenumber_300micro = data_300micro.iloc[:, 0]
absorbance_300micro = data_300micro.iloc[:, 1]

wavenumber_5ms = data_5ms.iloc[:, 0]
absorbance_5ms = data_5ms.iloc[:, 1]


plt.figure(figsize=(10, 6))
plt.plot(wavenumber_10micro, absorbance_10micro, label='10 µs')
plt.plot(wavenumber_300micro, absorbance_300micro, label='300 µs')
plt.plot(wavenumber_5ms, absorbance_5ms, label='5 ms')
plt.xlabel('Wavenumber (cm^-1)')
plt.ylabel('Absorbance (A.U)')
plt.legend()
plt.grid(True)
plt.xlim(800, 1800)  # Set the x-axis limits
plt.gca().invert_xaxis()  # Invert x-axis to go from 1800 to 800
plt.show()
