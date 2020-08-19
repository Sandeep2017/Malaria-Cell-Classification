# Malaria Cell Classification

[![forthebadge](https://forthebadge.com/images/badges/made-with-python.svg)](https://www.python.org/)
[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)](https://forthebadge.com)

 ## Overview
* [Contributors](#Contributors)
* [Introduction](#Introduction)
* [Dataset & Preprocessing](#Dataset-And-Preprocessing)
* [Model Architecture](#Network-Architecture)
* [Loss Function & Optimizer](#Loss-Function-And-Optimizer)
* [Learning Rate](#Learning-Rate)
* [Result](#Result)
* [Conclusion](#Conclusion)

### Contributors:
This project is created by the joint efforts of
* [Subham Singh](https://github.com/Subham2901)
* [Sandeep Ghosh](https://github.com/Sandeep2017)

### Introduction:
Malaria caused by the Plasmodium parasites,
is a blood disorder, which is transmitted through the bite of a woman Anopheles mosquito. With almost 240 million cases mentioned each year, the sickness puts nearly forty percentage of the global populace at danger.  Thus,treatment of this disorder at the inital stages of occurance in the host's body is very neccessary,but for the treatment to take place the first step is the proper diagnosis of the host to detect malaria. Microscopic examinations of thick and thin blood smears for infected RBCs is commonly used for method of malaria diagnosis. Depending on the local protocol, the examination includes: 
* classifying and counting the normal and infected erythrocytes in the thin smear images; and/or 
* ountingparasites in thick smear images as specified in the WHOguidelines. Thus, the diagnostic accuracy is heavilydependent on manual expertise and can be adversely impacted by the burden posed by large scale analyses that are common in malaria endemic regionsAlternative techniques such as polymerase chain reaction (PCR) and rapid diagnostic tests (RDT) are also widely used. However,
PCR tests are limited in their performance while RDTs are less cost-effective in zones with high disease prevalence 
### Dataset and preprocessing:
We have used the [NIH malaria dataset](https://lhncbc.nlm.nih.gov/publication/pub9932),which contains 27,588 cell images with equal instances of parasitized and uninfected cells. Positive samples contained Plasmodium and negative samples contained no Plasmodium but other types of objects including staining artifacts/impurities. There are total __13,779 paratisized and 13,779 uninfected__ image samples.

* __Here are some sample picture of the dataset we have dealt with.__
![](https://github.com/Subham2901/Malaria_Cell_Classification/blob/master/graphs/samplepic.JPG)
#### Preprocessing:
We augmented our data on the fly using the [Albumentations library](https://albumentations.ai/). We applied random flips and rotations with random changes in lighting by increasing/decreasing contrast, gamma & brightness. 
### Network Architecture:
We have created three model architecture using different API namely
#### * Sequential API : We have used [keras sequential API](https://keras.io/guides/sequential_model/) to build this architecture along with [keras image generators.](https://keras.io/api/preprocessing/image/)
###### Sequential API
![](https://github.com/Subham2901/Malaria_Cell_Classification/blob/master/images/seq.png)
#### * Functional API : We have used [funtional API](https://keras.io/guides/functional_api/) along with custom functional generator for this model architecture.
###### Functional API
__We have used the same model structure just in funtional paradigm along with custom generator and augmentations.__
### * Transfer Learning : We have used transfer learning with [DenseNet201](https://keras.io/api/applications/densenet/) along with functional API for this model.
#### Transfer Learning
![](https://github.com/Subham2901/Malaria_Cell_Classification/blob/master/images/TL.png)
### Loss Function And Optimizer:
The loss-function that we have used here is [binary cross entropy.](https://keras.io/api/losses/probabilistic_losses/#binarycrossentropy-class) And, the optimiser that we have used is [Nadam.](https://keras.io/api/optimizers/Nadam/)  
### Learning Rate:
In case of sequential API we have used a fixed learing rate.
But in case of the other two models the learning rate we have used here is not constant throughout the training of the data, instead we have used a learning rate schedular, which increases/decreases the learning rate gradually after every fixed set of epochs such that  we can attain the optimum convergence by the end of our training of the data.

### Result:
We have compared the results mainly on the basis of validation [accuracy](https://www.tensorflow.org/api_docs/python/tf/keras/metrics/AUC) and validation [AUC](https://www.tensorflow.org/api_docs/python/tf/keras/metrics/AUC) of three model architectures.

##### * Graphical comparision:  
![](https://github.com/Subham2901/Malaria_Cell_Classification/blob/master/graphs/Final%20Graph.JPG)
__Hence we can clearly see from the three graphs that the model architecture using functional API has performed better w.r.t to the other two models.__


#### * Tabular Representation:
* __Table 1__
![](https://github.com/Subham2901/Malaria_Cell_Classification/blob/master/graphs/acctable.JPG)

* __Table 2__
![](https://github.com/Subham2901/Malaria_Cell_Classification/blob/master/graphs/auctable.JPG)

### Conclusion:
__Hence we can conlcude that Using transfer learning we  extract many unwanted features in our model which stands out to be irrelevant while classifying the real data.Here, Our functional model with a custom generator has succesfully performed the task better than the model that we have created usng transfer learning__
