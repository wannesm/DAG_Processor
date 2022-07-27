# Energy-efficient execution of irregular directed acyclic graphs

The paper proposes a customized parallel architecture for energy-efficient execution of irregular directed acyclic graphs (DAG) from probabilistic machine learning and sparse linear algebra. A targeted compiler is developed to generate a binary program for the custom processor given an arbitrary DAG.

#### Aim of the experiments
The processor performance reported in the paper are reproduced through SystemVerilog RTL simulation. The processor instructions for the target workloads are generated with the custom compiler, also validating the compilation algorithm.

### This codebase includes the following components:
1) SystemVerilog-based microarchitectural RTL model of the processor (at [./hw/rtl/](https://github.com/nimish15shah/DAG_Processor/tree/main/hw/rtl)) and a testbench (at [./hw/tb/](https://github.com/nimish15shah/DAG_Processor/tree/main/hw/tb)).
2) A Python-based compiler (at [./src/](https://github.com/nimish15shah/DAG_Processor/tree/main/src)).
3) Input DAGs to reproduce the experiments (at [./data/](https://github.com/nimish15shah/DAG_Processor/tree/main/data))

### Dependencies
* Anaconda3: For Linux installation, see https://docs.anaconda.com/anaconda/install/linux/#installation
* Synopsys VCS simulator: Used for SystemVerilog simulation.

### Installation
Run the following commands to clone this repository and setup python dependencies. This script assumes that
```
git clone git@github.com:nimish15shah/DAG_Processor.git
cd DAG_Processor
./install.sh
```
The installation script creates a conda enviornment and install the required python dependencies.

### Runnning experiments
```
./run.sh
```
The script perfroms the following steps:
- The python-based compiler takes as input the DAG benchmarks and generates binary programs for each benchmark. 
- The SystemVerilog testbench reads the binary programs and the data input files generated by the compiler, and executes the RTL simulation (with the proprietary Synopsys VCS simulator) and generates the latency log. 
- Finally the charts are plotted according to the data collected during the compilation and RTL simulations.

**Disk space requirement**: Less than 200MB (not including Anaconda and Synopsys VCS installation).

**Experiments runtime**: 6-8 hours.

### Outputs
The output charts are available at ```./out/plots```.
- The results of fig. 14 of the paper is reproduced in the ```./out/plots/instruction_breakdown.pdf``` file.
- The results of our processor in fig. 15(a) of the paper is reproduced in the ```./out/plots/throughput.pdf``` file. Throughputs of the rest of the platforms are not reproduced in this codebase and are plotted from a fixed table.

Note: The large DAGs ("Large PC") from table 1 are not evaluated in this version of the codebase due to large experimental runtime (>24hours).




