# cnn-fashion-mnist
A repository contains various CNN architecture Deep Learning experiment for Fashion-MNIST Data

## Introduction
Fashion-MNIST is a dataset of Zalando's article images—consisting of a training set of 60,000 examples and a test set of 10,000 examples. Each example is a 28x28 grayscale image, associated with a label from 10 classes


## Data Loading
We separate the data become Training set and Testing set based on source

https://github.com/zalandoresearch/fashion-mnist

For training purpose, the dataset is augmented with several transform
* Resize
Image resize from 32x32 become 96x96
* RandomHorizontalFlip
Random flip image horizontally
* RandomRotation
Random rotation image with max 10 degree
* GrayScale(3)
Make image from grayscale 1 channel to 3 channel

## Training

### Initialization

Hyperparameter
* Criterion

```python
criterion = nn.CrossEntropyLoss()
```

* Optimizer

```python
optimizer = optim.SGD(net.parameters(), lr=0.01, momentum=0.9)
```
* Scheduler

```python
scheduler = optim.lr_scheduler.StepLR(optimizer, step_size=10, gamma=0.2)
```

### Process


## Testing Result

| CNN</br>Architecture | Model </br> size (MB)     | Best  </br> Accuracy (%) |  
|------------- |:-------------:|:-------------:    |
| VGG-16       | 1030          |92                 |  
| ResNet-18    | 89.25         |95                 | 
| ResNet-50    | 30            |94.31              | 
| ResNet-152   | 445           |95.39              | 
| DenseNet-121 |  54           | 95.52             |
    
## Optimize Result

### Test Time Augmentation
Augment the data for testing process. There are two types data, first is original and second is horizontal flip. Inference based averaging two output from augment test data

* Original accuracy = 95.52 %
* After augmented = 95.59 %

### Ensemble Method
For Ensemble the model I use _Bagging_ method, it means we only process all output from several models

<p align="center">
<img src="https://latex.codecogs.com/svg.latex?\Large&space;output=w_1.output_1+w_2.output_2" />
</p>

* Ensemble ResNet-152 + DenseNet-121
    * w<sub>1</sub> = 0.5, w<sub>2</sub> = 0.5
    
      Testing accuracy result is 95.75%
      
    * w<sub>1</sub> = 0.6, w<sub>2</sub> = 0.4
    
      Testing accuracy result is Accuracy 95.80 %


# Conclusion

* CNN Architecture component consideration
  * Parameter size
  * Capacity
  
* Based several training experiment, here the technique can increase accuracy
  * Data Augmentation (Resizing, RandomHorizontalFlip, RandomRotation)
  * Ensemble Method
  
* Efficient
