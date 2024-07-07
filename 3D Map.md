import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D


file_path = '/Users/melisaaykul/Desktop/3D_data.csv'
data = pd.read_csv(file_path, delimiter=';')


time = data.iloc[1:, 0].astype(float).values
wavenumbers = data.columns[1:].astype(float)


log_time = np.log10(time)

absorbance_values = data.iloc[1:, 1:].replace(',', '.', regex=True).astype(float).values


T, W = np.meshgrid(log_time, wavenumbers)


fig = plt.figure(figsize=(12, 8))
ax = fig.add_subplot(111, projection='3d')
surf = ax.plot_surface(T, W, absorbance_values.T, cmap='plasma', edgecolor='none')


ax.set_xlabel('Log(Time) (s)')
ax.set_ylabel('Wavenumber (cm$^{-1}$)')
ax.set_zlabel('Absorbance (A.U)')
ax.set_title('3D Absorbance Surface Plot')
ax.set_zlim(-0.0015, 0.0015)
fig.colorbar(surf, ax=ax, shrink=0.5, aspect=5, label='Absorbance')
plt.show()
