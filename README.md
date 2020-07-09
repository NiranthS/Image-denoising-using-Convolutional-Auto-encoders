# Denoising using CNN

Image denoising is a well-studied problem in Computer Vision. For this task I used a fully Convolutional auto-encoder network for image restoring. The network consists of multiple convolution and transposed convolution layers, learning mapping from corrupted images to original images. 
* The convolutional layers capture the contents of the image while eliminating the noise.
* The transposed convolution layers upsample the feature maps and recover the details of the image.
## Skip Connections
Skip connections are added from a convolutional layer to its corresponding mirrored transposed convolution layer.
These skip connections exhibit two major advantages:
* They pass image details from convolutional layers to transposed convolution layers which is useful in recovering the clean image.
* They allow signal to be back-propagated directly to the layers at the starting and hence tackling the problem of vanishing gradients.

## Architecture
* The network is fully convolutional and transposed convolution.

<p align="center">
   <img src="https://github.com/NiranthS/Denoising-using-CNN/blob/master/conv_deconv.jpg">
</p>

<p align="center">
   ** Image showing Convolutional and transposed convolutional layers with skip connections**
</p>

* The convolutional and transposed convolution layers are symmetric.
* ReLU/Leaky ReLU are used after every convolutional and transposed convolution layer.
* Pooling/unpooling is not used as pooling discards useful image details that are useful for these kind of tasks.
* Skip connections are added from a convolutional layes to its corresponding transposed convolution layer.

## Image denoising
* CIFAR-10 dataset is used in this task.
* An additive Gaussian noise with zero mean and standard deviation of 0.1,0.3,0.5 is used in this task.


# Graphs
* Show difference between skip and no skip model
* Show with and without padding
* Different noise levels performance
* PSNR vs epochs


# photos
* different noise levels: original images, noisy images and denoised images






# Blind denoising

