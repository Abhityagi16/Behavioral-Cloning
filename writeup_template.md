## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* run1.mp4 video of autonomous simulation 
* writeup_report.md or writeup_report.pdf summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

I used Nvidia's Deep Learning Model for Self-Driving Cars architecture.

The model consists of a convolutional neural network with 5x5 and 3x3 filter sizes and depths between 24 and 64.

#### 2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting. 

The model was trained and validated on different data sets to ensure that the model was not overfitting (code line 10-16). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (line 120 in model.py).

#### 4. Appropriate training data

I tried to create training data but simulator was lagging a lot to be able to create meaningful data so I used the data provided in the workspace.

### Model Architecture and Training Strategy

#### 1. Solution Design Approach


My basis for the model architecture is [Nvidia's End-to-End Deep Learning Model for Self-Driving Cars](https://devblogs.nvidia.com/parallelforall/deep-learning-self-driving-cars/).

I added one dropout layer after the first two CNN layers, one dropout layer after the last CNN layer and two dropout layers between the first two fully connected layers.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. 

Initially I was using 3 epochs to train the model (as given in lectures) but it was not working for me. After discussing it with other course mates I changed the number of epochs to 10 and mse dropped down significantly by 10th epoch. 

The vehicle managed to drive around Track 1 in autonomous mode but went off track on Track 2 after around 20 sec. Since today is the deadline I don't think I can submit Track 2 as well (I would really appreciate if the reviewer could give me some tips for the second track).

#### 2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers and layer sizes:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 40x160x3 YUV image   					    	| 
| Lambda Layer        	|                         						| 
| Convolution 5x5     	| Strides: 2x2, Output: 18x78x24              	|
| Convolution 5x5     	| Strides: 2x2, Output: 7x37x36               	|
| Dropout            	| rate: 0.3                                   	|
| Convolution 5x5     	| Strides: 2x2, Output: 2x17x48               	|
| Convolution 3x3     	| Output: 64x15x46                             	|
| Convolution 3x3     	| Output: 62x13x64                            	|
| Dropout            	| rate: 0.3                                   	|
| Flatten       		| Output: 3968     		                    	|
| Fully connected		| Output: 100                        			|
| Dropout            	| rate: 0.3                                   	|
| Fully connected		| Output: 50                          			|
| Dropout            	| rate: 0.3                                   	|
| Fully connected		| Output: 10                          			|
| Fully connected		| Output: 1                          			|

#### 3. Creation of the Training Set & Training Process

I used data provided in the workspace to for the training.

I used train_test_split method to create training and validation set.

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. I used an adam optimizer so that manually training the learning rate wasn't necessary.

I set the driving speed to 14 in drive.py to test my model on faster speed.
