# Instance Segmentation with EmbedSeg 

In this tutorial, we shall learn to use *EmbedSeg* notebooks to train a model for **2D** and **3D** instance segmentation on microscopy images.

### Goals

1. Train and Infer with a 2D *EmbedSeg* network
2. Infer with a 3D *EmbedSeg* network

## [1/2] **Train and Infer with a 2D *EmbedSeg* network**

### Overview

*EmbedSeg* belongs to the family of embedding-based approaches which have demonstrated success at instance segmentation. In this exercise, we shall demonstrate steps for training and predicting a 2D *EmbedSeg* network on the *BBBC010* dataset which contains bright field images of *C. elegans* worms.

### Goals

DIFFICULTY LEVEL = Medium

1. Download *EmbedSeg* notebooks
2. Preprocess data and save as crops
3. Train network for 1 epoch
4. Predict on evaluation data using under-trained and fully-trained model weights

### Installation [<5 min]

Open a fresh terminal window ( in the browser, withing *Jupyter*: *New > Terminal*) and enter the following commands:

```bash
conda create -n EmbedSegEnv python==3.7
cd DL4MIA
conda activate EmbedSegEnv
conda install pytorch torchvision cudatoolkit=10.2 -c pytorch
git clone https://github.com/juglab/EmbedSeg.git
cd EmbedSeg
git checkout v0.2.4
pip install -e .
```

Then browse to the 2D exercise 

```bash
cd examples/2d/bbbc010-2012
```

### Preprocess Data [<10 min]

 This notebook preprocesses the original images and instance masks into equally sized square crops. This is a way to augment the available data and also provide equally sized images.

1. Change kernel to `conda env:EmbedSegEnv`
2. Run the cells one after the other (Keyboard shortcut: *Shift-Enter*. This should take <5 minutes in total)
3. Go to ***data*** directory (it should be present at the same level as ***examples***)
4. Explore 1-2 images and masks by dragging and dropping in *Fiji*
5. Next go to the ***crops*** directory (it should be present at the same level as **examples/2d/bbc010-2012/.**) All the cropped images and masks should be present here.

### Train a 2D Model [<15 min]

The notebook (***02-train.ipynb***) enables training a neural network. Here the network accepts the cropped patches as input and learns the mapping to the target cropped instance masks. In this section, we shall note how we can resume training from the last model weights. 

1. Change kernel to `conda env:EmbedSegEnv`
2. Run the cells one after the other (Keyboard shortcut: *Shift-Enter.* This should begin training the network) 
3. Wait until the network has been trained for 1 epoch (<10 min)
4. Stop training once epoch 2 begins (click on black square *stop* button in the top panel). This should be the case after two progress bars are filled up… ;)
5. Change the parameter ***resume_path = save_dir+'/checkpoint.pth'*** in what might be the cell **[13]**. Don’t forget to execute that cell to activate the change. Again start the training by running the last (maybe 16th) cell. Note which epoch does the network begin from. (Spoiler: it should be the one you canceled the training at…)
6. Open a new terminal window and check the GPU memory usage by typing in ***nvidia-smi*** -- can you find out how much GPU memory the network we are training in this exercise requires? (Spoiler: not much at all!)

### Infer with under-trained and fully-trained model [<15 min]

The notebook (***03-predict.ipynb***) enables making predictions on unseen data by the trained neural network. In this notebook, we shall make predictions using weights from a fully-trained network and also the network trained by you for 1 epoch.

1. Change kernel to `conda env:EmbedSegEnv`
2. Run the cells one after the other -- all of them until the bottom. This will run a fully-trained model, one we trained for 200 epochs.
3. Browse to ***inference*** directory *(*the complete path is *`examples/2d/bbbc010-2012/inference/`*)
4. You could modify the third cell: uncomment commented lines and comment uncommented lines: re-run the following cells to see predictions from your own trained model.
5. On cell **[5]**, in **tta,** replace **True** with **False**. Test Time Augmentation (*tta*) may cause inconsistent results when testing with models trained for short times.

### Resources

1. [Link](https://bbbc.broadinstitute.org/BBBC010) to original dataset
2. [Link](https://github.com/juglab/EmbedSeg.git) to *EmbedSeg* repository 

## [2 / 2] Train and Infer with a 3D Network

### Overview

*EmbedSeg* also allows you to perform instance segmentation on 3D microscopy images. In this exercise, we shall download some mouse organoid data coming from the *Honigmann Lab*, employ a pretrained model on some evaluation images and visualize the results in jupyter notebooks.

### Goals

DIFFICULTY LEVEL = Easy

1. Download Data
2. Run pretrained model

### Download Data [<5 min]

The notebook (***01-data.ipynb***) allows you to download the data from an external link. In this case, we shall only run part of the notebook since we do not, for the purpose of this exercise, wish to train a network.

1. Change kernel to `conda env:EmbedSegEnv`
2. Go to `examples/3d/Mouse-Organoid-Cells-CBG/01-data.ipynb`
3. Run the first five cells (the fourth and fifth cell reserve some of the data for testing) 
4. If download takes too long, one could copy the data from `/group/carecourse/embedseg_data` as follows:

```
cd /group/carecourse/embedseg_data
cp -rv Mouse-Organoid-Cells-CBG ~/DL4MIA/EmbedSeg/data/. 
```

### Infer with a fully trained model [<15 min]

The notebook (***03-predict.ipynb***) allows you to use a fully-trained model on the images reserved for evaluation. 

1. Change kernel to `conda env:EmbedSegEnv`
2. Run the cells one after the other
3. Browse to ***inference*** directory *(*the complete path is *`examples/3d/mouse-organoid-cells-cbg/inference/`*). This folder contains  the model predictions on unseen data. 
4. If no visualizations appear inline in the last two cells, replace them by :

```bash
viewer = view(image_itk, label_image=prediction_itk, cmap=itkwidgets.cm.BrBG, annotations=False, vmax=800, ui_collapsed=True, background=(192, 192, 192))
embed_minimal_html('export_'+str(index)+'.html', views=viewer, title='Widgets export')
```

(This would produce an `export*.html` document at the same level as the notebooks which you can open in the browser to verify the quality of 3d segmentations)
