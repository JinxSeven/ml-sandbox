# ML Environment Setup

## Overview

Setting up a clean environment for ML work using MiniConda.
These are the steps to usually follow from scratch — installing, creating an environment, adding libraries, and getting Jupyter working properly.

## Installing MiniConda

### On Windows

* First, grab the Miniconda installer for Windows (64-bit).
* While installing, make sure to **add Conda to PATH** (so I can use it from any terminal).
* I also choose **install for all users** — makes it easier later.
* Once it’s done, check if it’s installed properly:

  ```cmd
  conda --version
  ```

  If this shows a version number, it’s fine.

### On macOS or Linux

* download the installer script, then run:

  ```bash
  chmod +x Miniconda3-latest.sh
  ./Miniconda3-latest.sh
  ```
* Quick check:

  ```bash
  conda --version
  ```

## Creating a Conda Environment

### Option 1 – Inside Project Folder

```bash
cd /path/to/project
conda create -p ./ml-env python=3.9
conda activate ./ml-env
```

The `-p` flag means I’m literally telling Conda *“make the environment right here.”*

### Option 2 – Default Conda Location

```bash
conda create -n ml-env python=3.9
conda activate ml-env
```

Here, `-n` just gives the environment a name. Conda keeps it in its default folder.

### Installing Packages

Right after activating the env, Install ML go-to stack:

```bash
# basic stuff
conda install numpy pandas matplotlib scikit-learn

# deep learning libs
conda install tensorflow keras pytorch torchvision torchaudio

# Jupyter + tools
conda install jupyter notebook jupyterlab ipykernel

# extras (if not on conda)
pip install opencv-python seaborn plotly
```

If want to save the setup:

```bash
pip freeze > requirements.txt
```

And to bring it back later:

```bash
pip install -r requirements.txt
```

## Setting Up Jupyter Notebook

### Create Config File

Generate a config file first:

```bash
jupyter notebook --generate-config
```

It usually appears in:

* **Windows:** `C:\Users\<username>\.jupyter\`
* **Linux/Mac:** `~/.jupyter/`

### Edit It

Open `jupyter_notebook_config.py` and scroll to the bottom, then add:

```python
c.ServerApp.root_dir = '/path/to/workspace'
```

## Using the Environment

To start working:

```bash
conda activate ml-env
jupyter notebook
```

or if want a specific folder:

```bash
jupyter notebook --notebook-dir=/path/to/workspace
```

To make sure Jupyter shows the right environment as a kernel:

```bash
python -m ipykernel install --user --name=ml-env --display-name="ML Environment"
```

## Common Commands I Keep Forgetting

### Conda Basics

| Action            | Command                        |
| ----------------- | ------------------------------ |
| List envs         | `conda env list`               |
| Activate env      | `conda activate env_name`      |
| Deactivate env    | `conda deactivate`             |
| Delete env        | `conda env remove -n env_name` |
| Update conda      | `conda update conda`           |
| List packages     | `conda list`                   |

Flags often used:
`-n` = environment name
`-p` = path to env
`-y` = auto confirm
`-c` = specific channel


## Conda Cheat Sheet

| Task                   | Command                               |
| ---------------------- | ------------------------------------- |
| Make new env (by name) | `conda create -n myenv python=3.9`    |
| Make env (by path)     | `conda create -p ./env python=3.9`    |
| Activate env           | `conda activate myenv`                |
| Exit env               | `conda deactivate`                    |
| Install package        | `conda install numpy`                 |
| Remove package         | `conda remove numpy`                  |
| List all envs          | `conda env list`                      |
| Export env             | `conda env export > environment.yml`  |
| Recreate env           | `conda env create -f environment.yml` |
| Clean up unused stuff  | `conda clean --all`                   |

## Jupyter Notebook Cheat Sheet

| Action              | Command / Shortcut                                                        |
| ------------------- | ------------------------------------------------------------------------- |
| Start notebook      | `jupyter notebook`                                                        |
| Start JupyterLab    | `jupyter lab`                                                             |
| Set directory       | `jupyter notebook --notebook-dir=/path/to/folder`                         |
| Generate config     | `jupyter notebook --generate-config`                                      |
| Add kernel          | `python -m ipykernel install --user --name=myenv --display-name="My Env"` |
| List kernels        | `jupyter kernelspec list`                                                 |
| Remove kernel       | `jupyter kernelspec remove myenv`                                         |
| Stop server         | `Ctrl + C`                                                                |
| Run cell            | `Shift + Enter`                                                           |
| Run + add below     | `Alt + Enter`                                                             |
| Interrupt kernel    | press `I, I`                                                              |
| Restart kernel      | press `0, 0`                                                              |
| Toggle command/edit | `Esc` / `Enter`                                                           |
| Save notebook       | `Ctrl + S`                                                                |
| Rename notebook     | `File → Rename`                                                           |
| Export notebook     | `File → Download as → HTML/PDF/Script`                                    |
