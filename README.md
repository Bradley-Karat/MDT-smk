# Snakemake workflow for using the Microstructure Diffusion Toolbox (MDT)
This is a snakemake workflow for using the [Microstructure Diffusion Toolbox (MDT)](https://mdt-toolbox.readthedocs.io/en/latest_release/index.html). This workflow was designed to run microstrcuture modelling on left and right hemisphere unfolded hippocampal diffusion data (more about unfolding the hippocampus by @jordandekraker at https://github.com/jordandekraker/HippUnfolding). This workflow makes use of a [bids app wrapper](https://github.com/khanlab/mdt-bids) for running MDT.

## Authors
* Bradley Karat (@Bradley-Karat)

Usage
-----

#### 1. **Install Snakemake**
* Install snakemake using [pip](https://snakemake.readthedocs.io/en/stable/getting_started/installation.html#installation-via-pip):

 ```python
   pip install snakemake
  ```

(note snakemake has non-python dependencies, such that the pip based installation has a limited functionality if those dependencies are not manually installed in addition)

* Install snakemake using [Conda](https://conda.io/projects/conda/en/latest/user-guide/install/index.html):

```python
 conda install -c conda-forge mamba    
  ```
  
   
```python
 conda activate snakemake  
  ```

For more details about installation [read the snakemake documentation](https://snakemake.readthedocs.io/en/stable/).


#### 2. **Configuring the Workflow**
Configure the workflow for your specific needs by adjusting the `config.yml` and `participants.tsv` files in the `Config` folder. Please note that at the top of the `snakefile` there is a variable called `model`. Replace the value for `model` with the microstructure model you wish to use. In our example we used the Neurite Orientation Density and Dispersion Imaging model (NODDI).


#### 3. **Testing with a Dry-run**
Test your configuration by performing a dry-run via
```python
 snakemake -np
```

Note that you may not wish to run all the rules in the snakefile. For example, you may already have a mask created and do not wish to create another one through MDT. In that case, specify the rule you would like to run. An example for only running the model fitting is:
```python
 snakemake -np results/{subject}_{hemi}/NODDI
```

To visualize the workflow you can use the following command to get a directed acyclic graph (DAG) pdf of jobs where the edges represent dependencies:
```python
 snakemake --dag | dot -Tpdf > dag.pdf
 ```

#### 4. **Executing on Graham (compute canada)**
The workflow can be executed by using the `cc-slurm` profile or by executing an interactive job. 
 
 
1. The **cc-slurm** profile sets up default options for running on compute canada. More information on cc-slurm can be found from the Khan lab [here](https://github.com/khanlab/cc-slurm). 
 
Install `cookiecutter` using:
```python
  pip install cookiecutter --user
```
(make sure you are have python 3 installed)

The next step is to deploy the profile. To do this run the following on grahams login node:
```python
  cookiecutter gh:khanlab/cc-slurm -o ~/.config/snakemake -f
```
Snakemake can then be ran with:
```python
  snakemake --profile cc-slurm ...
```

2. Submitting an **interactive** job by executing the workflow locally:
```python
 salloc --time=8:00:00 --gres=gpu:t4:1 --cpus-per-task=8 --ntasks=1 --mem=32000 --account=CC_acct srun snakemake --use-      singularity --cores 8 --resources gpus=1 mem_mb=32000 
```

#### 5. **Viewing Results**
After successful completion you can view your results using viewers such as `fsleyes` or if you have installed MDT locally you can use their GUI or command-line control `mdt-view-maps <your-model-choice>`. 
