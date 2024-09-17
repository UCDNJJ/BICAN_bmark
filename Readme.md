
### Summary

Here we present benchmark datasets utilized in the BICAN Mapping Task Force to evaluation cell type annotation methods. This repository extends previous work by the Allen Institute on a [bmark](https://github.com/AllenInstitute/bmark) GitHub repo.

In particular we:

1. Provide a reproducible and transparent generation of benchmark datasets covering diverse cell type annotation scenarios.
2. Provide an easy to understand summary through data cards for each benchmark dataset,
3. Define a supervised classification task and performance metrics to evaluate cell type annotation methods.
4. Report evaluation for each cell type annotation method in a way that permits a fair comparisons across methods.

This effort attempts to formulate a **decentralized** approach to **continuous** benchmarking.
 - Individualcomputational groups are only responsible for tuning and submitting results for their own methods.
 - New methods can be added at any time, but results can be compared in a fair manner to previously submitted methods.
 - All reporting (data + model cards) is intended to be succinct yet accessible to a non-expert.

We hope that this format can prevent misrepresentation of methods, have archival value through a minimal but necessary level of reproducibility, and provide the basis for informed decision making regarding choice of cell type annotation methods for specific tasks.

#### References

[1] [2021 Luecken et al.](https://openreview.net/forum?id=gN35BGa1Rt) <br>
[2] [2019 Mitchell et al.](https://arxiv.org/pdf/1810.03993.pdf) <br>
[3] [2021 Gebru et al.](https://arxiv.org/pdf/1803.09010.pdf) <br>

----

### BICAN Mapping Task Force benchmark datasets
 
Priority | Data set | Characteristics | Status | Download
1.1 | HMBA Basal Ganglia | Donor effects, multi-species | Ready | S3 Link TBD
1.2 | Siletti el al. Human Brain | Donor effects | Ready | S3 Link TBD


### Environment
```bash
conda create -n bmark
conda activate bmark
conda install python==3.8
conda install seaborn scikit-learn statsmodels numba pytables
conda install -c conda-forge python-igraph leidenalg
pip install scanpy
pip install gdown timebudget autopep8 toml sklearn
pip install jupyterlab
pip install -e .
```

 ### Pilot dataset
```bash
# Download
source scripts/download_scripts.sh
get_bmark_pilot /allen/programs/celltypes/workgroups/mousecelltypes/benchmarking/dat/pilot/

# Processing raw data with codes in ./scripts
python -m make_pilot_h5ad --data_path /allen/programs/celltypes/workgroups/mousecelltypes/benchmarking/dat/pilot --min_sample_thr 20 --write_h5ad 1
python -m make_pilot_markers --data_path /allen/programs/celltypes/workgroups/mousecelltypes/benchmarking/dat/pilot --write_csv 1
```

### Config
Create a `config.toml` file at the repository root with appropriate `data_dir` path:
```
['pilot']
data_dir = '/allen/programs/celltypes/workgroups/mousecelltypes/benchmarking/dat/pilot/'
```
 - `config.toml` is accessed through `load_config` in `bmark.utils.config`. 
 - Use `config.toml` to include any other hardcoded paths, needed for notebooks/ scripts to work correctly.

 ### Contributors
Rohan Gala, Nelson Johansen, Raymond Sanchez, Kyle Travaglini
