# PN Junction Depletion Width Calculator

An interactive web-based tool for analyzing PN junctions with arbitrary doping profiles in semiconductor physics. This calculator visualizes depletion width, electric field, and charge density distributions using the depletion approximation model.

## Overview

This project provides a comprehensive simulation of PN junction behavior, allowing users to define custom donor (N_D) and acceptor (N_A) concentration profiles and calculate the resulting depletion region characteristics under reverse-biased conditions.

## Features

- **Custom Doping Profiles**: Define arbitrary mathematical functions for donor and acceptor concentrations
- **Interactive Real-Time Visualization**: Dual-plot display showing:
  - Doping concentration profiles (N_D, N_A, and net concentration)
  - Depletion width as a function of reverse-bias voltage
- **Preset Junction Configurations**: Quick-load buttons for:
  - Abrupt junction (step function doping)
  - Linearly graded junction

## Physics Background

### Depletion Approximation Model

The calculator uses the depletion approximation to model PN junctions:
- A depletion width **W** exists around the p-n transition
- Charge carrier densities are negligible within the depletion region
- Outside the depletion region, carrier densities equal doping concentrations
- The semiconductor is electrically neutral outside the depletion width

### Fundamental Equations

The tool calculates three key distributions:

1. **Charge Density Distribution** ρ(x):
   - Based on net doping concentration: N(x) = N_A(x) - N_D(x)
   - ρ(x) = q × N(x) where q is elementary charge

2. **Electric Field** E(x):
   - Obtained by integrating the charge density
   - E(x) = -(q/ε) ∫ N(x) dx
   - Where ε is the permittivity of the semiconductor

3. **Voltage** V:
   - Calculated by integrating the electric field across the depletion region
   - V = -∫ E(x) dx from x_p to x_n

### Physical Constants Used

- Elementary charge: q = 1.602 × 10⁻¹⁹ C
- Permittivity of free space: ε₀ = 8.854 × 10⁻¹² F/m
- Relative permittivity (Silicon): εᵣ = 12
- Combined permittivity: ε = εᵣ × ε₀

## Live Demo

