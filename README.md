# FIESTA

This repository complements the work and results published in [Fault Injection Evaluation with Statistical Analysis - How to Deal with Nearly Fabricated Large Circuits](https://eprint.iacr.org/2025/1287). Specifically, it contains information on how to set up FIESTA and provides the configuration of the case studies conducted in the aforementioned publication.

**Note:** The FIESTA executable is currently only available as part of [PROLEAD](https://github.com/ChairImpSec/PROLEAD).

## Prerequisites

To use FIESTA/PROLEAD, you must have a working installation of the [Nix package manager](https://nixos.org/).

## Installation

1. **Clone PROLEAD (containing FIESTA):**
   ```bash
   git clone https://github.com/ChairImpSec/PROLEAD
   ```

2. **Enter the cloned repository:**
   ```bash
   cd PROLEAD
   ```

3. **Enter the nix-shell:**
   ```bash
   nix-shell
   ```

4. **Build FIESTA/PROLEAD:**
   ```bash
   make release
   ```

Now you are ready to execute FIESTA/PROLEAD.

For more information regarding the installation process, please refer to the [PROLEAD wiki](https://github.com/ChairImpSec/PROLEAD/wiki/Installation).

## Reproducing the Case Studies

In the root folder of the cloned repository, you will find the following folder structure:

```
examples/fiesta
└── asic
    ├── nang45
    │   ├── aes-hpc3-pipelined-d1
    │   │   ├── 00-design
    │   │   ├── 01-functional-correct
    │   │   ├── 02-experiments
    │   │   └── original-results
    │   ├── aes-hpc3-pipelined-d2
    │   │   ├── 00-design
    │   │   ├── 01-functional-correct
    │   │   ├── 02-experiments
    │   │   └── original-results
    │   ├── aes-ic2-w-dec-d1-k4
    │   │   ├── 00-design
    │   │   ├── 01-functional-correct
    │   │   ├── 02-experiments
    │   │   └── original-results
    │   ├── aes-ic2-w-dec-d2-k4
    │   │   ├── 00-design
    │   │   ├── 01-functional-correct
    │   │   ├── 02-experiments
    │   │   └── original-results
    │   ├── aes-mvoting-d1
    │   │   ├── 00-design
    │   │   ├── 01-functional-correct
    │   │   ├── 02-experiments
    │   │   └── original-results
    │   ├── aes-mvoting-d2
    │   │   ├── 00-design
    │   │   ├── 01-functional-correct
    │   │   ├── 02-experiments
    │   │   └── original-results
    │   └── aes-unprotected
    │       ├── 00-design
    │       ├── 01-functional-correct
    │       ├── 02-experiments
    │       └── original-results
    └── sky130
        ...
```

### Directory Structure Explanation

- **`00-design`:** Contains the circuit designs that were analyzed.
- **`01-functional-correct`:** Includes a simple configuration that can be used to verify the correctness of the given netlist and its simulation.
- **`02-experiments`:** Contains all configurations to compute the experiments using the most recent version of FIESTA.
- **`original-results`:** Provides the results visualized in the publication.

**Note:** The configurations in `original-results` cannot be used for the current version of FIESTA, as some options were renamed for clarity.
