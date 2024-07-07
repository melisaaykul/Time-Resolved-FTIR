import pandas as pd
import matplotlib.pyplot as plt
from scipy.optimize import curve_fit
import numpy as np


file_path = '/Users/melisaaykul/Desktop/1504.csv'


data = pd.read_csv(file_path)


time = data.iloc[:, 0]
absorbance = data.iloc[:, 1]


def exp_growth(x, a, b, c):
    return a * np.exp(-b * x) + c

def exp_decay(x, a, b, c):
    return a * np.exp(b * x) + c


decay_mask = (time > 1e-5) & (time < 4e-4)
growth_mask = (time > 4e-4) & (time < 1e-2)
decay2_mask = (time > 1e-2)  # New mask for the third exponential decay fit


print(f"Growth data points: {np.sum(growth_mask)}")
print(f"Decay data points: {np.sum(decay_mask)}")
print(f"Second Decay data points: {np.sum(decay2_mask)}")


initial_growth_params = [absorbance[growth_mask].max(), 1e3, absorbance[growth_mask].min()]  # Initial guess for growth parameters
popt_growth, pcov_growth = curve_fit(exp_growth, time[growth_mask], absorbance[growth_mask], p0=initial_growth_params, maxfev=10000)


initial_decay_params = [absorbance[decay_mask].max(), 1e3, absorbance[decay_mask].min()]  # Initial guess for decay parameters
popt_decay, pcov_decay = curve_fit(exp_decay, time[decay_mask], absorbance[decay_mask], p0=initial_decay_params, maxfev=10000)


initial_decay2_params = [absorbance[decay2_mask].max(), 1e0, absorbance[decay2_mask].min()]  # Adjust initial guess for decay parameters
popt_decay2, pcov_decay2 = curve_fit(exp_decay, time[decay2_mask], absorbance[decay2_mask], p0=initial_decay2_params, maxfev=10000)


fitted_growth = exp_growth(time[growth_mask], *popt_growth)
fitted_decay = exp_decay(time[decay_mask], *popt_decay)
fitted_decay2 = exp_decay(time[decay2_mask], *popt_decay2)


plt.figure(figsize=(10, 6))
plt.plot(time, absorbance, 'b-', label='1504 cm^-1')
plt.plot(time[growth_mask], fitted_growth, 'g-', label='Exponential Growth Fit')
plt.plot(time[decay_mask], fitted_decay, 'r-', label='Exponential Decay Fit')
plt.plot(time[decay2_mask], fitted_decay2, 'm-', label='Second Exponential Decay Fit')
plt.xscale('log')
plt.xlabel('Time (s)')
plt.ylabel('Absorbance (A.U)')
plt.legend()
plt.grid(True)
plt.show()


print("Exponential Growth Fit: a = {:.6f}, b = {:.6e}, c = {:.6f}".format(*popt_growth))
print("Equation: A(t) = {:.6f} * exp(-{:.6e} * t) + {:.6f}".format(*popt_growth))

print("Exponential Decay Fit: a = {:.6f}, b = {:.6e}, c = {:.6f}".format(*popt_decay))
print("Equation: A(t) = {:.6f} * exp({:.6e} * t) + {:.6f}".format(*popt_decay))

print("Second Exponential Decay Fit: a = {:.6f}, b = {:.6e}, c = {:.6f}".format(*popt_decay2))
print("Equation: A(t) = {:.6f} * exp({:.6e} * t) + {:.6f}".format(*popt_decay2))
