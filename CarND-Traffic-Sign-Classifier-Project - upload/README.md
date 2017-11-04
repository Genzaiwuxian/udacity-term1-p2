## Project: Build a Traffic Sign Recognition Program
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

Overview
---
In this project, you will use what you've learned about deep neural networks and convolutional neural networks to classify traffic signs. You will train and validate a model so it can classify traffic sign images using the [German Traffic Sign Dataset](http://benchmark.ini.rub.de/?section=gtsrb&subsection=dataset). After the model is trained, you will then try out your model on images of German traffic signs that you find on the web.

We have included an Ipython notebook that contains further instructions 
and starter code. Be sure to download the [Ipython notebook](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb). 

We also want you to create a detailed writeup of the project. Check out the [writeup template](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project/blob/master/writeup_template.md) for this project and use it as a starting point for creating your own writeup. The writeup can be either a markdown file or a pdf document.

To meet specifications, the project will require submitting three files: 
* the Ipython notebook with the code
* the code exported as an html file
* a writeup report either as a markdown or pdf file 

Creating a Great Writeup
---
A great writeup should include the [rubric points](https://review.udacity.com/#!/rubrics/481/view) as well as your description of how you addressed each point.  You should include a detailed description of the code used in each step (with line-number references and code snippets where necessary), and links to other supporting documents or external references.  You should include images in your writeup to demonstrate how your code works with examples.  

All that said, please be concise!  We're not looking for you to write a book here, just a brief description of how you passed each rubric point, and references to the relevant code :). 

You're not required to use markdown for your writeup.  If you use another method please just submit a pdf of your writeup.

The Project
---
The goals / steps of this project are the following:
* Load the data set
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

### Dependencies
This lab requires:

* [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit)

The lab environment can be created with CarND Term1 Starter Kit. Click [here](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) for the details.

### Dataset and Repository

1. Download the data set. The classroom has a link to the data set in the "Project Instructions" content. This is a pickled dataset in which we've already resized the images to 32x32. It contains a training, validation and test set.
2. Clone the project, which contains the Ipython notebook and the writeup template.
```sh
git clone https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project
cd CarND-Traffic-Sign-Classifier-Project
jupyter notebook Traffic_Sign_Classifier.ipynb
```

### Requirements for Submission
Follow the instructions in the `Traffic_Sign_Classifier.ipynb` notebook and write the project report using the writeup template as a guide, `writeup_template.md`. Submit the project code and writeup document.

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).

## Files Submitted
all files have been submitted, except for the dataset of german traffic sign dataset (like train.p, test.p,etc)

## Step1: Dataset Exploration
- download dataset from web
- load train/validation/test dataset, and check the shape or number of each dataset
- random select one image and its label, visual it, check file of 'signnames', and see whether the relationship is correct or not

## Step2: Design and Test a Model Architecture
### Preprocessing
- shuffle the dataset to obtain a better value
- firstly, i use process the gray and shape-norminlize process, however, in the step3:test, the download image's shape is not (32,32,3), and the image after gray is (XX, XX, 1) not suit for the LeNet() input type, so just leave it here and miss use it
### Model Architecture
- type of model used: use LeNet() as basic model architecture
- the number of layers: 5 layers
- the size of each layer: CNN()
   - layer 1 CNN: Input = 32x32x1. Output = 28x28x6, Relu activation, max_pooling:Input = 28x28x6. Output = 14x14x6
   - layer 2 CNN: nput = 14x14x6. Output = 10x10x16, Relu activation, max_pooling:Input = 10x10x16. Output = 5x5x6
   - layer 3 Fully connected layer: Input = 400. Output = 120, rele activation
   - layer 4 Fully connected layer: Input = 120. Output = 84, rele activation
   - layer 5 Fully connected layer: Input = 84.  Output = 10, return logits
### Model Training
- optimizer: Adam
- batch size: 128
- epochs: 10
- rate: 0.001
after 10 epochs, the accuracy is 0.987

## Step 3: Test a Model on New Images
## Acquiring New Images
- The submission includes 6 new German Traffic signs found on the web and the images are visualized
- Resize: as the size of image is different, and the LeNet only accept size of (32, 32,3), so use cv2.resize function to make all images into right size
## Performance on New Images
- 5 images is recognized correct among 6 images, the correct accuracy is 83.33%
## Model Certainty - Softmax Probabilities
- i think, because the good quality, 5 images are correct recongized
- the not correct image is NO. 23 Slippery road
- the result show that TOP 1 image is NO.29 Slippery road, and then the correct NO. 23 with softmax value near 0.2.
Discussion is made as to particular qualities of the images or traffic signs in the images that are of interest, such as whether they would be difficult for the model to classify.
