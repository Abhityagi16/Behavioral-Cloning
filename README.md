# Behavioral Cloning Project

[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

My basis for the model architecture is [Nvidia's End-to-End Deep Learning Model for Self-Driving Cars](https://devblogs.nvidia.com/parallelforall/deep-learning-self-driving-cars/).

I added one dropout layer after the first two CNN layers, one dropout layer after the last CNN layer and two dropout layers between the first two fully connected layers.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. 

Initially I was using 3 epochs to train the model (as given in lectures) but it was not working for me. After discussing it with other course mates I changed the number of epochs to 10 and mse dropped down significantly by 10th epoch. 

The vehicle managed to drive around Track 1 in autonomous mode but went off track on Track 2 after around 20 sec. Since today is the deadline I don't think I can submit Track 2 as well (I would really appreciate if the reviewer could give me some tips for the second track).

#### Final Model Architecture

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

#### Run1.mp4 file shows the autonomous drive by the above trained model.
