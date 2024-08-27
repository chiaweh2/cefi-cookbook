# How to Setup Analyses Ready Environment

This page is designed to guide you in setting up a local computational environment, which will enable you to perform the analyses demonstrated in this cookbook locally. However, if you're using the complimentary and lightweight cloud computing services provided by Binder or Google Colab, the environment setup is already taken care of for you in the cloud.

(conda-setup)=
## Steps Summary
- Install and initialize Conda (only necessary if Conda isn't already installed on your system).
- Create and activate a new "environment", utilizing the environment.yml file.
- Begin coding in Python or R within this environment. 

Remember, each step is crucial to ensure the correct setup and functioning of your Conda environment.

```{warning}
**Command Line Interface (CLI)** The following steps need to be performed in Command Line Interface. For Windows, search for `cmd` in the search bar for the Command Prompt app. For macOS and Linux, terminal app is the preinstalled app for CLI.
```
```{tips}
There are many useful setup intruction out there. The intruction here is unique in offering both R and Python setup for running the example shown in this entire cookbook. For other useful info related to setup other analyses ready material, we recommand [IOOS CodeLab](https://ioos.github.io/ioos_code_lab/content/ioos_installation_conda.html)
```


### Install and Initialize Conda
The following intruction will install "miniconda" which is the light-weight version of Conda system on a **Linux machine**.
For other system (macOS or Windows) please checkout the [official miniconda installation](https://docs.anaconda.com/miniconda/#quick-command-line-install)
`````{tab-set}
````{tab-item} Linux/MacOS
```
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
```
After the installation, we need to initialize the Conda
```
~/miniconda3/bin/conda init bash
``` 
````

````{tab-item} Windows
```
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe -o miniconda.exe
start /wait "" miniconda.exe /S
del miniconda.exe
```
After installing, open the “Anaconda Prompt (miniconda3)” program to use Miniconda3. For the Powershell version, use “Anaconda Powershell Prompt (miniconda3)”.
````
`````



````{dropdown} Why Conda? (optional read)
Conda is a software package management system that emphasizes on 'version management'. The purpose of this 'version management' is to ensure that in your local computational environment, you can maintain multiple versions of the same software, tailored to the requirements of the various projects you are working on.

```{important}
**Why do I need version control?** Imagine you've started a project, let's call it Project A, and you're using version 1 of a particular software for your coding, taking full advantage of the benefits of open source. Suddenly, there's an update, and your software is now at version 2. However, this update causes your code for Project A to stop working. This is where Conda's version control comes in handy. It ensures that you can maintain both versions of the software. This way, you can thoroughly test Project A with the new software version before deciding to update it while still have the working Project A with version 1 existing on your local system.
```
Conda manages versions by creating separate 'conda environments'. Within each 'conda environment', users have the freedom to choose which software and what version to install. The installed software and its specific version are confined to that particular 'conda environment'. Users can activate a specific 'conda environment' to utilize the desired software and version.

```{tip}
A useful strategy when using the Conda system is to set up distinct environments for each project. This approach offers the flexibility to install specific software exclusively for a particular project. As a result, the software installed for one project won't interfere with the software used in another project.
This way, you can maintain the integrity and functionality of each project independently. 😊
```
````

(conda-create)=
### Create and Activate Conda Environment
1. Download the `environment.yml` file from the [CEFI-Cookbook repository on GitHub](https://github.com/NOAA-CEFI-Portal/cefi-cookbook)
    `````{tab-set}
    ````{tab-item} Python
    ```
    wget https://raw.githubusercontent.com/NOAA-CEFI-Portal/cefi-cookbook/main/environment.yml
    ```
    ````

    ````{tab-item} R
    ```
    wget https://raw.githubusercontent.com/NOAA-CEFI-Portal/cefi-cookbook/r-setup/environment.yml
    ```
    ````
    `````


    ```````{dropdown} If you do not have wget (trouble shooting read)
    ``````{admonition} Method 1 (Manuel download)
    - For Python, go to GitHub page which contain the Python version of [environment.yml file](https://github.com/NOAA-CEFI-Portal/cefi-cookbook/blob/main/environment.yml)
    - For R, go to GitHub page which contain the R version of [environment.yml file](https://github.com/NOAA-CEFI-Portal/cefi-cookbook/blob/r-setup/environment.yml)

    and download the `environment.yml` file. On the top right corner of the code space, there is a "download raw file" button.
    `````{image} ../images/download_yml.png
    :alt: environment.yml file download button location on GitHub
    :class: bg-primary mb-1
    :width: 90%
    :align: center
    `````
    ``````

    ``````{admonition} Method 2 (Manuel create the environment.yml)
    Copy the following text and paste in any of the text editor, and save the file that is named as `environment.yml`
    `````{tab-set}
    ````{tab-item} Python
    ```
    name: cefi-cookbook
    channels:
    - conda-forge
    dependencies:
    - python=3.10
    - jupyterlab
    - dask
    - netcdf4
    - erddapy=1.2.1
    - scipy
    - xarray
    - matplotlib
    - folium
    - bokeh
    - plotly
    ```
    ````

    ````{tab-item} R
    ```
    name: cefi-cookbook-r
    channels:
    - conda-forge
    dependencies:
    - jupyterlab
    - r-irkernel
    - r-rerddap
    - r-ncdf4
    - pip
    - pip:
        - nbgitpuller
    ```
    ````
    `````
    ``````
    ````````

2. Create the "conda environment"
    ```
    conda env create -f environment.yml
    ```

3. Activate the conda environemnt
    `````{tab-set}
    ````{tab-item} Python
    ```
    conda activate cefi-cookbook
    ```
    ````

    ````{tab-item} R
    ```
    conda activate cefi-cookbook-r
    ```
    ````
    `````

### Start Coding in Python or R
Now that you have install the necessary software and packages.
You can start coding in Python or R using your prefered text editor.
- To execute the Python or R scripts
    `````{tab-set}
    ````{tab-item} Python
    ```
    python script.py
    ```
    ````
    ````{tab-item} R
    ```
    Rscript script.R
    ```
    ````
    `````

- To enter the interactive coding mode (line-by-line code execution) for Python or R
    `````{tab-set}
    ````{tab-item} Python
    ```
    python
    ```
    ````
    ````{tab-item} R
    ```
    R
    ```
    ````
    `````




