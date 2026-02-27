# SpaceGFN

This repository contains the implementation code for our research paper, [Designing the Haystack: 
Programmable Chemical Space for Generative Drug Discovery]()

## Introduction

Here we present SpaceGFN, a next-generation molecular generation framework centered on autonomous chemical space design, which integrates Discovery and Editing modes. In the Discovery mode, SpaceGFN enables DIY construction of chemical spaces.In the Editing mode, we systematically incorporate molecular editing into generative AI, establishing the reaction template dataset Edit Rule V1, and validate its effectiveness and generality across 96 drug targets in large-scale optimization tasks. Collectively, SpaceGFN establishes a new balance between creativity and feasibility, providing a paradigm for the deep integration of generative AI, chemical synthesis, and drug discovery, with the potential to systematically expand the accessible chemical space and accelerate the discovery of next-generation therapeutics.

![GUE](figures/spacegfn.png)

## Installation

Follow these steps to set up the environment and install all dependencies for this project.

```bash
conda create --name spacegfn python==3.12.9
conda activate spacegfn
bash install_dependencies.sh
```

## Data

SpaceGFN provides two operational modes: Discovery and Editing, which are designed for de novo molecular generation and molecular optimization, respectively.

In Discovery mode, we provide [example data processing workflows](dataprocess/Discovery%20mode.ipynb).

Building block libraries for constructing different chemical spaces can be sourced as follows:  
- **Synthetic space**: [Enamine](https://enamine.net/)  
- **Pseudo-Natural Product space**: [Waldmann et al.](https://www.nature.com/articles/nchem.1506)  
- **Evo space**: [HMDB](https://hmdb.ca/)  

We also include the reaction template dataset integrated in the previous SynGFN project as the [standard synthetic reaction dataset](dataprocess/raw/discovery/Synthetic/template_syngfn.csv).  
For Evo space, the reaction dataset can be obtained from [RetroBioCat](https://www.nature.com/articles/s41929-020-00556-z) (note: it provides retrosynthetic reaction templates). 

Users can also prepare their own building block libraries and reaction templates to design chemical spaces of interest. SpaceGFN provides a framework for users to construct and explore their own chemical spaces.

In Editing mode, we currently provide [examples](dataprocess/raw/editing/template_edit_rule_v1.csv) derived from our Edit Rule V1 dataset (a curated molecular editing reaction set), as well as [corresponding data processing examples](dataprocess/Editing%20mode.ipynb).
The Edit Rule database will be continuously updated and released to the public when appropriate.


## Usage

To train a SpaceGFN model, simply run

```bash
python main.py user.logdir.root=<path/to/log/files/>
```

Alternatively, you can create a user configuration file in `config/user/<username>.yaml` specifying a `logdir.root` and run

```bash
python main.py user=<username>
```

SpaceGFN uses [Hydra](https://hydra.cc/docs/intro/) to handle configuration files. The [main.yaml](config/main.yaml) file provides a set of basic adjustable parameters. 


## Updates from SynGFN

Compared to the original [SynGFN](https://github.com/ChemloverYuchen/SynGFN), SpaceGFN introduces several key updates:

1. **Customizable reaction steps**  
   Users can now specify the number of reaction steps by adjusting the `reaction_step` parameter in [main.yaml](config/main.yaml).

2. **Two operational modes: Discovery and Editing**  
   These modes support both *de novo* molecular design and molecular optimization.  
   In Discovery mode, we provide a flexible framework for users to construct their own DIY chemical spaces.

3. **Efficiency enhancements**  
   Several improvements have been made to boost computational efficiency.  
   For example, the reward feedback system now supports [UniDock](https://github.com/dptech-corp/Uni-Dock) as a general docking-based scoring module.

## Contact
If you have any question, please feel free to email us (yuchenzhu@zju.edu.cn).