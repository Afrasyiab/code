
# 📉 Calculating Bulk Modulus and Specific Heat

**Author:** Afrasyiab Ahmed  
📧 [afrayiabahmed@gmail.com](mailto:afrayiabahmed@gmail.com)

---

## 📘 Introduction

This section focuses on the computation of two key thermodynamic properties:

- **Bulk Modulus (B)**: Describes a material's resistance to uniform compression.
- **Specific Heat Capacity (Cₚ)**: Indicates the amount of heat required to change the temperature of a unit mass of a substance.

### 🧮 Bulk Modulus Formula:

The bulk modulus is calculated using elastic constants:

\[
B = \frac{1}{9} \left[2(c_{11} + c_{12}) + c_{33} + 4c_{13}\right]
\]

---

## 🔷 Bulk Modulus Calculation

We use the elastic constants from the Excel file to calculate the bulk modulus.

### 📜 Python Code

```python
import numpy as np
import pandas as pd

file_path = 'interpolate.xlsx'
sheet_name = 'c13_r'
df = pd.read_excel(file_path, sheet_name=sheet_name)

c1112 = df['c11+c12)jkbar'].values
c33 = df['(c33)jkbar'].values
c13 = df['c13'].values

# Bulk modulus calculation
B = 1 / 9 * (2 * c1112 + c33 + 4 * c13)

# Save results
results_df = pd.DataFrame({'B': B})
results_df.to_excel('output_results.xlsx', index=False)
```

---

## 🔶 Specific Heat Capacity Calculation

The heat capacity is computed using temperature (T), volume (V), bulk modulus (B₀), thermal expansion coefficient (β), and constant-volume heat capacity (Cᵥ):

\[
C_p = TVB_0 \beta^2 + C_v
\]

### 📜 Python Code

```python
import numpy as np
import pandas as pd

file_path = 'ch_graphs.xlsx'
df = pd.read_excel(file_path, sheet_name='cp')

T = df['T'].values
V = df['V'].values
B0 = df['B0'].values
beta = df['beta'].values
Cv = df['Cv'].values

# Compute specific heat capacity at constant pressure
c_p_values = T * V * B0 * beta**2 + Cv

# Save to DataFrame and Excel
df['cp'] = c_p_values
df.to_excel('output_cp.xlsx', index=False)
```

---

## 📂 Output

- **Bulk modulus values** saved in: `output_results.xlsx`
- **Specific heat capacity values** saved in: `output_cp.xlsx`

---

## ✅ Summary

By combining mechanical (elastic constants) and thermal (volume, temperature, expansion) properties, we have successfully calculated:

- Bulk modulus to understand compressibility.
- Specific heat capacity for thermal analysis.

---
