# cnn-fashion-mnist
A repository contains various CNN architecture Deep Learning experiment for Fashion-MNIST Data

## Project Structure
data

## Data Loading

## Training

### Initialization

### Process

## Testing Result

| CNN</br>Architecture | Model </br> size (MB)     | Best  </br> Accuracy (%) |  
|------------  |:-------------:|:-------------:    |
| VGG-16       | 10            |92                 |  
| ResNet-18    | 89.25         |95                 | 
| ResNet-50    | 30            |94.31              | 
| ResNet-152   | 445           |95.52              | 
| DenseNet-121 |  54           | 95.49             |
    
## Optimize Result

### Test Time Augmentation

### Ensemble Method

DenseNet-121  95.52%

ResNet-152 95.39%


Ensemble 95.75%

95.80 % (0.6, 0.4)

# Conclusion

* CNN Architecture component consideration
  * Parameter size
  * Capacity
* Based several training experiment, here the technique can increase accuracy
  * Data Augmentation (Resizing, RandomHorizontalFlip, RandomRotation)
  * asdad
* Efficient
