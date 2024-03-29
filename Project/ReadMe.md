#  Effectiveness of Data Augmentation on Image Classification Performance

Contributors :  Pallavi Singh, Sebastian Gazda, Mehmet Ayanoglu, Zhenyi Chen


### Project Summary

We propose exploring the problem associated with the classification of the model with insufficient data like in the field of medical industry where data is heavily protected and also not
enough cases for providing a better model for diagnosis. It is common knowledge that more data in the ML model will perform better, higher quality than with less data which could result in lower quality
of the model making the testing data prone to failure.One of the methods to overcome the insufficient data problem is by increasing the data size using data augmentation “ Data Augmentation can improve the performance of their models and
expand limited datasets to take advantage of the capabilities of big data ”[1] The datasets we examine are Fashion-mnist and mnist, here we train our model with typical data augmentation techniques and hyperparameter tuning, we restrict our data in two classes first with larger training size and then with smaller training size, the convolutional neural network learns
augmentation and then gives the best accuracy with minimum loss. Finally, we will measure classification performance on the testing sets and calculate the
parameters of the Confusion matrix.

## Experimental Setup
For our testing, we used two datasets: Mnist and Fashion-Mnist. Since we are comparing the effect of augmenting images, we decided it would be best if we worked with proven datasets that are
known to work well and by using two datasets, we can show the effect on two different samples.Both datasets consist of 60K training and 10k testing images with an image size of 28x28 and
they were prepared in two ways. First, we normalized all of the samples in the dataset. The normalized data were then used in the CNN as a control group. Second, we used “ImageDataGenerator” which is found in Keras, to augment the images. The augmentations that we chose were rotation, vertical and horizontal shift, and zoom. Once augmented, the images were then
normalized and used in the CNN as the testing group.


##Methodology
* 1) Data Augmentation
Data augmentation was performed using “ImageDataGenerator” found in Keras. Once the dataset is loaded through Keras, “ImageDataGenerator” is set up for rotation, shift, and zoom. The generator creates a new dataset that holds the augmented versions of the images in the input
dataset. The original dataset was then appended to also include the augmented images, and then the pixel values of every image were divided by 255 to normalize the images. This final normalized dataset was then used in the CNN.
* 2) Overall Network Model, Architecture
The main factors in the CNN model are the channels of training images, size and number of CNN kernels, pooling size, number of layers, the loss function, and the classes of output. We have 4
convolution layers with 3 x 3 filters which were good enough for the classification performance. No dropouts was used because we found that overfitting may not be a problem here and therefore dropout would not have much effect in our experiments. Rectified linear unit (RELU) activation
function was used for the hidden layers. 2 MaxPooling layers with pooling window size of 2 x 2 which is a popular setting and helps shorten training time and reduce the number of parameters.
Categorical crossentropy was selected as the loss function because there are 10 classes to predict from. Stochastic Gradient Descent (SGD) optimizer was selected which is responsible for updating
the weights of the neurons via backpropagation. There are a total of 1,221,546 parameters in the network.
* 3) Hyperparameter Tuning
The hyperparameter tuning process is accomplished by;
      * a) Selection of the optimizer
      * b) Definition of the parameters to be optimized, manually trying a variety of values to understand the direction of the likelihood.
      * c) Application of different techniques such as learning rate scheduler and different functions for the scheduling algorithm.
      * d) Using techniques such as gridsearchcv to verify that the selected parameters were in the expected range.
The hyperparameters that can be optimized in SGD are learning rate, momentum, decay and nesterov . We decide to keep the number of epochs and batch size constant for the research
process of the SGD hyperparameters.We used different momentum applications such as Nesterov as well as different momentum values. Momentum is a small change to the SGD parameter update that accelerates learning
compared to plain Stochastic Gradient Descent. Nesterov momentum is a simple change to normal momentum where gradient is added after the momentum direction is applied towards the better theta
at the iteration of descent. Nesterov momentum application provided improvement on both our accuracy and loss.
Also, a custom learning rate change using LearningRateScheduler was implemented. The decay hyperparameter holds the value of degradation of the learning rate after each epoch. For this
implantation we use the callbacks, to call back the Loss and the learning rate of the fit function after each epoch, and update the LR value and use it for the training of the next epoch of the model. The
decay formula we chose is; 𝑙𝑟=𝑙𝑟₀ × 𝑒^(−𝑘𝑡) k = decay rate, t = epoch number The LearningRateScheduler technique also improved both our accuracy and loss.

For verification and research purposes, we also tried tuning hyperparameters using Cross-Validation with GridSearchCV from Scikit-Learn. This is a process to evaluate categorical
cross-entropy and compare accuracy and loss depending on different sets of Hyperparameters. We tried a grid search for Learning Rate and Momentum; learn_rate = [0.001, 0.01, 0.1], and
momentum = [0.6, 0.8, 0.9]. Best results were: 0.8802 accuracy using {'learn_rate': 0.01, 'momentum': 0.9}
* 4) Evaluation Measurement of the models To test the effectiveness of the datasets with augmentation and without augmentation for both 60K and 6K training sets, we run each experiment for 10 epochs at the learning rate of 0.01 using SGD
optimization. The results of the experiments are tabulated below. The validation accuracy at the 10th epoch is recorded.


## Results
Graph 1 shows Fashion_Mnist with/without Augmentation Vs Mnist with/without Augmentation [for 60K training], Graph 2 shows Fashion_Mnist with/without Augmentation Vs Mnist with/without
Augmentation [for 6K training].
All the experiments were evaluated for precision,recall and F1 score using the confusion matrix A comparison between all the experiments is shown in the table below with 60K training set and 6K
training set.

##Conclusion and lessons learned

Using gridsearchcv is an important tool to apply to figure the direction to be headed towards in the assignment of the hyperparameter values. Application of the learning rate scheduler on top of the
predetermined hyperparameter values provided improvement on both accuracy and minimizing the loss.

Data augmentation has been shown to produce improvements with the small training set [Fashion_Mnist_6000] vs larger training set [Fashion_Mnist_60K], however, in the Mnist dataset,
there is no improvement with data augmentation. This verifies that Data Augmentation is an important technique to consider when small amounts of data are provided also help improve the current state of
art algorithms for classification. While we only doubled the size of our dataset with augmented images, this dataset size could have easily been increased with even more augmentations.

References;
[1] Shorten, C., Khoshgoftaar, T.M. A survey on Image Data Augmentation for Deep Learning. J Big
Data 6, 60 (2019). https://doi-org.ezproxy.lib.usf.edu/10.1186/s40537-019-0197-0

