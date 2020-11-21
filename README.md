<i>Star the Repository if it helps you :smile:</i>

# DeblurGAN: Blind Motion Deblurring Using Conditional Adversarial Networks

- [Paper](https://arxiv.org/pdf/1711.07064.pdf)
- [Dataset - GoPro_Large](https://drive.google.com/file/d/1H0PIXvJH4c40pk7ou6nAwoxuR4Qh_Sa2/view)

## Authors

- [Saujas Adarkar](https://github.com/Saujas)
- [Aryan Mehra](https://github.com/aryanmehra1999)
- [Siddhant Khandelwal](https://github.com/siddhantkhandelwal)

## What is Image Deblurring?

Blurry images are caused due to motion of the camera lense, rotational components, or slight movement on the part of the target itself. The blur is modelled by the following equation:

```IB = k(M) * IS + N```

 - IB is the blurry image
 - IS is the sharp image
 - k(M) is the unknown blur chanel 
 - \* is the convolution operation

## DeblurGAN

DeblurGAN is an end-to-end learned method for motion deblurring. It achieves state of the art performance both in structural similarity and visual appearance.

![Results on GoPro_Large Dataset](https://github.com/siddhantkhandelwal/deblur-gan/blob/master/images/result_go_pro_large.png)

### Model Architecture

![GAN Model Architecture](https://github.com/siddhantkhandelwal/deblur-gan/blob/master/images/model-arch.png)

-  It contains two strided convolution blocks, nine residual blocks and two transposed convolution blocks.
- Each ResBlock consists of a convolution layer, instance normalization layer and ReLU activation. Dropout regularization
with a probability of 0.5 is added after the first convolution layer in each ResBlock.
- The critic network is Wasserstein GAN with gradient penalty. The architecture of critic network is identical to PatchGAN. All the convolutional layers except the last are followed by InstanceNorm layer and LeakyReLU with α = 0.2.

## Performance

- We trained for 200 epochs (original implementation was 300 epochs)
- Metrics
  - PSNR
  - SSIM

SSIM and PSNR are image similarity tests. They are used to determine, how much quality is lost with the encoding process. PSNR is an engineering abbreviation for peak signal-to-noise ratio. SSIM stands for structural similarity index and is a more complex test aimed to determine perceivable difference between two images.

Our model's performance

PSNR | SSIM
------------- | -------------
25.4 | 0.8208

## Results

Our model successfully deblurs the images without loss of context and contrast.

![Model's results on GoPro_Large Dataset](https://github.com/siddhantkhandelwal/deblur-gan/blob/master/images/result_model_go_pro_large-1.png)

![Model's results on GoPro_Large Dataset](https://github.com/siddhantkhandelwal/deblur-gan/blob/master/images/result_model_go_pro_large-2.png)

![Model's results on GoPro_Large Dataset](https://github.com/siddhantkhandelwal/deblur-gan/blob/master/images/result_model_go_pro_large-3.png)

## Setup

- Create the environment
  
  - Modify ```prefix``` in environment file to the location where you wish to install the environment
  
  ```bash
  conda env create -f environment.yml
  conda activate deblurgan
  ```

- Launch the jupyter notebook
  
    ```bash
    jupyter notebook
    ```
## Future Prospects

Taking the project forward, some ideas can further be taken up. This includes the use of different networks for the pre-trained weights of the perceptual loss. MobileNetv2, ImageNet or ResNet are just some of the few examples of feature extraction based networks that can be used for the same. Along with that, debluring can be approached with a different perspective using NAS based approaches or other image translatin approaches with CNN based architectures that are encoder decoder based but are much more resource efficient.  

## Referred Implementation

- We referred to [Raphael Meudec's](https://github.com/RaphaelMeudec) Keras implementation for the model's architecture [here](https://github.com/RaphaelMeudec/deblur-gan).
