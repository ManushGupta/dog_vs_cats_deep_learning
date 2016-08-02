# dog_vs_cats_deep_learning

This project is an attempt to solve this kaggle competition:

https://www.kaggle.com/c/dogs-vs-cats

The training and test data was received from the competition page and put into separate folders called 'test' and 'train' inside a folder called 'input' in the main repository

Steps:

1. Run create_lmdb.py after preparing data in input folder. create_lmdb.py script does the following:

Runs histogram equalization on all training images for adjusting contrast.
Resizes all training images to a 227x227 format.
Divides the training data into 2 sets: One for training (5/6 of images) and the other for validation (1/6 of images).
Stores the training and validation in 2 LMDB databases. train_lmdb for training the model and validation_lmbd for model evaluation.

2. Generate the mean image of training data:

Substract the mean image from each input image as a common preprocessing step in supervised machine learning.

/path/to/caffe/build/tools/compute_image_mean -backend=lmdb /path/to/input/train_lmdb /path/to/input/mean.binaryproto

3. Model definition and Solver definition inside caffe models folder.

Made few modifications to the original bvlc_reference_caffenet prototxt file here for 2 classes as output. 
 
This model is a replication of AlexNet with a few modifications.

I chose lr_policy: "step" with stepsize: 2500, base_lr: 0.001 and gamma: 0.1. In this configuration, i start with a learning rate of 0.001, and will drop the learning rate by a factor of ten every 2500 iterations.

After Training, i obtained the learning curve as follows(this training was done without transfer learning)

![alt tag](/caffe_models/caffe_model_1/caffe_model_1_learning_curve.png)

It produced around 87.5% accuracy on Test Data set as given by Kaggle. 80th place on the competition charts.

![alt tag](/kaggle_1.png)

After training with tranfer learning, i obtained the learning curve as follows: (i use the trained bvlc_referrence_caffenet for transfer learning)

![alt tag](/caffe_models/caffe_model_2/caffe_model_2_learning_curve.png)

It produced around 97% accuracy on Test Data set as given by Kaggle. 22nd place in the competition charts.

![alt tag](/kaggle_2.png)
