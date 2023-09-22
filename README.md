# OpenAWSEM
## An implementation of the AWSEM coarse-grained protein folding forcefield in OpenMM

The OpenAWSEM code is currently being tested. Use at your own risk. And let us know what you find. :-)


## Installation
* Clone openawsem repository
```
git clone https://github.com/npschafer/openawsem.git
```
* Download and install STRIDE and put it in your PATH: http://webclu.bio.wzw.tum.de/stride/
* Download and install psiblast and put it in your PATH: ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ or using ```conda install -c bioconda blast``` to install
* Download pdb_seqres.txt and put it in the cloned openawsem repository location
```
wget ftp://ftp.wwpdb.org/pub/pdb/derived_data/pdb_seqres.txt
```
* Install conda or miniconda: https://conda.io/en/latest/miniconda.html
* Create an openmm environment that includes the necessary Python packages.
```
conda create -n openmm python=3.6 biopython matplotlib numpy pandas 
```
* Set OPENAWSEM_LOCATION environment variable (the location where you cloned this Github repository).
```
export OPENAWSEM_LOCATION='/YOUR/OPENAWSEM/DIRECTORY/'
```
* Activate the openmm environment.
```
source activate openmm
```
* Install additional python packages
```
conda install -c omnia -c conda-forge openmm pdbfixer mdtraj 
```

## Example
Simulate Phage 434 repressor amino terminal domain (1r69)

* Activate the openmm environment.
```
source activate openmm
```
* Setup simulation folder:
```
python YOUR_OPENAWSEM_LOCATION/mm_create_project.py 1r69 --frag
```
* Or if you already have 1r69.pdb:
```
python YOUR_OPENAWSEM_LOCATION/mm_create_project.py PATH_TO_YOUR_PDB/1r69.pdb --frag
```
* Run the simulation:
```
python mm_run.py 1r69 --platform CPU --steps 1e5 --tempStart 800 --tempEnd 200 -f forces_setup.py
```
* Note:

forces_setup.py controls which force(energy) term will be included in the simulation. 

* Compute energy and Q:
```
python mm_analysis.py 1r69 > energy.dat
```

* Note 2:
If you dont have GPU avaliable, you might want to consider using http://awsem-md.org. For small proteins, the LAMMPS version could be faster than openAWSEM.  

* Note 3:
Due to the size limitation, the data for the paper OpenAWSEM with Open3SPN2: a fast, flexible, and accessible framework for large-scale coarse-grained biomolecular simulations is stored in https://app.globus.org/file-manager?origin_id=b4cef8ce-7773-4016-8513-829f388f7986&origin_path=%2FopenAWSEM_data%2F

## Citation
Lu, W., Bueno, C., Schafer, N. P., Moller, J., Jin, S., Chen, X., ... & Wolynes, P. G. (2021). OpenAWSEM with Open3SPN2: A fast, flexible, and accessible framework for large-scale coarse-grained biomolecular simulations. PLoS computational biology, 17(2), e1008308. https://doi.org/10.1371/journal.pcbi.1008308
