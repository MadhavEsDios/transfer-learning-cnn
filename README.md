This is a quick implemenatation of transfer learning tecnhiques and how it can be used for classification problems using CNN's
This technique is also known as 'fine tuning of a pre-trained network'.

Tranfer Learning is when a neural network that has been trained on a completely different task is used directly on another problem to achieve high levels of performance. This involves either directly using the network along with its learnt weights or just using the architecture of the network.

The main idea behind transfer learning in CNN's is that CNN's which have been trained on extremely huge and diverse datasets with the help of GPU's over a period of months to achieve state-of-art levels of performance can also be used on other seemingly different tasks to achieve a very high level of accuracy without high computation costs.

Lets take the example of a classification task where pictures of dogs need to be classified with their breeds being the output label. So like explained above I download a pre-trained network which has been trained on the ImageNet dataset (which also includes pictures of dogs), in this case I use the pre-trained VGG19 model. The idea is that the VGG19 model has already learnt all the low-level (eg. lines, curves, etc) and high-level(eg.compex boundaries resembling dogs,etc.) features of identifying dogs and other objects, which in turn can prove to be of great use in our scenario. Thus,we can directly use these features obtained by forward propogation of the image through the pre-trained convolutional part of the network and only change the Fully Connected Layers at the end to obtain our desired labels.

There are 2 popular ways of doing this :

1) Add your own choice of FC layers after the pre-trained convoultional model, set all the layers of pre-trained convolutional model to be non-trainable i.e back-propagation only needs to learn parameters in the FC layers and nothing before it, compile it and fit the new-model like any Keras model.

Adv: You can use data-augmentation techniques,
Disadv : VGG 19 is computationally expensive and is run multiple times

2) Forward propogate the images throught the pre-trained convoultional netwrok and save the output feature vectors for both the training and validation datasets. Now, this becomes your new training and validation dataset, this will then be used as input to a model which is nothing but your FC layers and then will be used to learn the parameters of this model to output your desired class labels.

Adv: VGG 19 is only run once unlike above,
Disadv: Data augmentation techniques cannot be used, unless explicitly computed and stored.


In both these implementations we have not messed around with the convolutional part of the pre-trained network and just added onto it, but the same techniques can be used to learn the parameters of more layers(convolutional / FC) from scratch
For eg. in the 1st technique some of the convolutional layers at the end might be excluded from being non-trainable



Note: I have written a quick dirty implementation of the pre-processing of the images, this can also be done in a better way using the pandas library, but that is not the point of this project.


The Stanford Dog dataset is available on Kaggle : https://www.kaggle.com/c/dog-breed-identification/data
