# FIESTA

[![IACR ePrint](https://img.shields.io/badge/Paper-IACR%20ePrint%202025.1287-blue)](https://eprint.iacr.org/2025/1287)
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

``` plaintext
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
The `<examples/fiesta>` directory contains a single top-level subdirectory, `asic`, which organizes all ASIC-related designs.
Future work may introduce additional categories (e.g., FPGAs) alongside `asic`.

The second hierarchical level (nang45, sky130) divides the experiments conducted in [Fault Injection Evaluation with Statistical Analysis - How to Deal with Nearly Fabricated Large Circuits](https://eprint.iacr.org/2025/1287), into two parts:
- **`nang45`**: Experiments studying designs implemented using the [Nangate 45 PDK](https://www.cs.upc.edu/~jpetit/CellRouting/nangate/Front_End/Doc/Databook/CornerList.html).
- **`sky130`**: Experiments studying designs implemented using the [Skywater 130 PDK](https://skywater-pdk.readthedocs.io/en/main/).

The next hierarchical level (e.g.,aes-hpc3-pipelined-d1, ..., aes-unprotected) identifies the circuits under investigation.

This structure is summarized in the following table:
| Level | Description |
|-------|-------------|
| **`asic/`** | Top-level directory for ASIC designs (FPGA support may be added later). |
| **`nang45/` / `sky130/`** | PDK-specific experiments (Nangate 45nm or SkyWater 130nm). |
| **`<circuit-name>`** | Individual circuits (e.g., `aes-unprotected`). |

Each **`<circuit-name>`** directory contains the following directories:
- **`00-design`:** Contains the circuit designs/netlist (verilog files) that were analyzed.
- **`01-functional-correct`:** Includes a simple configuration that can be used to verify the correctness of the given netlist and its simulation.
- **`02-experiments`:** Contains all configurations to compute the experiments using the most recent version of FIESTA.
- **`original-results`:** Provides the results used to create the Figures in the original publication ([Fault Injection Evaluation with Statistical Analysis - How to Deal with Nearly Fabricated Large Circuits](https://eprint.iacr.org/2025/1287)).

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
- The **`<fault-type>`** is either sa0 (stuck-at-zero), sa1 (stuck-at-one), or tgl (toggle).
- The **`<probability>`** is further divided in two parts: `p<base>e<exponent>`.

Based on this naming convention `<probability>` is interpreted as `<base>`<sup>-`<exponent>`</sup>.
Thus, sa0-p2e007 contains the configuration for an experiment where stuck-at-zero faults are induced with probability 2<sup>-7</sup>.
Inside these folders, following the `<fault-type>-<probability>` naming scheme, you may find another directory level.
Specifically, a `sa0-p2e007` directory might contain the folders `all-cells` and `storage-cells`.
In `all-cells` all cells of the circuit are attacked, while in `storage-cells` only cells with a sequential characteristic, such as registers, are considered by FIESTA.

---

### Running an Experiment
Putting things together: The folder `aes-unprotected/02-experiments/sa0-p2e006/all-cells` can be used to compute the results depicted in Figure 7a for $\log_2(\varphi) = -6$, while `aes-unprotected/02-experiments/sa0-p2e026/all-cell` can be used to generate the results for $\log_2(\varphi) = -26$.

When starting FIESTA with a `./run.sh` file located in any of these directories, the corresponding `config.json` is read by FIESTA.
In all following logs `<TIMESTAMP>` replaces the date and time at which the log´ entries were created.

Assume that the working directory is `aes-unprotected/02-experiments/sa0-p2e007/all-cells` and `./run.sh` is executed; then FIESTA will first report:

``` plaintext
[<TIMESTAMP>] Successfully validated the settings file.
[<TIMESTAMP>] Successfully read the library with name "nang45".
[<TIMESTAMP>] Successfully parsed 35 cells from the library.
[<TIMESTAMP>] Successfully found buffer cell with identifier "BUF_X1" and others.
[<TIMESTAMP>] Successfully read design file with topmodule "circuit"!
[<TIMESTAMP>] ------------------------------------------------------------------------------------------------------------------------
```
These log entries are produced by the parser and inform the user about some properties of the parsed settings and netlist.

Before the simulation process is started, FIESTA computes and reports fundamental properties of the analysis:
``` plaintext
[<TIMESTAMP>] Prepare statistical evaluation of adversary 0 in the general random fault model!
[<TIMESTAMP>] All possible faults are derived from configuration file.
[<TIMESTAMP>] Properties of the analysis:
[<TIMESTAMP>] ---------------------------------------------------------------------------------------------------
[<TIMESTAMP>] | #Used Threads |      #Faults |   #Positions | Confidence Level |  Fault Probability (min / max) |
[<TIMESTAMP>] ---------------------------------------------------------------------------------------------------
[<TIMESTAMP>] |             6 |       394220 |         1714 |         0.999999 |            0.007812 / 0.007812 |
[<TIMESTAMP>] ---------------------------------------------------------------------------------------------------
```
These log entries contain the below defined key metrics:
 | Metric                                                                | Description                                                                                              |
 |-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
 | **Total sampleable faults** (`#faults`)                               | Product of the number of targeted gates (#positions) and the clock cycles available for fault injection. |
 | **Faultable gate count** (`#positions`)                               | Number of distinct gates where faults can be injected.                                                   |
 | **Confidence level**                                                  | User-configured statistical confidence for the analysis.                                                 |
 | **Fault probability range** (`Fault Probability (min / max)`)         | Minimum and maximum probability across all injectable faults.                                            |
Note that `#faults` is the product of the gates that are targeted and the clock cycles in which a fault can be injected.

The following log header is printed at the start of the simulation to track progress:
``` plaintext
[<TIMESTAMP>] Analysis is starting...
[<TIMESTAMP>] -----------------------------------------------------------------------------------------------------------
[<TIMESTAMP>]         Elapsed Time |        Used Memory | #Effective Faults | Lower Bound | Upper Bound | Interval Size |
[<TIMESTAMP>] -----------------------------------------------------------------------------------------------------------
```
This header displays real-time metrics for each simulation step:

- **Resource Metrics:** `Elapsed Time` and `Used Memory`
- **Fault Analysis:**
  - `#Effective Faults`: Cumulative count of effective faults across all (computed) steps
  - `Lower Bound`/`Upper Bound`: Adversary advantage bounds derived from:
    - Effective faults count
    - Processed simulations
    - User-defined confidence level ($\gamma$)
    - `Interval Size`: Confidence interval width ($L = \mu^u - \mu^\ell$)

The batch size (simulations per step) is configurable via `config.json`.

The progress of the simulation is then indicated by values corresponding to the simulation header:
``` plaintext
[<TIMESTAMP>] |         0-00:04:08 |   0TB    0GB 831MB |   65536 /   65536 |  0.99977864 |  1.00000000 |    0.00022136 |
[<TIMESTAMP>] |         0-00:09:35 |   0TB    0GB 831MB |  131072 /  131072 |  0.99988931 |  1.00000000 |    0.00011069 |
[<TIMESTAMP>] |         0-00:14:58 |   0TB    0GB 831MB |  196608 /  196608 |  0.99992621 |  1.00000000 |    0.00007379 |
[<TIMESTAMP>] |         0-00:20:32 |   0TB    0GB 831MB |  262144 /  262144 |  0.99994466 |  1.00000000 |    0.00005534 |
[<TIMESTAMP>] |         0-00:26:19 |   0TB    0GB 831MB |  327680 /  327680 |  0.99995572 |  1.00000000 |    0.00004428 |
[<TIMESTAMP>] |         0-00:31:43 |   0TB    0GB 831MB |  393216 /  393216 |  0.99996310 |  1.00000000 |    0.00003690 |
[<TIMESTAMP>] |         0-00:37:08 |   0TB    0GB 831MB |  458752 /  458752 |  0.99996837 |  1.00000000 |    0.00003163 |
[<TIMESTAMP>] |         0-00:42:33 |   0TB    0GB 831MB |  524288 /  524288 |  0.99997233 |  1.00000000 |    0.00002767 |
[<TIMESTAMP>] |         0-14:19:44 |   0TB    0GB 831MB |  589824 /  589824 |  0.99997540 |  1.00000000 |    0.00002460 |
[<TIMESTAMP>] |         0-14:23:35 |   0TB    0GB 831MB |  655360 /  655360 |  0.99997786 |  1.00000000 |    0.00002214 |
[<TIMESTAMP>] |         0-14:28:39 |   0TB    0GB 831MB |  720896 /  720896 |  0.99997987 |  1.00000000 |    0.00002013 |
[<TIMESTAMP>] |         0-14:33:56 |   0TB    0GB 831MB |  786432 /  786432 |  0.99998155 |  1.00000000 |    0.00001845 |
[<TIMESTAMP>] |         0-14:39:09 |   0TB    0GB 831MB |  851968 /  851968 |  0.99998297 |  1.00000000 |    0.00001703 |
[<TIMESTAMP>] |         0-14:44:19 |   0TB    0GB 831MB |  917504 /  917504 |  0.99998419 |  1.00000000 |    0.00001581 |
[<TIMESTAMP>] |         0-14:49:38 |   0TB    0GB 831MB |  983040 /  983040 |  0.99998524 |  1.00000000 |    0.00001476 |
[<TIMESTAMP>] |         0-14:54:55 |   0TB    0GB 831MB | 1048576 / 1048576 |  0.99998616 |  1.00000000 |    0.00001384 |
[<TIMESTAMP>] -----------------------------------------------------------------------------------------------------------
```
This visualizes the decrease of the Interval Size $L$ for increasing number of simulations.

The computed result is reported with the following format:
``` plaintext
[<TIMESTAMP>] Final Report:
[<TIMESTAMP>] -----------------------------------------------------------------------------------------------------------
[<TIMESTAMP>] |       Elapsed Time |        Used Memory | #Effective Faults | Lower Bound | Upper Bound | Interval Size |
[<TIMESTAMP>] -----------------------------------------------------------------------------------------------------------
[<TIMESTAMP>] |         0-14:54:55 |   0TB    0GB 831MB | 1048576 / 1048576 |  0.99998616 |  1.00000000 |    0.00001384 |
[<TIMESTAMP>] -----------------------------------------------------------------------------------------------------------
[<TIMESTAMP>] Evaluation done in 53695.380127 seconds.
```
These log-entries repeat the header and the last line of the simulation-progress for better readability.
The confidence interval for `aes-unprotected/02-experiments/sa0-p2e007/all-cells` is computed as (0.99998616, 1.00000000).

> [!NOTE]
> Currently, we recompute the results using the new configuration version.
> These computations follow an improved report format, which is in line with [PROLEAD](https://github.com/ChairImpSec/PROLEAD)'s logging to increase uniformity.
> After the computation has completed, they will be added.

> [!NOTE]
> FIESTA was submitted as artifact to CHES2025.
> To keep our changes since the initial artifact submission transparent, we have tagged the state initially submitted with `fiesta-initial`.
> This applies to both repositories, [FIESTA](https://github.com/ChairImpSec/FIESTA) and [PROLEAD](https://github.com/ChairImpSec/PROLEAD).
> An extended documentation for the initial state can be found in the legacy version of the [README.md](legacy/README.md).
