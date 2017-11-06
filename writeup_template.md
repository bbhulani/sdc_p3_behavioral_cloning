**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


####1. Submission includes all required files and can be used to run the simulator in autonomous mode
My project includes the following files:
* model.py.ipynb containing the python notebook to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md summarizing the results
* run1.mp4 is the captured video 

####2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
python drive.py model.h5

####3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

###Model Architecture and Training Strategy

####1. An appropriate model architecture has been employed
- First image is normalized with a zero mean
- The image is cropped from 160x320x3 to 65x200x3
- The model chosen was a modified version of the Nvidia acrhitecure. It has 4 convolutional layers and 4 fully connected layers. 


####2. Attempts to reduce overfitting in the model
The model was overfitting so to reduce it I added dropouts for each fully connected layer 5, 6, 7

The model was trained and validated on different data sets using validation split to ensure that the model was not overfitting. The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

####3. Model parameter tuning
The model used an adam optimizer, so the learning rate was not tuned manually.

####4. Appropriate training data
Training data was chosen to keep the vehicle driving on the road. 
I used the following different data sets collected by my poor driving skills :P
- Smooth driving through the track over 3 laps
- Reovery driving through the track over 1 laps
- Driving in the opposite direction over 1 laps (used this same data twice)

###Model Architecture and Training Strategy

####1. Solution Design Approach
The overall strategy for deriving a model architecture was to use the Nvidia architecture for the convolutional neural network. 
The approach taken was
- Use a generator function so that large amount of data can be used for training
- Each image captured from data set is flipped to augment the data and decrease the left side bias. 
- Each image captured is normaliezed and cropped before processing. 
- Each image captured is processed with the convolutional neural network based on Nvidia's architecture
- Capturing the right data set is the key. Including recovery driving and driving the car in the opposite direction were the key to keep the car on track throughout the course. 
- After collecting the right dataset and running thru the model I added dropout layers for each fully connected layer to avoid overfitting

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

####2. Final Model Architecture
- After normalizing and cropping input image sise to the convnet is 65x200x3
- Layer1: Convolutional layer with 5x5 kernel and max pooling 2x2. Output = 31x98x24
- Layer2: Convolutional layer with 5x5 kernel and max pooling 2x2. Output = 14x47x36
- Layer3: Convolutional layer with 5x5 kernel and max pooling 2x2. Output = 5x22x48
- Layer4: Convolutional layer with 3x3 kernel and max pooling 2x2. Output = 2x10x64
* I ran into some shape mismatch error when I tried to add a 5th convolutional layer after Layer4 conv2d (i.e. w/o max pooling in layer4). So I decided instead to just keep 4 layers and use max pooling on the 4th layer
- Layer5: Fully connected layer. Output 1x1x100
- Layer6: Fully connected layer. Output 1x1x50
- Layer7: Fully connected layer. Output 1x1x10
- Layer8: Fully connected layer. Output 1x1x1


####3. Creation of the Training Set & Training Process
- To capture good driving behavior I ran the simulator and capture about 3 laps of smooth driving through the track. This got the cat going in autonomous mode but it was primarily drifting to the left of the road. 
[image1]: ./visualization/center_2017_11_03_23_18_37_315.jpg 
[image2]: ./visualization/center_2017_11_03_23_18_38_753.jpg
[image3]: ./visualization/center_2017_11_03_23_18_38_855.jpg
[image4]: ./visualization/center_2017_11_03_23_18_38_925.jpg
[image5]: ./visualization/center_2017_11_03_23_18_38_980.jpg
[image6]: ./visualization/center_2017_11_03_23_18_39_053.jpg
[image7]: ./visualization/center_2017_11_03_23_18_39_123.jpg
[image8]: ./visualization/center_2017_11_03_23_18_39_194.jpg
[image9]: ./visualization/center_2017_11_03_23_18_39_293.jpg
[image10]: ./visualization/center_2017_11_03_23_18_39_362.jpg
[image11]: ./visualization/center_2017_11_03_23_18_39_440.jpg
[image12]: ./visualization/center_2017_11_03_23_18_39_535.jpg
[image13]: ./visualization/center_2017_11_03_23_18_39_611.jpg

- Next I collected data to drive the car in the oppossite direction. This was really helpful the car was staying more towards the center of the lane. It made it pass the bridge with this but would crash at the sharp turn 
[image1]: ./visualization/center_2017_10_29_10_28_09_596.jpg
[image2]: ./visualization/center_2017_10_29_10_28_09_523.jpg
[image3]: ./visualization/center_2017_10_29_10_28_09_447.jpg
[image4]: ./visualization/center_2017_10_29_10_28_09_371.jpg
[image5]: ./visualization/center_2017_10_29_10_28_09_294.jpg
[image6]: ./visualization/center_2017_10_29_10_28_09_203.jpg
[image7]: ./visualization/center_2017_10_29_10_28_09_140.jpg
[image8]: ./visualization/center_2017_10_29_10_28_09_051.jpg
[image9]: ./visualization/center_2017_10_29_10_28_08_978.jpg
[image10]: ./visualization/center_2017_10_29_10_28_09_861.jpg
[image11]: ./visualization/center_2017_10_29_10_28_09_768.jpg
[image12]: ./visualization/center_2017_10_29_10_28_09_709.jpg

- Then I captured recovery drving and added that to the data set. This allowed it to make it past the sharp turn and finally I was able to drive the car autonomously and complete the lap. 
[image1]: ./visualization/center_2017_11_03_23_54_27_549.jpg
[image2]: ./visualization/center_2017_11_03_23_54_27_440.jpg
[image3]: ./visualization/center_2017_11_03_23_54_27_339.jpg
[image4]: ./visualization/center_2017_11_03_23_54_27_261.jpg
[image5]: ./visualization/center_2017_11_03_23_54_27_163.jpg
[image6]: ./visualization/center_2017_11_03_23_54_27_092.jpg
[image7]: ./visualization/center_2017_11_03_23_54_27_009.jpg
[image8]: ./visualization/center_2017_11_03_23_54_26_921.jpg

- Finally I reused the dataset when the car drove in the opposite direction. With this the car was able to drive more smoothly and not drift to the left

I finally randomly shuffled the data set and put 20% of the data into a validation set. 

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was 15 as evidenced by ... I used an adam optimizer so that manually training the learning rate wasn't necessary.
