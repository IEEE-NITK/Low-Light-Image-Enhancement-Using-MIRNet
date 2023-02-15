# Low-Light-Image-Enhancement-Using-MIRNet
The project entails two main objectives: to understand the entire architecture of the underlying neural network, and to implement a deep learning based image processing algorithm on an embedded device, namely the Arduino Nano 33 BLE Sense.


Updates:

MIRNet_v1.ipynb - A full working pipeline of the MIRNet model

tf_lite_convert.ipynb - Code to convert tf code to tf_lite

## Introduction
Recently CNNs(Convolutional Neural Networks) have played a key role in various image processing tasks.Existing CNN-based methods typically operate either on full-resolution or on progressively low-resolution representations.In the former case, spatially precise but contextually less robust results are achieved, while in the latter case, semantically reliable but spatially less accurate outputs are generated. MIRNet Architecture has been designed in such a manner that it achieve both the goals collectively: **Maintaining spatially precise high-resolution representations through the entire network and receive strong contextual information from low resolution representations.** We have adopted the MIRNet architecture for this project and have referred to a research paper for the same.

## Technologies Used
[![Tech_Used](https://skills.thijs.gg/icons?i=py,tensorflow,arduino&theme=dark)](https://skills.thijs.gg)

## MIRNet Architecture
The core of the MIRNet Architecture is a multi-scale residual block containing several key elements: <br>
(a) parallel multi-resolution convolution streams for extracting multi-scale features.<br>
(b) information exchange across the multi-resolution streams.<br>
(c) spatial and channel attention mechanisms for capturing contextual information.<br>
(d) attention based multi-scale feature aggregation.

![MIRNet Arch](https://user-images.githubusercontent.com/122466008/218511835-13eee4cc-252b-40b6-aeaf-b6e7c6c9bad0.jpg)
<p align="center">Framework of the MIRNet Architecture</p>

### Overall Pipeline

### Multi-scale Residual Block
The research paper proposes a multi scale residual block which is capable of generating a spatially-precise output by maintaining high-resolution representations, while receiving rich contextual information from low-resolution representations.The MRB consists of multiple (three in this paper) fully-convolutional streams
connected in parallel. It allows information exchange across parallel streams in
order to consolidate the high-resolution features with the help of low-resolution
features, and vice versa. The components of MRB are described as follows:

#### **1. Selective Kernel Feature Fusion(SKFF)**
SKFF module performs dynamic adjustment of receptive fields via two operations: Fuse and Select.The fuse operator generates
global feature descriptors by combining the information from multi-resolution
streams. The select operator uses these descriptors to recalibrate the feature
maps (of different streams) followed by their aggregation.



#### **2. Dual Attention Unit(DAU)**
While the SKFF block fuses information across
multi-resolution branches, there is a need for  a mechanism to share information within
a feature tensor, both along the spatial and the channel dimensions. For this purpose we require DAU and the feature recalibration is achieved by using channel and spatial attention mechanisms.<br>
Channel Attention branch exploits the inter-channel relationships of the convolutional feature maps by applying squeeze and excitation operations
<br>
Spatial Attention branch is designed to exploit the inter-spatial dependencies of convolutional features.


#### **3. Residual Resizing Modules**
In order to maintain the residual nature of the architecture(refers to the use of skip connections to create residual blocks that allow information to flow directly from one layer to another, bypassing one or more intermediate layers), we introduce residual resizing modules to perform downsampling and upsampling operations.

## Dataset
For the purpose of image enhancement, the architecture is trained on **LoL** dataset. LoL is created for low-light image enhancement problem. It consists of 485 images for training and 15 images for testing. Each image pair in LoL consists of a low-light input image and its corresponding well-exposed reference image.

## Performance and Results

## References
1. [Learning Enriched Features for Real Image Restoration and Enhancement](https://arxiv.org/pdf/2003.06792.pdf)
2. https://github.com/swz30/MIRNet
3. https://github.com/soumik12345/MIRNet
4. https://keras.io/examples/vision/mirnet/

## Project Mentors:
1. [Pranav Koundinya](https://github.com/pranavmkoundinya)
2. [Ashrith D R](https://github.com/ashrithdr)

## Project Mentees:
1. Dev Goti
2. [K V Srinanda](https://github.com/Srinandakv2004)
3. [Shubham Swadi](https://github.com/shubham-swadi)
4. Sushree Shivani Sethi
5. D Jagannadha Reddy

