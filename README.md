# ResNet-for-Tiny-Imagenet

This project is to create a full pre-activation ResNet architecture for the Tiny Imagenet dataset to evaluate the validation accuracy.

### About the Dataset:
Tiny Imagenet is a smaller version of the Imagenet Dataset with 100,000 images and 200 classes, i.e 500 images per class. Each image is of the size 64x64 and has classes like [ Cat, Slug, Puma, School Bus, Nails, Goldfish etc. ]. For Validation, we have 10,000 images of size 64x64 with 50 images per class. Most of the images for testing are extremely difficult to recognize the class even with the naked eye.

### Proposed Full Pre-Activation ResNet:

![res_block](https://qph.fs.quoracdn.net/main-qimg-c2aaf6646cbe1dcb10709e6d2004727d "ResNet architectures")

Each block used is a Full Pre-Activation ResNet model which outperforms the ResNet architecture. Here, the difference is in each block, it is `Batch Normalization ---> ReLU ---> Convolution` instead of the other way round.

### Model Architecture:
The Model architecture used is as following: 

![res_model](https://github.com/kesaroid/ResNet-for-Tiny-Imagenet/blob/master/model.png "ResNet model implemented")

9 blocks in total, with 8 ResNet blocks and GlobalAveragePooling at the end. 

I have used Softmax activation, Categorical cross entropy loss.
Adam optimizer is used for the initial epochs followed by Stochastic Gradient Descent.

Callbacks used are: Model checkpoint, Reduce learning rate on plateu and CSV logger. 

### Augmentation Techniques:

I used the `imgaug` library to augment my images, and few of the augmentation methods are 

* Gaussian Blur
* Horizontal Flip
* Crop
* Coarse Dropout
* Scale
* Translate Percent
* Rotate
* Shear

### Class Weights:

I have implemented an algorithm to recognize the classes that are performing badly and make the model concentrate more on these specific classes by adding a factor to the weights.
