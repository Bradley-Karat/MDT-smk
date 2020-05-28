# Snakemake workflow for using the Microstructure Diffusion Toolbox (MDT)
This is a snakemake workflow for using the Microstructure Diffusion Toolbox (MDT - https://mdt-toolbox.readthedocs.io/en/latest_release/index.html). It was designed to run microstrcuture modelling on unfolded hippocampal diffusion data (more about unfolding the hippocampus by @jordandekraker at https://github.com/jordandekraker/HippUnfolding). 

## Authors
* Bradley Karat (@Bradley-Karat)

Usage
-----

#### **Install Snakemake**
Install snakemake using [pip](https://snakemake.readthedocs.io/en/stable/getting_started/installation.html#installation-via-pip):

  ```                                                                                           pip install snakemake```

(note snakemake has non-python dependencies, such that the pip based installation has a limited functionality if those dependencies are not manually installed in addition)

Install snakemake using [Conda](https://conda.io/projects/conda/en/latest/user-guide/install/index.html):

   ```conda install -c conda-forge mamba                                                                                          ```

  ```conda activate snakemake                                                                                                    ```

For more details about installation [read the snakemake documentation](https://snakemake.readthedocs.io/en/stable/).


