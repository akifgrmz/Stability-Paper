# Effort-Dependent CCFES: Stability and Sensitivity Analysis

[![MATLAB](https://img.shields.io/badge/MATLAB-R2020b+-blue.svg)](https://www.mathworks.com/products/matlab.html)
[![License](https://img.shields.io/badge/License-Research-green.svg)]()
[![Status](https://img.shields.io/badge/Status-Active-success.svg)]()

## Overview

This repository contains the computational models, simulation code, and analysis scripts for investigating the stability and sensitivity of **effort-dependent Contralaterally-Controlled Functional Electrical Stimulation (CCFES)** for post-stroke hand rehabilitation.

### Analysis Capabilities
- **Stability Analysis**: Nyquist methods with uncertainty bounds
- **Sensitivity Analysis**: Parameter sweeps across 5 key variables
- **Performance Metrics**: Tracking error, SNR, effort accuracy (R²)
- **Case Scenarios**: Mild, moderate, severe impairment + filter quality scenarios

## Requirements

### Software
- **MATLAB** R2020b or later
- **Simulink** (included with MATLAB)

### Toolboxes
- Control System Toolbox
- Statistics and Machine Learning Toolbox
- Optimization Toolbox
- Signal Processing Toolbox (recommended)

## Usage

### Quick Start

1. **Load baseline model:**
```matlab
   open_system('NSFsim_syn');
```

2. **Run a single simulation:**
```matlab
   SimTime = 10;  % 10 second simulation
   sim('NSFsim_syn', SimTime);
```

3. **View results:**
```matlab
   plot(ans.Outcome(:,5))  % Plot paretic hand opening
   ylabel('Hand Opening (%)')
   xlabel('Time (s)')
```

### Sensitivity Analysis

Run parameter sweeps to analyze system behavior:
```matlab
% Example: Vary volitional hand opening time constant
low = 1;
high = 4;
NumPoints = 100;
wc = logspace(log10(low), log10(high), NumPoints);

for i = 1:NumPoints
    set_param('NSFsim_syn/GainP', 'Gain', sprintf('%0.2f', wc(i)));
    sim('NSFsim_syn', SimTime);
    % Store results...
end
```

**Last Updated:** December 2024  
**Status:** Active Development  
**MATLAB Version Tested:** R2020b, R2023a
