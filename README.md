# Denoising using Convolutional Auto-encoders

Run [Denoising_using_CAE.ipynb](https://github.com/NiranthS/Image-denoising-using-Convolutional-Auto-encoders/blob/master/Denoising_using_CAE.ipynb) for implementation. Link to Colab notebook is [here](https://colab.research.google.com/drive/1IBWibQWdS8VA_DJSQcqn2gOGe8isP1XQ?usp=sharing).

Pretrained models are available [here](https://drive.google.com/drive/folders/1p_9WpFwvPebwQ6Sxe_wXxMjaJ0ti9lfJ?usp=sharing)

One of the fundamental challenges in the field of image processing and computer vision is image denoising, where the underlying goal is to estimate the original image by suppressing noise from a noise-contaminated version of the image.It is a well-studied problem in Computer Vision.

<p align="center">
   <img src="https://github.com/NiranthS/Image-denoising-using-Convolutional-Auto-encoders/blob/master/3imgs.png">
</p>

For this task I used a fully Convolutional auto-encoder network for image restoring. The network consists of multiple convolution and transposed convolution(deconvolution) layers, learning mapping from corrupted images to original images. 
* The convolutional layers capture the contents of the image while eliminating the noise.
* The transposed convolution layers upsample the feature maps and recover the details of the image.
## Skip Connections
Skip connections are added from a convolutional layer to its corresponding mirrored transposed convolution layer.
These skip connections exhibit two major advantages:
* They pass image details from convolutional layers to transposed convolution layers which is useful in recovering the clean image.
* They allow signal to be back-propagated directly to the layers at the starting and hence tackling the problem of vanishing gradients.

## Architecture
* The network is fully convolutional and transposed convolution(deconvolution).

<p align="center">
   <img src="https://github.com/NiranthS/Image-denoising-using-Convolutional-Auto-encoders/blob/master/conv_deconv.jpg">
</p>



* The convolutional and transposed convolution layers are symmetric.
* ReLU is used after every convolutional and transposed convolution layer.
* Pooling/unpooling is not used as pooling discards useful image details that are useful for these kind of tasks.
* Skip connections are added from a convolutional layes to its corresponding transposed convolution layer.

## Image denoising
* CIFAR-10 dataset is used in this task.
* An additive Gaussian noise with zero mean and standard deviation of 0.1,0.3,0.5,0.7,1.0 is used in this task.
* Peak signal-to-noise ratio(PSNR) is used to compare the performance. It is given by
 
```python
psnr = 20 * np.log10(max_pixel / np.sqrt(mse))
```
mse- mean square error;
max_pixel- Max value of pixel in an image


## Results
* Network performance on different values of standard deviation:

<p align="center">
   <img src="https://github.com/NiranthS/Image-denoising-using-Convolutional-Auto-encoders/blob/master/psnr_all.png">
</p>

<center>

standard deviation  | PSNR 
--- | --- 
0.1  | 28.33 
0.3  | 22.81  
0.5  | 20.42 
0.7  | 18.98  
1.0  | 15.35 

</center>

Images showing original images(row 1), noisy images(row2), denoised images(row 3) for standard deviation 0.1

<p align="center">
   <img src="https://github.com/NiranthS/Image-denoising-using-Convolutional-Auto-encoders/blob/master/result_01.png">
</p>

Images showing original images(row 1), noisy images(row2), denoised images(row 3) for standard deviation 0.1


More results are shown in the results.pdf







## References
* [Chunwei Tian et al., Deep Learning on Image Denoising: An Overview
](https://arxiv.org/abs/1912.13171)
* [Xiao-Jiao Mao et al., Image Restoration Using Convolutional Auto-encoders with Symmetric Skip Connections](https://arxiv.org/pdf/1606.08921.pdf)

