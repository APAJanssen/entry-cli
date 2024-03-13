Entryway analysis
=================

![Build](https://github.com/HergenrotherLab/entry-cli/workflows/Python%20application/badge.svg)

The eNTRy rules are a series of guidelines that can increase small-molecule
accumulation in gram-negative bacteria. A molecule is likely to accumulate if it
contains few rotatable bonds, low three dimensionality, and an ionizable
nitrogen.

The webapp [entry-way](http://www.entry-way.org) was created to aid in the application of these guidelines
by performing the necessary predictions of physiochemical properties. Although
freely available at entry-way.org, these same calculations can be performed
locally.

**FORKED TO FIX AND IMPLEMENT LOCALLY**

Dependencies
------------

Entryway relies on [OpenBabel](http://openbabel.org) and [RDKit](https://www.rdkit.org/) for handling chemical 
structures and conformer generation and NumPy for globularity calculations. These dependencies are most conveniently 
installed via [Conda](https://conda.io/docs/user-guide/install/index.html). The included `environment.yml` 
file makes this straightforward:

```bash
conda env create -f environment.yml
conda activate entry-cli-env
```

Alternatively, they can be installed individually:

```bash
conda create -n entry-cli python=3.11
pip install rdkit
conda install -c conda-forge openbabel=3.1.1
conda activate entry-cli
```

Running calculations
--------------------

Molecules can only be submitted as SMILES strings for now.

This can be achieved through command line arguments:

```bash
# Ampicillin
python calc_props.py -s "O=C(O)[C@@H]2N3C(=O)[C@@H](NC(=O)[C@@H](c1ccccc1)N)[C@H]3SC2(C)C"

# Deoxynybomycin
python calc_props.py -s "CC(C1=CC(C(C)=CC(N2C)=O)=C2C3=C1N4CO3)=CC4=O"
```

Alternatively, a batch file can be provided that contains several molecules with SMILES and names. Results are reported 
as a csv file. The name of the output file is optional. If no output file is specified, then the base name of the batch
file is used:

```bash
# The following will provide the same result
python calc_props.py -b tests/b-lactams.smi -o tests/b-lactam.csv
python calc_props.py -b tests/b-lactams.smi
```

Citing
------

Please cite the paper on the eNTRy rules:

[Richter, M. F.; Drown, B. S.; Riley, A. P.; Garcia, A.; Shirai, T.; Svec, R. L.; Hergenrother, P. J. *Nature* __2017__,
*545*, 299-304.](https://doi.org/10.1038/nature22308)
