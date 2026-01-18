# PN-Junction-Depletion-Width-Calculator

An interactive web-based calculator for analyzing PN junctions with arbitrary doping profiles in semiconductor physics. This tool visualizes the depletion width and related electrical properties of PN junctions under reverse-biased voltage conditions.

## Overview

This project provides a comprehensive simulation of PN junction behavior using the depletion approximation. It allows users to define custom donor (N_D) and acceptor (N_A) concentration profiles and calculates the resulting depletion region characteristics.

## Features

- **Custom Doping Profiles**: Define arbitrary mathematical functions for donor and acceptor concentrations
- **Interactive Visualization**: Real-time plotting of doping profiles and depletion width
- **Preset Configurations**: Quick-load buttons for common junction types:
  - Abrupt junction
  - Linearly graded junction
- **Mathematical Functions Support**: Includes trigonometric, exponential, logarithmic functions, and the Heaviside step function
- **Physical Calculations**: Computes charge density, electric field, and voltage distributions based on semiconductor physics principles

## Physics Background

The calculator uses the depletion approximation to model PN junctions, where:
- The depletion width W exists around the p-n transition
- Charge carrier densities are negligible within the depletion region
- Outside the depletion region, carrier densities equal doping concentrations
- The semiconductor is electrically neutral outside the depletion width

The tool calculates:
1. **Charge density distribution** ρ(x) based on doping profiles
2. **Electric field** E(x) through integration of charge density
3. **Voltage** V across the junction

## Live Demo

Access the interactive calculator at: [GitHub Page](https://simonprato.github.io/pn-depletion-width/)

## Project Structure

```
PN-Junction-Depletion-Width-Calculator/
├── index.html          # Main HTML interface with embedded JavaScript
├── calculations.js     # Core calculation functions for depletion width
├── img/                # Formula images and example plots
│   ├── formula_charge_density.png
│   ├── formula_electric_field.png
│   ├── formula_voltage.png
│   └── plots.png
└── README.md
```

## Technologies Used

- HTML5/CSS3 for interface
- JavaScript for calculations and interactivity
- jQuery (v3.6.0) for DOM manipulation
- Plotly.js for interactive plotting
- Flot for additional charting capabilities
- MathJax for mathematical notation rendering

## Usage

1. Enter mathematical expressions for donor concentration N_D(x) and acceptor concentration N_A(x)
2. Specify the spatial range (x1 to x2) in micrometers
3. Click "Plot" to visualize the results
4. View both the doping concentration profile and depletion width as a function of reverse-biased voltage

## Example Inputs

**Abrupt Junction:**
- N_D(x) = `1.1E21*H(x-5)` m⁻³
- N_A(x) = `1.1E21 - 1.1E21*H(x-5)` m⁻³

**Linearly Graded Junction:**
- N_D(x) = `1E20*x` m⁻³
- N_A(x) = `5E20` m⁻³

## Mathematical Functions Supported

- Trigonometric: sin, cos, tan, asin, acos, atan
- Exponential/Logarithmic: exp, log
- Power: pow(x,y) or x**y
- Utility: sqrt, abs, round, H (Heaviside step function)
- Constants: pi

## Screenshots

![Depletion Width and Doping Profile Plots](img/plots.png)

## License

This project is open source and available for educational and research purposes.

## Contributing

Contributions, issues, and feature requests are welcome. Feel free to check the issues page or submit a pull request.
