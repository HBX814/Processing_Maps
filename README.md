# Processing Maps for Mild, Microalloyed and Maraging Steel

Welcome to the repository for generating **Processing Maps** for microalloyed and maraging steel using Python. This project includes scripts to calculate and visualize the efficiency of power dissipation and instability regions based on flow stress data at varying temperatures and strain rates. The code uses numerical methods to interpolate data onto a finer grid for smoother contour plots, making it easier to interpret material behavior under different processing conditions.

## Overview

Processing maps are essential tools in materials science for identifying optimal conditions for hot working of metals. They combine the efficiency of power dissipation (η) and instability criteria (ξ) to highlight safe and unsafe processing regimes. This repository contains three distinct scripts that:

1. Generate a smoothed contour map for a generic dataset.
2. Create a detailed processing map for microalloyed steel.
3. Produce a processing map for maraging steel with interpolated efficiency data.

Each script calculates key parameters like strain rate sensitivity (m), efficiency of power dissipation (η), and instability (ξ), and visualizes the results using contour plots with `matplotlib`.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
  - [Script 1: Generic Smoothed Contour Map](#script-1-generic-smoothed-contour-map)
  - [Script 2: Microalloyed Steel Processing Map](#script-2-microalloyed-steel-processing-map)
  - [Script 3: Maraging Steel Processing Map](#script-3-maraging-steel-processing-map)
- [Code Explanation](#code-explanation)
  - [Key Concepts](#key-concepts)
  - [Data Interpolation](#data-interpolation)
  - [Visualization](#visualization)
- [Output](#output)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

To run the scripts in this repository, you need the following Python libraries installed:

- `numpy` - For numerical computations and array handling.
- `matplotlib` - For plotting contour maps and visualizations.
- `scipy` - For data interpolation using `griddata`.

You can install these dependencies using pip:

```bash
pip install numpy matplotlib scipy
```

## Installation

1. Clone this repository to your local machine:

   ```bash
   git clone https://github.com/HBX814/Processing_Maps.git
   cd processing-maps
   ```

2. Ensure you have Python 3.x installed along with the required libraries (see [Prerequisites](#prerequisites)).

3. Run the scripts individually as described in the [Usage](#usage) section.

## Usage

This repository contains three independent scripts for generating processing maps. Each script can be run separately to produce its respective output. Save the code snippets into separate `.py` files (e.g., `generic_map.py`, `microalloyed_map.py`, `maraging_map.py`) and execute them using Python.

### Script 1: Mild Steel Contour Map

**File**: `Mild_Steel_map.py`

This script creates a smoothed contour map for a small dataset of temperatures and strain rates with predefined efficiency values (η).

- **Input Data**: Hardcoded arrays for temperatures (900–1200°C), strain rates (0.01–5 s⁻¹), and efficiency values.
- **Process**: Interpolates data onto a finer grid using `scipy.interpolate.griddata` with the 'cubic' method for smoother contours.
- **Output**: A contour plot with labeled efficiency levels.

Run the script:

```bash
python generic_map.py
```

### Script 2: Microalloyed Steel Processing Map

**File**: `microalloyed_map.py`

This script generates a detailed processing map for microalloyed steel at a strain of 0.3, including efficiency contours and shaded instability regions.

- **Input Data**: Flow stress data for temperatures (850–1200°C) and strain rates (0.001–100 s⁻¹).
- **Process**: Calculates strain rate sensitivity (m) and efficiency (η) from flow stress data, interpolates onto a finer grid, and identifies instability regions (strain rates > 1 s⁻¹ between 850–1150°C).
- **Output**: A contour plot of efficiency with shaded instability regions.

Run the script:

```bash
python microalloyed_map.py
```

### Script 3: Maraging Steel Processing Map

**File**: `maraging_map.py`

This script creates a processing map for maraging steel at a strain of 0.3, focusing on smoothed efficiency contours.

- **Input Data**: Flow stress data for temperatures (900–1200°C) and strain rates (0.001–100 s⁻¹).
- **Process**: Computes strain rate sensitivity (m), efficiency (η), and instability criterion (ξ), then interpolates efficiency onto a finer grid for smooth visualization.
- **Output**: A contour plot of efficiency with labeled levels.

Run the script:

```bash
python maraging_map.py
```

## Code Explanation

### Key Concepts

- **Strain Rate Sensitivity (m)**: Calculated as the derivative of log(flow stress) with respect to log(strain rate), i.e., $$ m = \frac{d(\log\sigma)}{d(\log\dot{\epsilon})} $$.
- **Efficiency of Power Dissipation (η)**: Derived using the formula $$ \eta = \frac{2m}{m+1} $$, often expressed as a percentage.
- **Instability Criterion (ξ)**: Determined using dynamic material modeling, where negative values of $$ \xi = m + \frac{d(\log(m/(m+1)))}{d(\log\dot{\epsilon})} $$ indicate unstable flow.

### Data Interpolation

To achieve smooth contour lines, the scripts use `scipy.interpolate.griddata` with the 'cubic' method. This interpolates sparse data points (temperature and strain rate) onto a finer mesh, improving the visual quality of the plots.

- Original coarse grids are flattened into point-value pairs.
- A finer grid is created using `linspace` (for temperature) and `logspace` (for strain rate, due to logarithmic scaling).
- Interpolated values are computed for efficiency (η) on the finer grid.

### Visualization

The scripts use `matplotlib.pyplot` to create contour plots:

- Efficiency contours are drawn with labeled levels for easy interpretation.
- Logarithmic scaling is applied to the strain rate axis for better representation of wide-ranging values.
- Grids, labels, and titles are added for clarity, with instability regions shaded where applicable.

## Output

Each script generates a unique plot saved to the display (or can be modified to save as an image file like PNG). The outputs are:

1. **Generic Map**: A simple contour plot with smoothed efficiency lines.
2. **Microalloyed Steel Map**: A detailed map with efficiency contours and shaded instability regions.
3. **Maraging Steel Map**: A clean contour plot focusing on efficiency for maraging steel.

To save the plots, modify the scripts by adding `plt.savefig('filename.png')` before `plt.show()`.

## Contributing

Contributions are welcome! If you have suggestions for improvements, additional datasets, or new features (e.g., adding color maps or interactive plots), please follow these steps:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes and commit them (`git commit -m 'Add feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
