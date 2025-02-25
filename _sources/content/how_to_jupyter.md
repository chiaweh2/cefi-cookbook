# Launch A Local JupyterLab
```{important}
Sometime Binder or Colab just will not work due to the limited capacity and other factors. Setting up the local JupyterLab is the next best solution for running the cookbook content. Setting up the local environment give you the freedom of storing the changes and less waiting time on the computational resources.
```

This page is designed for users who want to setup a local JupyterLab interface. A install of the conda environment from the previous [page](conda-setup) is necessary to launch the JupyterLab interface.

## Steps Summary
- Activate the conda environment
- Launch the JupyterLab (for any project)
- Launch the JupyterLab with cefi-cookbook locally

```{warning}
**Command Line Interface (CLI)** The following steps need to be performed in Command Line Interface. For Windows, search for `cmd` in the search bar for the Command Prompt app. For macOS and Linux, terminal app is the preinstalled app for CLI.
```

### Activate the conda environment
The is mentioned in the previous [page](conda-create). To activate the conda environment
`````{tab-set}
````{tab-item} Python
```
conda activate cefi-cookbook-dev
```
````

````{tab-item} R
```
conda activate cefi-cookbook-dev
```
````
`````

### Launch the JupyterLab
After the conda environment is activated,
1. Go to the project top level (assuming the project directory is in my home directory)
    ```
    cd ~/project1/
    ```
2. Launch the JupyterLab (make sure the "space" is between jupyter and lab)
    ```
    jupyter lab
    ```
This will automatically launch the jupyterlab in a browser using the port 8888 if not used by other processes on your local computer.

### Launch the JupyterLab with cefi-cookbook locally
To use the local Jupyterlab to run the cookbook content, please download the entire GitHub repository by pressing the download zip file shown in the image
```{image} ../images/download_cookbook.png
:alt: download entire cookbook from github repo
:class: bg-primary mb-1
:width: 90%
:align: center
```
1. Go to the cookbook download folder (Mac is default to ~/Downloads/)
    ```
    cd ~/Downloads/cefi-cookbook-main/
    ```
2. Launch the JupyterLab (make sure the "space" is between jupyter and lab)
    ```
    jupyter lab
    ```
This will automatically launch the jupyterlab in a browser with the left column showing all the cefi-cookbook-main contents
```{image} ../images/jupyter_left.png
:alt: jupyter lab left column
:class: bg-primary mb-1
:width: 90%
:align: center
```

User can use the mouse to double click on the `content` directory to find any interesting jupyternotebook content with the file name "*.ipynb" and execute or modified the notebook content as needed.





