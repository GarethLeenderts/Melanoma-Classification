# Melanoma Prediction



## Overview

According to the [Skin Cancer Foundation](https://www.skincancer.org/skin-cancer-information/skin-cancer-facts/):

* More people are diagnosed with skin cancer each year in the U.S. than all other cancers combined.
* The annual cost of treating skin cancers in the U.S. is estimated at $8.1 billion: about $4.8 billion for nonmelanoma skin cancers and $3.3 billion for melanoma.
* When detected early, the 5-year survival rate for melanoma is 99 percent.



Developing tools which can aid in the early detection of cancerous skin lesions could help to save numerous lives, as well as decrease the time and costs related to cancer detection.

The goal of this project is to build a model which can predict whether the skin lesion(mole) in the given image is a melanoma or not.

## Data 

link to competition: https://www.kaggle.com/c/siim-isic-melanoma-classification/overview

* Over 33000 training images
* Extremely Imbalanced(less than 2% of the dataset are positive cases)
* Metadata about patients also provided(eg. age, anatomical site, & sex)



## Results

Evaluation Criteria: AUC

Best Scores: 

* Private Score:   0.8984     Public Score:   0.8903    [Ensemble 4]
* Private Score:   0.8978     Public Score:   0.8984    [Ensemble 2]
* Private Score:   0.8977     Public Score:   0.8990    [Ensemble 2]



## Models Used

* VGG16
* VGG19
* WideResNet50
* ResNext50
* ResNet152
* EfficientNet (b0 - b7)
* Ensemble 1
  * Base models - VGG16, WideResNet50, & ResNext50 
  * Each 1000 feature output concatenated to give a 3000 feature layer
  * Added linear layers to get down to a single prediction
* Ensemble 2
  * Base models - VGG16, VGG19, WideResNet50,  ResNext50, & ResNet152 (note: these models had single feature outputs here instead of 1000 feature outputs)
  * Concatenate the model outputs
  * Add a final fully-connected/linear layer to get single output prediction
* Ensemble 3
  * A simple average of all model predictions
* Ensemble 4
  * A simple average of predictions for the following models:
    *  VGG16
    *  VGG19
    *  WideResNet50
    *  ResNext50
    *  ResNet152



## Techniques Used

* Image Augmentation(rotate & flip)
* Upsampling (using PyTorch's weighted sampler)
* Focal Loss (instead of plain Binary Cross-Entropy Loss)
* Learning Rate Scheduler (ReduceOnPlateau)
* Image Resizing (resized to 224x224 px)
* Transfer Learning (using torchvision's pretrained models - trained on ImageNet)
* Test-time augmentation (aka. Inference-time augmentation)



## Improvements

Some changes that may improve results/predictions:

* Larger Images (eg. 512x512 px)
* Self-supervised pre-training (several methods discussed in literature)
* K-Fold ensembles
* More models (bigger ensemble)
* More training data (there is extra data from older competitions)
* More image augmentation (add more methods into the augmentation pipeline such as cut-out and blurring)
* Use of a learning rate finder may help with faster training
* Test different learning rate schedulers
* Train an autoencoder as a pretext task (anomaly detection approach - images which the autoencoder was not trained on get "corrupted" or distorted)

