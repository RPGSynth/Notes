# Setting Up a Polyglot Notebook in VS Code with Python and R Kernels

This guide will help you set up a Polyglot Notebook in Visual Studio Code (VS Code) using the Polyglot Notebooks extension, enabling you to use both Python and R kernels seamlessly in the same notebook. This setup allows you to combine the power of Python's data analysis and R's statistical tools in a single environment.

## Step 1: Install VS Code and Polyglot Notebooks Extension
1. **Install Visual Studio Code**: If you don't already have VS Code, download and install it from [here](https://code.visualstudio.com/).
2. **Install the Polyglot Notebooks Extension**:
   - Open VS Code and go to the Extensions view (`Ctrl+Shift+X`).
   - Search for **Polyglot Notebooks** (previously called .NET Interactive Notebooks) and install it.

This extension enables you to work with multiple languages, including Python, R, and others, within a single notebook.

## Step 2: Set Up Python Kernel
1. **Install Miniconda/Anaconda**: If you haven't installed Miniconda or Anaconda, you can download and install Miniconda from [here](https://docs.conda.io/en/latest/miniconda.html). This helps in managing Python environments effectively.
2. **Create a Python Environment**:
   - Open your terminal and create a new Conda environment named `phd`:
     ```bash
     conda create --name phd python=3.9
     ```
   - Activate the environment:
     ```bash
     conda activate phd
     ```
3. **Install Jupyter and IPython Kernel**:
   - Install Jupyter and `ipykernel` to enable the use of Python in the notebook:
     ```bash
     conda install jupyter ipykernel
     ```
   - Register the kernel with Jupyter:
     ```bash
     python -m ipykernel install --name phd --display-name "Python (phd)"
     ```

## Step 3: Set Up R Kernel
1. **Install R**: You can install R within your Conda environment:
   ```bash
   conda install -c r r-essentials
   ```
   The `r-essentials` package contains R and commonly used R packages, including `IRkernel`.
2. **Install IRkernel in R**:
   - Start an R session by running `R` in your terminal (make sure your Conda environment is active).
   - In the R console, install and register the kernel:
     ```R
     install.packages('IRkernel')
     IRkernel::installspec(user = FALSE)
     ```

## Step 4: Verify Kernel Installation
To ensure that both the Python and R kernels are properly installed, you can run the following command:
```bash
jupyter kernelspec list
```
You should see entries for both `Python (phd)` and `ir` in the output.

## Step 5: Create a New Polyglot Notebook in VS Code
1. **Create a New Notebook**:
   - Open VS Code and press `Ctrl+Shift+P` to open the Command Palette.
   - Type `Polyglot Notebook: Create New Blank Notebook` and select it.
2. **Add Language Cells**:
   - The Polyglot Notebooks extension allows you to switch between languages within a single notebook.
   - At the top-right of each cell, you can select which language to use (Python or R).

## Step 6: Sharing Variables Between Python and R
### Using `#!set` to Share Variables
- To share variables between Python and R kernels, you can use the `#!set` directive.
- **Python to R Example**:
  1. **Python Cell**:
     ```python
     data = {'Name': ['Alice', 'Bob', 'Charlie'], 'Age': [25, 30, 35]}
     #!set --name shared_data --value @python:data
     ```
  2. **R Cell**:
     ```r
     shared_data <- .NET$shared_data
     shared_df <- as.data.frame(shared_data)
     print(shared_df)
     ```
- The `#!set` directive shares the Python variable (`data`) and makes it accessible in R.

## Summary
With this setup, you can:
- Seamlessly use both Python and R within the same notebook in VS Code.
- Share variables between Python and R using `#!set`.

This configuration is powerful for data scientists and analysts who need the capabilities of multiple languages in a single environment, enabling more flexible workflows and analysis techniques.

