# FIESTA

[![Paper](https://img.shields.io/badge/Paper-IACR%20ePrint%202025.1287-blue)](https://eprint.iacr.org/2025/1287)
[![PROLEAD](https://img.shields.io/badge/Part%20of-PROLEAD-green)](https://github.com/ChairImpSec/PROLEAD)
[![Nix](https://img.shields.io/badge/Requires-Nix%20Package%20Manager-5277C3)](https://nixos.org/)

This repository complements the work and results published in **[Fault Injection Evaluation with Statistical Analysis - How to Deal with Nearly Fabricated Large Circuits](https://eprint.iacr.org/2025/1287)**.
Specifically, it contains information on how to set up FIESTA and provides the configuration of the case studies conducted in the aforementioned publication.

> [!NOTE]
> The FIESTA executable is currently only available as part of [PROLEAD](https://github.com/ChairImpSec/PROLEAD).

---

## 📋 Prerequisites

To use FIESTA/PROLEAD, you must have a working installation of the [Nix package manager](https://nixos.org/).

---

## 🛠️ Installation

1. **Clone PROLEAD (includes FIESTA):**
   ```bash copy
   git clone https://github.com/ChairImpSec/PROLEAD
   ```

2. **Enter the cloned repository:**
   ```bash copy
   cd PROLEAD
   ```

3. **Enter the nix-shell:**
   ```bash copy
   nix-shell
   ```

4. **Build FIESTA/PROLEAD:**
   ```bash copy
   make release
   ```

Now you are ready to execute FIESTA/PROLEAD.

 > [!TIP]
 > For detailed installation steps, see the **[PROLEAD Wiki](https://github.com/ChairImpSec/PROLEAD/wiki/Installation)**.

---

## 🔬 Reproducing the Case Studies

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

### 📂 Directory Structure
The examples/fiesta directory contains a single top-level subdirectory, `asic`, which organizes all ASIC-related designs.
Future work may introduce additional categories (e.g., FPGAs) alongside `asic`.

The second hierarchical level (nang45, sky130) divides the experiments conducted in [Fault Injection Evaluation with Statistical Analysis - How to Deal with Nearly Fabricated Large Circuits](https://eprint.iacr.org/2025/1287), into two parts:
- **`nang45`**: Experiments studying designs implemented using the [Nangate 45 PDK](https://www.cs.upc.edu/~jpetit/CellRouting/nangate/Front_End/Doc/Databook/CornerList.html).
- **`sky130`**: Experiments studying designs implemented using the [Skywater 130 PDK](https://skywater-pdk.readthedocs.io/en/main/).

The next hierarchical level (e.g.,aes-hpc3-pipelined-d1, ..., aes-unprotected) identifies the circuits under investigation.
This is summarized in the following table:
| Level | Description |
|-------|-------------|
| **`asic/`** | Top-level directory for ASIC designs (FPGA support may be added later). |
| **`nang45/` / `sky130/`** | PDK-specific experiments (Nangate 45nm or SkyWater 130nm). |
| **`<circuit-name>`** | Individual circuits (e.g., `aes-unprotected`). |

Each **`<circuit-name>`** directory contains the following directories:
- **`00-design`:** Contains the circuit designs/netlist (verilog files) that were analyzed.
- **`01-functional-correct`:** Includes a simple configuration that can be used to verify the correctness of the given netlist and its simulation.
- **`02-experiments`:** Contains all configurations to compute the experiments using the most recent version of FIESTA.
- **`original-results`:** Provides the results used to create the Figures in the original publication ([Fault Injection Evaluation with Statistical Analysis - How to Deal with Nearly Fabricated Large Circuits](https://eprint.iacr.org/2025/1287).

> [!NOTE]
> The configurations in `original-results` cannot be used for the current version of FIESTA, as some options were renamed for clarity.
> However, the results produced with these configurations can be reproduced when adapting the `config.json` files to the updated configuration format.
> This updated configuration format was introduced to provide better clarity on what each setting does.
> The configurations given in `01-functional-correct` and `02-experiments` follow this updated configuration format, but leading to the same computation the configs in `orignal-results` lead.

---

### Mapping Figures to Directories
The following table maps the Figures (and Sections) of [Fault Injection Evaluation with Statistical Analysis - How to Deal with Nearly Fabricated Large Circuits] to a subdirectory of `prolead/examples/fiesta/asic`,
which contains the configurations to generate the Figures.
The label column additionally provides information on which config was used to generate which line in the line charts.

| Directory **`<circuit-name>`** | Section                                          | Figure    | Label        |
| ------------------------------ | ------------------------------------------------ | --------- | ------------ |
| sky130/a2o-circuit             | 3.6 An Illustrative Example                      | Figure  3 |              |
| nang45/1-1-sinina              | 4.3.2 Accuracy                                   | Figure  4 |              |
| nang45/1-1-sinina              | 4.3.3 Efficiency                                 | Figure  5 |              |
| nang45/1-1-sinina              | 4.3.3 Efficiency                                 | Figure  6 |              |
| nang45/aes-unprotected         | 5.2 Evaluations                                  | Figure  7 |              |
| nang45/aes-mvoting-d1          | 5.2.1 Influence of Replication                   | Figure  8 | Three Inst.  |
| nang45/aes-mvoting-d2          | 5.2.1 Influence of Replication                   | Figure  8 | Five Inst.   |
| nang45/aes-ic2-w-dec-d1-k4     | 5.2.2 Influence of Impeccable Circuits II (ICII) | Figure  9 | ICII (δ = 3) |
| nang45/aes-ic2-w-dec-d2-k4     | 5.2.2 Influence of Impeccable Circuits II (ICII) | Figure  9 | ICII (δ = 5) |
| nang45/aes-hpc3-pipelined-d1   | 5.2.3 Influence of Masking                       | Figure 10 | HPC3 (d = 1) |
| nang45/aes-hpc3-pipelined-d2   | 5.2.3 Influence of Masking                       | Figure 10 | HPC3 (d = 2) |


<!-- TODO: Add mappings for case studies in Section 7 -->

---

### Experiment Naming Scheme
The 02-experiments subdirectories of the **`<circuit-name>`** directories given in the [table above](#mapping-figures-to-directories) contain multiple subdirectories with names, such as, sa0-p2e007.
These strings are build using the following naming scheme: <fault-type>-<probability>.
The `<fault-type>` is either sa0 (stuck-at-zero), sa1 (stuck-at-one), or tgl (toggle).
The *`<probability>` is further divided in two parts: `p<base>e<exponent>`.
Based on this naming convention `<probability>` is interpreted as `<base>`<sup>-`<exponent>`</sup>.
Thus, sa0-p2e007 contains the configuration for an experiment where stuck-at-zero faults are induced with probability 2<sup>-7</sup>.
Inside these folders, following the `<fault-type>-<probability>` naming scheme, you may find another directory level.
Specifically, a `sa0-p2e007` directory might contain the folders `all-cells` and `storage-cells`.
In `all-cells` all cells of the circuit are attacked, while in `storage-cells` only cells with a sequential characteristic, such as registers, are considered by FIESTA.

---

### Running an Experiment
Putting things together: The folder `aes-unprotected/02-experiments/sa0-p2e006/all-cells` can be used to compute the results depicted in Figure 7a for $\log_2(\varphi) = -6$, while `aes-unprotected/02-experiments/sa0-p2e026/all-cell` can be used to generate the results for $\log_2(\varphi) = -26$.

When starting FIESTA with a `run.sh` file located in any of these directories, the corresponding `config.json` is read by FIESTA.
Assume that the working directory is `aes-unprotected/02-experiments/sa0-p2e006/all-cells` and `./run.sh` is executed; then FIESTA will first report:

```
Found child with key: analysis_strategy and type: string
<...>
Successfully validated the settings file.
Successfully read the library with name "nang45".
Successfully parsed 35 cells from the library.
Successfully found buffer cell with identifier "BUF_X1" and others.
```
where <...> simply replaces multiple logger lines that correspond to file parsing.
Then the simulation process is started, and FIESTA reports:



```
[ ] Prepare simulation engin...
[+] Simulation enging is prepared with:
    Number of shares :1
    Number of groups :128
    Number of bits :1
[+] Available fault locations: 394220
```
This gives some information on what is evaluated in the following.
Specifically, the number of faults that can be injected is reported 394220.
Note that this number is the product of the gates that are targeted and the clock cycles in which a fault can be injected.
The lines:
```
    Number of shares :1
    Number of groups :128
    Number of bits :1
```
are debug prints and can be ignored.

The progress of the simulation is indicated by
```
[0.00048204] Step:  3/15, Simulation:    0/1023
<...>
[   5184.18] Step:  5/15, Simulation: 1023/1023
```
Where <...> replaces furhter intermediate steps.

The computed result is reported with the following format:
```
-------------------- Evaluation Completed --------------------
     Computation Time: 5184.55 seconds!
     Individual Faults: 394220
     Faulted Cycles:
        1
        2
        3
        <...>
        228
        229
        230
     Effective Faults Per Thread:
        196608
        196608
        131072
        131072
        196608
        196608
     Effective Faults Total:
         Success 1048576
         Trials 1048576


    Probability faults lead to non correctable fault:
        p_l: 0.99998616
        p_u: 1
```
where <...> replaces the numbers 4 to 227.
To reproduce the result of Figures 7 to 10, the following 3 lines must be considered:
```
    Probability faults lead to non correctable fault:
        p_l: 0.99998616
        p_u: 1
```

Here p_l indicates the lower boundaries of the advantage of the adversary (in the FIESTA paper denoted with $(\mu^\ell, \mu^u)$.
$\mu^\ell$ is the lower bound, while $\mu^u$ is the upper bound.
Note that the previous three lines relate to ```aes-unprotected/02-experiments/sa0-p2e006/all-cells```.
For a smaller probability, such as ```aes-unprotected/02-experiments/sa0-p2e024/all-cells```, the results would be

```
    Probability faults lead to non correctable fault:
        p_l: 0.0076496222
        p_u: 0.0084395282
```



> [!NOTE]
> Currently, we recompute the results using the new configuration version.
> These computations follow an improved report format, which is in line with [PROLEAD]'s logging to increase uniformity.
> After the computation has completed, they will be added.

> [!NOTE]
> FIESTA was submitted as artifact to CHES2025.
> To keep our changes since the initial artifact submission transparent, we have tagged the state initially submitted with `fiesta-initial`.
> This applies to both repositories, [FIESTA](https://github.com/ChairImpSec/FIESTA) and [PROLEAD](https://github.com/ChairImpSec/PROLEAD).
