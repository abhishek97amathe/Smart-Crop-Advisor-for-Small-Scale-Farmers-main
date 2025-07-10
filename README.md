###Dataset
-------------
![](/figures/figure-1.jpg)
> Figure 1: Dataset samples

We extracted our dataset from the well known Plantvillage dataset, which contains nearly 5,000 image of 14 crop species and 26 diseases.
We choose to work with 9,000 images on Tomato leaves, our dataset contains samples for 5 types of Tomato diseases in addtion to healthy leaves, 6 classes in total as follow:
- class (0): Bacterial Spot.
- class (1): Early Blight.
- class (2): Healthy.
- class (3): Septorial Leaf Spot.
- class (4): Leaf mold.
- class (5): Yellow Leaf Curl Virus.

The images were resized into 150×150 for faster computations but without compromising the quality of the data.

###Model
-------------
Our model takes raw images as an input, so we used CNNs (Convolutional Nural Networks) to extract features, in result the model would consist of two parts:
- The first part of the model (features extraction), which was the same for full-color approach and gray-scale approach, it consist of 4 Convolutional layers with Relu activation function, each followed by Max Pooling layer. 
- The second part after the flatten layer contains two dense layers for both approaches, but in full-color the first has 256 hidden units which makes the total number of network trainable parameters 3,601,478, in the other hand gray-scale approach has 128 hidden units in the fist dense layer and 1,994,374 as total  trainable parameters, we shrinked the size of the gray-scal network to avoid overfitting, for the last layer for both has Softmax as activation and 6 outputs representing the 6 classes.

##### Full-Color Model Sammary:

| Layer (type)   | Output Shape | Param # |
| ------------- | ------------- | ------------- |
|  conv2d_1 (Conv2D)  | (None, 148, 148, 32)| 896  |
| max_pooling2d_1 (MaxPooling2)  | (None, 74, 74, 32)  | 0  |
| conv2d_2 (Conv2D)  | (None, 72, 72, 64)  | 18496  |
| max_pooling2d_2 (MaxPooling2)  | (None, 36, 36, 64)  | 0  |
| conv2d_3 (Conv2D)  | (None, 34, 34, 128)  | 73856  |
| max_pooling2d_3 (MaxPooling2)  | (None, 17, 17, 128)  | 0  |
| conv2d_4 (Conv2D)  | (None, 15, 15, 256)  | 295168  |
| max_pooling2d_4 (MaxPooling2)  | (None, 7, 7, 256)  | 0  |
| flatten_1 (Flatten)  | (None, 12544)  | 0  |
| dropout_1 (Dropout)  | (None, 12544)  | 0  |
| dense_1 (Dense)  | (None, 256)  | 3211520  |
| dense_2 (Dense)  | (None, 6)  | 1542  |



##### Gray-Scale Model Sammary:

| Layer (type)   | Output Shape | Param # |
| ------------- | ------------- | ------------- |
|  conv2d_1 (Conv2D)  | (None, 148, 148, 32)| 320  |
| max_pooling2d_1 (MaxPooling2)  | (None, 74, 74, 32)  | 0  |
| conv2d_2 (Conv2D)  | (None, 72, 72, 64)  | 18496  |
| max_pooling2d_2 (MaxPooling2)  | (None, 36, 36, 64)  | 0  |
| conv2d_3 (Conv2D)  | (None, 34, 34, 128)  | 73856  |
| max_pooling2d_3 (MaxPooling2)  | (None, 17, 17, 128)  | 0  |
| conv2d_4 (Conv2D)  | (None, 15, 15, 256)  | 295168  |
| max_pooling2d_4 (MaxPooling2)  | (None, 7, 7, 256)  | 0  |
| flatten_1 (Flatten)  | (None, 12544)  | 0  |
| dropout_1 (Dropout)  | (None, 12544)  | 0  |
| dense_1 (Dense)  | (None, 128)  | 1605760  |
| dense_2 (Dense)  | (None, 6)  | 774  |



### Methods:
-------------
We experimented with two types of images to see how the model work and what exactly it learns, first we take the image as it is with 3 color channels, and then we experemented with 1 color channel images (Gray-Scale).
And as expected the model learns different  patterns in each approach.


### Data visualisation
-------------
To see how the model works and what exactly learns we choose to visualiz intermediate  activations that  consists of  displaying  the  feature  maps  that  are output by various convolution and pooling layers in a network, given a certain input (the  output  of  a  layer  is  often  called  its  activation,  the  output  of  the  activation  func-tion).  This  gives  a  view  into  how  an  input  is  decomposed  into  the  different  filters learned  by  the  network. 

As showen in Figures 3 and 4, the full-color model learned how to identefy the diseas spots, the gray-scale method in the other hand did not learn how to locate the disease, but insted learned only the shape of the leaf and some patterns in the background.

![](/figures/figure-2.JPG)
> Figure 2: Input image

![](/figures/figure-3.png)
> Figure 3: Full-Color intermediate  activations

![](/figures/figure-4.png)
> Figure 4: Gray-Scale intermediate  activations

### Results:
-------------
We are so proud to show that out best model (Full-Color) achieved an accuracy of 99.84% on a held-out test set, and second best model (Gray-Scale) achieved an accuracy of 95.54%,  Figures 5 and 6 show how the models accuracy progress over epochs.

![](/figures/figure-5.png)
> Figure 5: Full-Color Training and Validation Accuracy

![](/figures/figure-6.png)
> Figure 6: Gray-Scale Training and Validation Accuracy



###Tools:
-------------
- ipython                   7.0.1 
- jupyter                   1.0.0
- Keras                     2.2.4
- matplotlib                3.0.1
- numpy                     1.15.1
- opencv-python             3.4.3.18
- python                    3.6.7
- tensorflow-gpu            1.11.0

