import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.colors import Normalize


file_path = '/Users/melisaaykul/Desktop/step_scan1.csv'
data = pd.read_csv(file_path, delimiter=';')


wavenumbers = data.columns[1:].astype(float)
time = data.iloc[:, 0].astype(float)
absorbance_values = data.iloc[:, 1:].replace(',', '.', regex=True).astype(float).values
norm = Normalize(vmin=-0.0012, vmax=0.0018)


fig, ax = plt.subplots(figsize=(18, 5))
cax = ax.imshow(absorbance_values, aspect='auto', cmap='plasma', norm=norm, origin='lower')
ax.set_xlabel(r'Wavenumber $\nu$ (cm$^{-1}$)', fontsize=20)
ax.set_ylabel('Number of Measurement over Time', fontsize=15)
ax.set_title('Absorbance Heatmap', fontsize=18)
y_ticks = np.linspace(0, len(time)-1, 3)
y_labels = [0, 35, 70]
ax.set_yticks(y_ticks)
ax.set_yticklabels(y_labels, fontsize=10)
x_ticks = np.linspace(0, len(wavenumbers)-1, len(np.arange(1800, 700, -100)))
x_labels = np.arange(1800, 700, -100)
ax.set_xticks(x_ticks)
ax.set_xticklabels(x_labels, rotation=45, fontsize=10)
cbar = fig.colorbar(cax, ax=ax, orientation='vertical', ticks=np.arange(-0.0012, 0.0019, 0.0003))
cbar.set_label('Absorbance')
plt.show()
