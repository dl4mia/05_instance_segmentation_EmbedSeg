# Instance Segmentation with EmbedSeg (DL4MIA-22)

### Goals

1. Train from scratch and Infer with a 2D *EmbedSeg* network
2. Fine-tune using a pre-trained 2D EmbedSeg model and Infer with a 2D EmbedSeg network
3. Train from scratch and Infer with a 3D (sliced) *EmbedSeg* network
4. Train from scratch and Infer with a 3D *EmbedSeg* network

### Overview

In this tutorial, we shall learn to use *EmbedSeg* notebooks to train a model for **2D** and **3D** instance segmentation on microscopy images.

*EmbedSeg* belongs to the family of embedding-based approaches which have demonstrated success at instance segmentation.

In this exercise, we shall demonstrate steps for training and predicting using a 2D (**G**-1) and 3D (**G**-3,4) *EmbedSeg* network. We shall also see how we can use a model trained on one dataset and fine-tune it on limited labels of a separate dataset (**G**-2).

General pipeline of each notebook is:

- **Preprocess data, get data properties and save as crops**

We preprocess the original images and instance masks into equally sized square crops. This is a way to augment the available data and also provide equally sized images.

- **Train network for a few epochs**

We either train a model from scratch (**G-**1,2 & 4) or fine-tune a pre-trained model (**G**-2) for a few epochs.

- **Predict on evaluation data**

We test the trained model on data which has never been shown to the model during the training phase.

### [0/4] Download EmbedSeg code

If `pytorchEnv` environment already exists (which we created in the *U-Net* example), then open a fresh terminal window (click on *Activities* at top-left and select *Terminal* Window), change directory to `DL4MIA` and enter the following commands (this installs `EmbedSeg` within the existing environment):

```bash
cd DL4MIA
conda activate pytorchEnv
git clone https://github.com/juglab/EmbedSeg.git
cd EmbedSeg
git checkout DL4MIA-22
pip install -e .
```

Else, create a fresh environment:

```bash
cd DL4MIA
conda create -y -n pytorchEnv python==3.7
conda activate pytorchEnv
conda install -y pytorch torchvision cudatoolkit=11.3 -c pytorch
git clone https://github.com/juglab/EmbedSeg.git
cd EmbedSeg
git checkout DL4MIA-22
pip install -e .
```

### [1/4] **Train and Infer with a 2D *EmbedSeg* network**

Browse to the 2D exercise:

```bash
cd examples/DL4MIA/train-and-predict-2d.ipynb
jupyter notebook
```

Total runtime of this notebook (`Kernel >Restart and Run All`) is around `35` min.

### [2/4] Fine-tune a pretrained model **and Infer with a 2D *EmbedSeg* network**

Browse to the 2D fine-tuning exercise in the browser (*examples/DL4MIA/train-and-predict-2d_finetuning.ipynb*).

Total runtime of this notebook is under `10` min.

### [3/4] **Train and Infer with a 3D (sliced) *EmbedSeg* network**

Note: *3D sliced* exercise is an approach that uses a 2D network during training but is able to interpolate predictions between slices of a 3D stack during inference and predict instance segmentations for 3D images.

Browse to the 3D sliced exercise in the browser (*examples/DL4MIA/train-and-predict-3d-sliced.ipynb*).

Total runtime of this notebook is under `25` min.

### [4/4] **Train and Infer with a 3D *EmbedSeg* network**

Browse to the 3D exercise in the browser (*examples/DL4MIA/train-and-predict-3d.ipynb*).

Total runtime of this notebook is under `15` min.