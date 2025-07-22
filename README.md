# Unsupervised Seismic Waveform Classification Tutorial

## Overview

This repository provides a step-by-step tutorial on applying unsupervised machine learning for seismic waveform classification. The goal is to automatically group seismic traces into "seismic facies" based on their shape, which can help interpreters identify geological features like channels, fans, or changes in rock properties.

The tutorial is designed for geoscientists with a foundational to intermediate understanding of Python. It progresses from simple synthetic examples to a real-world 3D seismic dataset, demonstrating the entire workflow in a clear and practical manner.

## Project Structure

This repository contains three main Jupyter Notebooks, each building upon the last:

1.  **`2D_seismicWaveformClassification.ipynb`**: A foundational notebook that introduces the core concepts using a simple 2D synthetic geological model. It's the perfect place to start to understand the basic principles.
2.  **`2.5D_seismicWaveformClassification.ipynb`**: This notebook increases the geological complexity by creating a synthetic 2.5D meandering river channel model and adds random noise to simulate more realistic conditions.
3.  **`3D_seismicWaveformClassification.ipynb`**: The final notebook applies the complete workflow to a real-world 3D seismic dataset (the F3 block), demonstrating how to integrate seismic and horizon data for a practical interpretation task.

## Getting Started

To run these notebooks on your local machine, you will need to set up a Python environment with the necessary libraries. The recommended way to do this is by using `conda` (via Anaconda or Miniconda).

### Prerequisites

-   **Anaconda** or **Miniconda**: If you don't have it installed, you can download it from the [Anaconda website](https://www.anaconda.com/products/distribution).

### Installation Steps

1.  **Clone the Repository**
    Open a terminal or Git Bash and clone this repository to your local machine:
    ```bash
    git clone https://github.com/roderickperez/seismicWaveformClassification.git
    cd seismicWaveformClassification
    ```

2.  **Create and Activate the Conda Environment**
    Use the provided `requirements.txt` file to create a new conda environment with all the necessary libraries. This ensures you have the correct versions and avoids conflicts with your other Python projects.
    ```bash
    # Create a new environment named 'seismicWaveformClassification' with Python 3.11
    conda create --name seismicWaveformClassification python=3.11 -y

    # Activate the new environment
    conda activate seismicWaveformClassification

    # Install the required packages using pip
    pip install -r requirements.txt
    ```

3.  **Launch Jupyter Notebook**
    Once the environment is activated and the packages are installed, you can start Jupyter Notebook:
    ```bash
    jupyter notebook
    ```
    This will open a new tab in your web browser where you can navigate to and open the `.ipynb` files.

## Dataset

-   **2D and 2.5D Notebooks**: The data for these examples is generated synthetically within the notebooks themselves. No external data download is required.

-   **3D Notebook**: This notebook uses the open-source **F3 Block seismic dataset** from the Dutch North Sea. You will need to download this dataset to run the notebook.
    -   **Download Link**: [https://terranubis.com/datainfo/F3-Demo-2023](https://terranubis.com/datainfo/F3-Demo-2023)
    -   **Required Files**: You will need the seismic data (`1_Original_Seismics.sgy`) and the horizon data (`Horizon.csv`).
    -   **IMPORTANT**: After downloading the files, you must update the file paths in the `3D_seismicWaveformClassification.ipynb` notebook to point to the location where you saved them on your computer. Look for the cells defining `segyfile_path` and `hrz_file`.

## Notebook Summaries

### 1. 2D Synthetic Example
This notebook serves as the entry point to the workflow. It covers:
-   Creating a simple 2D geological model with a single, distinct layer using reflection coefficients.
-   Generating a Ricker wavelet and convolving it with the model to create a clean 2D synthetic seismic section.
-   Applying the K-Means clustering algorithm to group the seismic traces.
-   Using the Elbow Method to validate the choice of the number of clusters.
-   Visualizing the results through a seismic facies map and plots of the average waveform for each cluster.

### 2. 5D Synthetic Example
This notebook builds on the 2D case by:
-   Creating a more complex, pseudo-3D geological model of a meandering river channel.
-   Adding random noise to the synthetic seismic data to better simulate real-world conditions.
-   Applying the same K-Means classification workflow to demonstrate its robustness in identifying geological patterns in the presence of noise.
-   Using advanced visualizations, like a three-panel plot, to directly compare the seismic data with the classification results.

### 3. 3D Real Data Example
This is the final and most comprehensive notebook. It demonstrates the application of the workflow on real field data and includes:
-   Loading a 3D seismic cube from a SEGY file using the `segysak` library.
-   Importing and integrating a picked horizon from a CSV file.
-   Performing essential Quality Control (QC) by creating and analyzing horizon maps and inline displays to ensure data is correctly aligned.
-   Extracting waveform snippets from a small window around the picked horizon for every trace in the survey.
-   Running K-Means clustering to classify the waveforms into eight distinct seismic facies.
-   Generating final interpretive products, including a 2D facies map and overlays on seismic sections, to translate the machine learning output into a meaningful geological interpretation.