Access the interactive calculator at: [https://simonprato.github.io/pn-depletion-width/](https://simonprato.github.io/pn-depletion-width/)

## Project Structure

```
PN-Junction-Depletion-Width-Calculator/
├── index.html                      # Main application interface
├── css/
│   └── styles.css                  # Styling and layout
├── js/
│   ├── main.js                     # Main application logic and event handlers
│   ├── constants.js                # Physical constants definitions
│   ├── mathUtils.js                # Mathematical utility functions
│   ├── dopingProfile.js            # Doping profile parsing and evaluation
│   ├── depletionCalculations.js   # Core depletion width calculations
│   └── plotting.js                 # Visualization and plotting functions
├── img/                            # Formula images and examples
│   ├── formula_charge_density.png
│   ├── formula_electric_field.png
│   ├── formula_voltage.png
│   └── plots.png
└── README.md                       # This file
```

## Technologies Used

- **Frontend**: HTML5, CSS3
- **JavaScript Libraries**:
  - jQuery 3.6.0 - DOM manipulation
  - Flot 0.8.3 - Interactive plotting
  - MathJax 2.7.1 - Mathematical notation rendering
- **Architecture**: Modular JavaScript with separation of concerns

## Usage Guide

### Basic Usage

1. **Enter Doping Profiles**: Define mathematical expressions for:
   - N_D(x): Donor concentration in m⁻³
   - N_A(x): Acceptor concentration in m⁻³
2. **Set Spatial Range**: Specify x₁ and x₂ in micrometers (µm)
3. **Calculate**: Click the "Plot" button to visualize results
4. **Analyze**: View both plots:
   - Left plot: Depletion width vs. reverse-bias voltage
   - Right plot: Doping concentration profiles

### Example Inputs

#### Abrupt Junction
Represents a sharp transition between p and n regions:
```
N_D(x) = 1.1E21*H(x-5)                  [m⁻³]
N_A(x) = 1.1E21 - 1.1E21*H(x-5)         [m⁻³]
Range: x = 0 to 10 µm
```

#### Linearly Graded Junction
Represents a gradual transition:
```
N_D(x) = 1E20*x                          [m⁻³]
N_A(x) = 5E20                            [m⁻³]
Range: x = 0 to 10 µm
```

#### Custom Exponential Profile
```
N_D(x) = 1E21*exp(-(x-5)**2)            [m⁻³]
N_A(x) = 5E20*H(5-x)                     [m⁻³]
Range: x = 0 to 10 µm
```

### Mathematical Functions Supported

| Function | Syntax | Description |
|----------|--------|-------------|
| Trigonometric | sin(x), cos(x), tan(x) | Standard trig functions |
| Inverse Trig | asin(x), acos(x), atan(x) | Arc functions |
| Exponential | exp(x) | e^x |
| Logarithm | log(x) | Natural logarithm (ln) |
| Power | pow(x,y) or x**y | x raised to power y |
| Square Root | sqrt(x) | √x |
| Absolute Value | abs(x) | \|x\| |
| Rounding | round(x) | Round to nearest integer |
| Heaviside | H(x) | Step function: 0 for x<0, 0.5 for x=0, 1 for x>0 |
| Constant | pi | π ≈ 3.14159... |

### Important Notes

- **Multiplication**: Must be explicit with `*` symbol (e.g., `3*x` not `3x`)
- **Exponentiation**: Use `**` or `pow()` (e.g., `x**2` not `x^2`)
- **Variables**: Only `x` is recognized as the spatial variable
- **Units**: 
  - Position (x): micrometers (µm)
  - Concentration: m⁻³
  - Voltage: Volts (V)

## How It Works

### Calculation Algorithm

1. **Parse Input**: Convert user expressions to evaluable JavaScript functions
2. **Sample Doping**: Evaluate N_D(x) and N_A(x) at 301 points across the range
3. **Calculate Net Doping**: Compute N(x) = N_A(x) - N_D(x)
4. **Validate Junction**: Ensure exactly one sign change (one PN junction)
5. **Find Junction Position**: Locate where N(x) crosses zero
6. **Iterate Depletion Width**: 
   - Start from junction and extend depletion region
   - Calculate electric field by integrating charge density
   - Balance fields on both sides of the junction
   - Compute voltage for each depletion width
7. **Plot Results**: Display concentration profiles and W-V relationship

### Key Algorithms

- **Cumulative Integration**: Trapezoid rule with fractional index support
- **Field Balancing**: Iteratively extends depletion region to maintain field continuity
- **Interpolation**: Linear interpolation for smooth voltage-width curves

## Visualization Details

### Depletion Width Plot (Left)
- **X-axis**: Depletion width in µm
- **Y-axis**: Reverse-bias voltage in V
- **Curves**:
  - Green: Total depletion width (W_total)
  - Red: p-side depletion width (W_p)
  - Blue: n-side depletion width (W_n)

### Doping Profile Plot (Right)
- **X-axis**: Position (x) in µm
- **Y-axis**: Concentration in m⁻³ (exponential notation)
- **Curves**:
  - Blue: Donor concentration (N_D)
  - Red: Acceptor concentration (N_A)
  - Black: Net concentration (N_A - N_D)

## Limitations and Assumptions

- **Single Junction**: Only handles one PN junction per profile
- **Depletion Approximation**: Assumes complete depletion within W
- **Reverse Bias Only**: Calculations valid for reverse-biased conditions
- **Silicon Properties**: Uses εᵣ = 12 (typical for silicon)
- **Temperature**: Room temperature (300K) is assumed
- **Abrupt Transitions**: Mathematical discontinuities may need careful handling

## Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is open source and available for educational and research purposes.

**Note**: For best results, ensure your doping profiles create exactly one PN junction (one sign change in N_A - N_D) within the specified spatial range.
