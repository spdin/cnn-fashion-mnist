# cnn-fashion-mnist
A repository contains various CNN architecture Deep Learning experiment for Fashion-MNIST Data

## Introduction
Fashion-MNIST is a dataset of Zalando's article images—consisting of a training set of 60,000 examples and a test set of 10,000 examples. Each example is a 28x28 grayscale image, associated with a label from 10 classes

<p align="center">
<img src="https://cdn-images-1.medium.com/max/1600/1*QQVbuP2SEasB0XAmvjW0AA.jpeg" width="300px" />
 
<small><i>Fashion MNIST Data</i></small>
</p>


## Data Loading
We separate the data become Training set and Testing set based on source

[Fashion-MNIST Dataset](https://github.com/zalandoresearch/fashion-mnist)


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

#### Hyperparameter Tuning
* Learning Rate
* Batch Size
* Number of Epoch

#### Implementation
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

## Testing Result

| CNN</br>Architecture | Model </br> size (MB)     | Best  </br> Accuracy (%) |  
|------------- |:-------------:|:-------------:    |
| VGG-16       | 1030          |93.25                 |  
| ResNet-18    | 89.25         |94.17                 | 
| ResNet-50    | 30            |93.11              | 
| ResNet-152   | 445           |95.39              | 
| DenseNet-121 |  54           | 95.52             |
| DenseNet-161 |  203.24       |  95.42             |
 
 
## Optimize Result

### Test Time Augmentation
Augment the data for testing process. There are two types data, first is original and second is horizontal flip. Inference based averaging two output from augment test data

* Original accuracy = 95.52 %
* After augmented = 95.59 %

### Ensemble Method
For Ensemble the model I use _Bagging_ method, it means we only process all output from several models

<p align="center">
<img src="https://latex.codecogs.com/svg.latex?\Large&space;output=w_1.output_1+w_2.output_2+...+w_n.output_n" />
</p>

Here the result
* Ensemble ResNet-152 + DenseNet-121
    * w<sub>1</sub> = 0.5, w<sub>2</sub> = 0.5
    
      Testing accuracy result is 95.75%
      
    * w<sub>1</sub> = 0.6, w<sub>2</sub> = 0.4
    
      Testing accuracy result is Accuracy 95.80 %

* Ensemble DenseNet-121 + DenseNet-161
    * w<sub>1</sub> = 0.5, w<sub>2</sub> = 0.5
      
      Testing accuracy result is 95.95%
      
    * w<sub>1</sub> = 0.6, w<sub>2</sub> = 0.4
      
      Testing accuracy result is Accuracy 96.01 %
      
    * w<sub>1</sub> = 0.4, w<sub>2</sub> = 0.6
    
      Testing accuracy result is Accuracy 95.86 %      
      
    * w<sub>1</sub> = 0.7, w<sub>2</sub> = 0.3
    
      Testing accuracy result is Accuracy 95.95 %    
      
 * Ensemble DenseNet-121 + DenseNet-161 + ResNet-152    
   * w<sub>1</sub> = 0.33, w<sub>2</sub> = 0.33, w<sub>3</sub> = 0.33 (mean)  
   
     Testing accuracy result is 95.71%
     
   * w<sub>1</sub> = 0.4, w<sub>2</sub> = 0.3, w<sub>3</sub> = 0.3  
   
     Testing accuracy result is 95.71%

# Conclusion

* CNN Architecture component consideration
  * Parameter size
  * Capacity
  
* Based several training experiment, here the technique can increase accuracy
  * Data Augmentation (Resizing, RandomHorizontalFlip, RandomRotation)
  * Ensemble Method
  
* Transfer learning speed up training process and increase testing accuracy
