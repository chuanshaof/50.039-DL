# 50.039-DL

This repository contains the code for the 50.039-DL project.

## Setup

Before running the code, please follow these setup instructions:

1. Run the `setup.sh` script. This script downloads a `checkpoints.zip` file and unzips it into a `checkpoints` folder. You can run the script with the following command:

```bash
./setup.sh
```

Make sure the script is executable. If it's not, you can make it executable with the following command:

```bash
chmod +x setup.sh
```

If the installation fails, you can manually download the `checkpoints.zip` file from [this link](https://storage.googleapis.com/dl-project-checkpoints/checkpoints.zip) and unzip it into a `checkpoints` folder in the root project directory on the same level as notebooks, sota, src folders.

2. Install the required Python dependencies. You can do this with the following command:

```bash
pip install -r requirements.txt
```

This command reads the `requirements.txt` file and installs all the listed packages.

After following these setup instructions, you should be ready to run the code.

## Project Structure

This project is organised into several key directories and files:

- `src/`: This directory contains the models that we developed for this project. Specifically, it includes implementations of U-Net, U-NetR, and SegFormer models from scratch with reference to research papers for the architecture.

- `sota/`: This directory contains state-of-the-art models that we used for comparison with our models. Specifically, it includes an implementation of the TransFuse model.

- `sweeps.ipynb`: This Jupyter notebook contains the code for performing hyperparameter sweeps on our models. We used this notebook to find the best hyperparameters for each model.

- `train.ipynb`: This Jupyter notebook contains the code for training our models. After finding the best hyperparameters for each model, we used this notebook to train each model for 10 epochs.

- `evaluation.ipynb`: This Jupyter notebook contains the code for evaluating our models. After training the models, we used this notebook to compute the Dice score on the test set for each model.

## Evaluation

We evaluated our models using the Dice score metric. This metric provides a measure of the overlap between the predicted and actual segmentations, with a higher score indicating better performance.

We compared the performance of our models with that of the state-of-the-art TransFuse model. This comparison allowed us to assess the effectiveness of our models in relation to existing methods.

## Running the Code

To validate our test results, you can run the `evaluation.ipynb` Jupyter notebook. This notebook loads the trained weights of each model and computes the Dice Score on the test set.

Before running the notebook, make sure you have the `checkpoints` folder in your project directory. This folder should contain the trained weights for all the models. You can obtain this folder by running the `setup.sh` script as described in the Setup section.

## Reproducing sweeps, training, and evaluation
Note that you will have to set up a WandB account and configure your CLI to run the codes correctly.

### Sweeps
1. Go to `notebooks/sweeps.ipynb`
2. Scroll to the section on "Training Loop" to comment out the model of choice. 
3. Scroll to the section on "Init Wandb" and change the number of `run_cap` in the configuration. For U-net: 43, UNETR: 65, SegFormer: 39.
4. Run the entire notebook and wait for the number of desired sweeps to complete. 
### Training
1. Go to `notebooks/train.ipynb`
2. Scroll to the section on "Training Loop" to comment out the model of choice. The models have already been pre-loaded with the best hyperparameters from the sweeps section.
3. Run the entire notebook and wait for 10 epochs to complete.

### Evaluation
1. Go to `notebooks/evaluation.ipynb`
2. Download the weights from [this link](https://storage.googleapis.com/dl-project-checkpoints/checkpoints.zip) and unzip it into the `notebooks/checkpoints` folder.
3. Run the entire notebook.
