# 2019-Feb-25_jupyter

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/johnsolk/2019-Feb-25_jupyter/master)

# Intro

[Jupyter](https://jupyter.org/) notebooks started as the IPython (interactive Python) notebook. This is why the file extension of the notebooks is `.ipynb`. Now, you - as the user - can use the re-branded Jupyter notebook for Python coding in addition to [many other languages, including R](https://jupyter.org/try).

The cool thing about Jupyter notebooks is you can see the output rendered directly below the code. This is different than other interactive developer environments (IDE) where the code is stored in a separate file and the output is rendered separately.

This comes in handy when running analyses with code because you can see and save output and plots and keep track of tweaking parameters, showing your flow of logic and process of arriving at an analytical decision, just like you would with a lab notebook and lab troubleshooting lab results.

The stumbling blocks for using and disseminating jupyter notebooks to colleagues/customers are large input datasets, jupyter is memory hungry and will take up all of your system processes if left to its own devices, installing jupyter, running the notebook, and installing required dependencies, version control.

GitHub will render .ipynb files, so you can see the output and the lines of code. The output can be made into an .html file or an .pdf for easy formatting as supplementary materials. There are several packages, such as binder and nbviewer that will make the notebook live for interactive use. The notebooks have to be small, though - with small input datasets. 

Motivation:
* Keep code and output rendered in a single document.
* Spatial tutorial with scanpy
* Juan's dataset in ipynb
* Roadmap tour guides - make ipynb files available in GitHub repo? (supplemental files to link out to if people want; they will still be written as normal on the website)
* Interact with data files: 
    * [On bespin or locally, like compbio does](https://10xtech.atlassian.net/wiki/spaces/COMPBIO/pages/565413235/Jupyter+Running+jupyterlab+on+bespin1+2)
    * [Leah also started SFO page](https://10xtech.atlassian.net/wiki/spaces/SFO/pages/579044637/SFO+Jupyter+notebook+setup+for+tutorials)

# Objectives:

Today, we will walk through steps on your own computer how to:

* Install jupyter notebook
* Start a new notebook, save and export
* Load someone else's notebook file
* Work with an existing notebook file in the cloud (binder demo)

# Binder





# (OPTIONAL) Install jupyter notebook locally

Use Miniconda, a smaller version of conda (doesn't install EVERYTHING, just basic dependencies).

```
wget -O ~/miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
bash ~/miniconda.sh -b -p $HOME/miniconda
source ~/miniconda/bin/activate
```
Create environment:
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
Install:
```
pip install numpy scipy pandas matplotlib seaborn SpatialDE louvain python-igraph
```
