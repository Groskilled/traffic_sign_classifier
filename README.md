#**Traffic Sign Recognition** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/train_data_viz.jpg "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/12163.jpg "Traffic Sign 1" 
[image5]: ./examples/08272.jpg "Traffic Sign 2" 
[image6]: ./examples/04576.jpg "Traffic Sign 3" 
[image7]: ./examples/09797.jpg "Traffic Sign 4" 
[image8]: ./examples/09161.jpg "Traffic Sign 5" 
## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
###Writeup / README

####1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/Groskilled/traffic_sign_classifier/blob/master/Traffic_Sign_Classifier.ipynb)

###Data Set Summary & Exploration

####1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the numpy and collections libraries to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32x3
* The number of unique classes/labels in the data set is 43

####2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how the data ...

![alt text][image1]

###Design and Test a Model Architecture

####1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to normalize the images but my network's performance got worse so I dicided not to use it.
Then I tried to generate additional data to see if it could help. So I flipped every image horizontaly and verticaly and trained my network on every possible combination (no flip, flip horizontal + base, flip vertical + base, both flips + base) and the vertical flip did not help so I removed it. I did not use grayscale transformation because my model works with 3 channels images.


####2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 3x3     	| 3x3 stride, same padding, outputs 32x32x64 	|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 32x32x64 	|
| Max pooling	      	| 2x2 stride,  outputs 16x16x128 				|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 16x16x128 	|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 16x16x128 	|
| Max pooling	      	| 2x2 stride,  outputs 8x8x256 				|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 8x8x256 	|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 8x8x256 	|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 8x8x256 	|
| Max pooling	      	| 2x2 stride,  outputs 4x4x512 				|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 4x4x512 	|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 4x4x512 	|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 4x4x512 	|
| Max pooling	      	| 2x2 stride,  outputs 2x2x512 				|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 2x2x512 	|
| Convolution 3x3     	| 3x3 stride, same padding, outputs 2x2x512  |
| Convolution 3x3     	| 3x3 stride, same padding, outputs 2x2x512 	|
| Max pooling	      	| 2x2 stride,  outputs 1x1x512 				|
| Fully connected		| outputs 4096        									|
| Fully connected		| outputs 4096        									|
| Fully connected		| outputs 43          									|
 


####3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an Adam optimizer cause it usually does well and I am named Adam. I set the batch size to 128 since my GPU is not powerful enough to have a bigger batchsize without having memory problems. Concerning the number of epochs I went for 15 since it allows me to reach the score needed to complete the project, and for the learning rate I had bad results with 0.001, reaching a plateau and probably overshooting and increasing the error at some point.

####4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 99.5%
* validation set accuracy of 93.8% 
* test set accuracy of 91.65 %

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?
* What were some problems with the initial architecture?
* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
* Which parameters were tuned? How were they adjusted and why?
* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?

If a well known architecture was chosen:
* What architecture was chosen?
I went for vgg16.
* Why did you believe it would be relevant to the traffic sign application?
I go for a vgg16 everytime I need to work with images since it performs well and weights are available (even if I did not used it here) and it is used for classification, exactly what we need here.
* How does the final model's accuracy on the training, validation and test set provide evidence that the model is working well?
 

###Test a Model on New Images

####1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]

The first image might be difficult to classify because there is another sign we can partially see on the image.

####2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Road work			| Road work				|
| Keep right			| Keep right 				|
| SpeedLimit 70					| SpeedLimit 70		|
| Right-of-way at the next intersection			| Beware of ice/snow		|
| Roundabout mandatory			| Keep Right						|



The model was able to correctly guess 3 of the 5 traffic signs, which gives an accuracy of 60%. This does not compares favorably to the accuracy on the test set of 91%

####3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a stop sign (probability of 0.6), and the image does contain a stop sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| .52         			| Road Work   									| 
| .16     				| Traffic Signals 										|
| .13					| Speed limit 20											|
| .11	      			| Bumpy Raod					 				|
| .8				    | Bicycles Crossing      							|


### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
####1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


