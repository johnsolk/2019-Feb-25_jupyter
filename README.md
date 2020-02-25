# 2020-Feb-25_jupyter

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/johnsolk/2020-Feb-25_jupyter/master)

# Intro

[Jupyter](https://jupyter.org/) notebooks started as IPython (interactive Python) notebook. This is why the file extension of the notebooks is `.ipynb`. You can use Jupyter notebooks for Python coding in addition to [many other languages, including R](https://jupyter.org/try).

Jupyter notebooks allow you to see and save output rendered directly below the code. This is different than other interactive developer environments (IDE) where the code is stored in a separate file and the output is rendered separately.

Motivation:
* Save analyses, keep code and output rendered in a single document
* Tutorials

# Objectives:

Today, we will:

* Load an existing notebook file
* Export
* Start a new notebook file
* (Optional) R jupyter notebook, R Studio with mybinder
* (Optional) install jupyter notebook locally

# Load an existing notebook file

1. Click on the [mybinder](https://mybinder.org/) link below:

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/johnsolk/2020-Feb-25_jupyter/master)

Click on the 'Build logs' to show what is being installed.

2. Open Terminal to install scanpy:
```
git clone https://github.com/theislab/scanpy.git
cd scanpy
pip install --user .
pip install spatialde
```

3. Open notebook file. This was copied from the [Analysis and visualization of spatial transcriptomics data](https://nbviewer.ipython.org/github/giovp/scanpy-tutorials/blob/spatial/analysis-visualization-spatial.ipynb) by the [scanpy](https://scanpy.readthedocs.io/en/stable/) folks.
4. Run commands.

# Export

Click on the 'File' menu, select 'Download as'. There are several options. I use .pdf, .html, and .ipynb. These are the easiest to share with other people. Only the .ipynb will be executable for others.

# Start a new notebook file

1. Start a new Python 3 notebook file.

2. Copy/paste:

These are some plots/commands from this [tutorial](https://colab.research.google.com/github/pachterlab/kallistobustools/blob/master/notebooks/kb_intro_1_python.ipynb).

```
from scipy.io import mmread
from sklearn.decomposition import TruncatedSVD
import matplotlib.pyplot as plt
import numpy as np
```
If you try to run the above, you can't because `sklearn` is not intalled.

To install it, run this:
```
!pip install sklearn
```
Download from [5k Peripheral blood mononuclear cells (PBMCs) from a healthy donor with cell surface proteins (Next GEM)](https://support.10xgenomics.com/single-cell-gene-expression/datasets/3.1.0/5k_pbmc_protein_v3_nextgem):
```
!wget http://cf.10xgenomics.com/samples/cell-exp/3.1.0/5k_pbmc_protein_v3_nextgem/5k_pbmc_protein_v3_nextgem_filtered_feature_bc_matrix.tar.gz
```
Take a look:
```
!ls -lah
```
Annotate a cell with markdown (change from 'code' to 'markdown' with the pulldown menu) :
```
Who is [jovyan](https://github.com/jupyter/docker-stacks/issues/358)?
```
Decompress:
```
!tar -xvzf 5k_pbmc_protein_v3_nextgem_filtered_feature_bc_matrix.tar.gz
!gunzip filtered_feature_bc_matrix/*.gz
```
Import:
```
mtx = mmread('filtered_feature_bc_matrix/matrix.mtx')
```

SVD on filtered:
```
# Perform Singular Value Decomposition
tsvd = TruncatedSVD(n_components=2)
tsvd.fit(mtx_filtered)
X_filtered = tsvd.transform(mtx_filtered)
```
Plot 2D PCA projection:
```
fig, ax = plt.subplots(figsize=(10, 7))
ax.scatter(X[:,0], X[:,1], alpha=0.5, c="green")
plt.axis('off')
plt.show()
```
Create a plot genes detected vs. UMI counts:
```
fig, ax = plt.subplots(figsize=(10, 7))
ax.scatter(np.asarray(mtx.sum(axis=1))[:,0], np.asarray(np.sum(mtx>0, axis=1))[:,0], color="green", alpha=0.01)
ax.set_xlabel("UMI Counts")
ax.set_ylabel("Genes Detected")
ax.set_xscale('log')
ax.set_yscale('log', nonposy='clip')
ax.set_xlim((0.5, 4500))
ax.set_ylim((0.5,2000))
plt.show()
```
Example [violin plots from seaborn library](https://seaborn.pydata.org/examples/grouped_violinplots.html):
```
import seaborn as sns
sns.set(style="whitegrid", palette="pastel", color_codes=True)

# Load the example tips dataset
tips = sns.load_dataset("tips")

# Draw a nested violinplot and split the violins for easier comparison
sns.violinplot(x="day", y="total_bill", hue="smoker",
               split=True, inner="quart",
               palette={"Yes": "y", "No": "b"},
               data=tips)
sns.despine(left=True)
```

# (Optional) R jupyter notebook & R Studio with mybinder

### R jupyter notebook

Jupyter+R: [![Binder](http://mybinder.org/badge_logo.svg)](http://mybinder.org/v2/gh/binder-examples/r/master?filepath=index.ipynb)

[Examples with R](https://github.com/binder-examples/r)

### R Studio with mybinder

Running [RStudio](https://github.com/binder-examples/dockerfile-rstudio) through binder:

[![Binder](http://mybinder.org/badge.svg)](http://mybinder.org/v2/gh/binder-examples/dockerfile-rstudio/master)

Install Biocondutor and DropletUtils library:

```
if (!requireNamespace("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
BiocManager::install("DropletUtils")
library("DropletUtils")
```
Download:
```
wget http://cf.10xgenomics.com/samples/cell-exp/3.1.0/5k_pbmc_protein_v3_nextgem/5k_pbmc_protein_v3_nextgem_molecule_info.h5
```
Import:
```
mol.info.file <- "5k_pbmc_protein_v3_nextgem_molecule_info.h5"
molinfo <- read10xMolInfo(mol.info.file)
molinfo
```

Click [here for instructions on how to run an R Jupyter notebook with binder](https://github.com/binder-examples/r).

# (OPTIONAL) install jupyter notebook locally

Install Miniconda, a smaller version of conda. (doesn't install everything, just basic dependencies)

```
wget -O ~/miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
bash ~/miniconda.sh -b -p $HOME/miniconda
source ~/miniconda/bin/activate
```
Create [environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html):
```
conda create -y -n py3.jupyter jupyter
```
Activate:
```
conda activate py3.jupyter
```
Install scanpy:
```
git clone https://github.com/theislab/scanpy.git
cd scanpy
pip install --user .
```
Add to path:
```
export PATH=/home/ljcohen/.local/bin:$PATH
```
Install dependencies:
```
pip install numpy scipy pandas matplotlib seaborn SpatialDE louvain python-igraph
```
