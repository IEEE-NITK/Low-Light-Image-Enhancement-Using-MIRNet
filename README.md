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
Let 𝐈 be an Image of dimensions ℝ<sup>HxWx3</sup>. The network first applies a convolutional layer to extract low-level features 𝐗<sub>𝐎</sub> ∈ ℝ<sup>HxWxC</sup>. Next, the feature maps 𝐗<sub>𝐎</sub> to pass through N number of recursive residual groups (RRGs), which yield deep features 𝐗<sub>𝐝</sub> ∈ ℝ<sup>HxWxC</sup>. RRG contains several multi-scale residual blocks. In the next step we apply one more convolutional layer to deep features 𝐗<sub>𝐝</sub> to obtain a residual image 𝐑 ∈ ℝ<sup>HxWx3</sup>. The restored image is obtained as follows: Î = 𝐈 + 𝐑. We use Charbonnier loss to optimize our proposed network.
$$𝓛(Î,𝐈*) = \sqrt{||Î - 𝐈*||^2 + ε^2}$$
where,<br>
𝐈* denotes the ground-truth image<br>
ε is a constant which we  emperically set to 10<sup>-3</sup> for all the experiments.

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


![SKFF](https://user-images.githubusercontent.com/122466008/218926078-1c142a70-b2d4-4532-8283-63a9c2631ab7.jpg)
<p align="center">Schematic for SKFF</p>

#### **2. Dual Attention Unit(DAU)**
While the SKFF block fuses information across
multi-resolution branches, there is a need for  a mechanism to share information within
a feature tensor, both along the spatial and the channel dimensions. For this purpose we require DAU and the feature recalibration is achieved by using channel and spatial attention mechanisms.<br>
Channel Attention branch exploits the inter-channel relationships of the convolutional feature maps by applying squeeze and excitation operations
<br>
Spatial Attention branch is designed to exploit the inter-spatial dependencies of convolutional features.
![DAU](https://user-images.githubusercontent.com/122466008/218926336-c5a49991-4377-4451-9dfc-99d62e759e1d.jpg)
<p align="center">DAU with channel and spatial attention mechanisms</p>

#### **3. Residual Resizing Modules**
In order to maintain the residual nature of the architecture(refers to the use of skip connections to create residual blocks that allow information to flow directly from one layer to another, bypassing one or more intermediate layers), we introduce residual resizing modules to perform downsampling and upsampling operations.
![RRM](https://user-images.githubusercontent.com/122466008/218926366-73021c4f-e59c-42fb-9bfb-8531ee3db6f4.jpg)
<p align="center">RRMs to perform upsampling and downsampling</p>

## Dataset
For the purpose of image enhancement, the architecture is trained on **LoL** dataset. LoL is created for low-light image enhancement problem. It consists of 485 images for training and 15 images for testing. Each image pair in LoL consists of a low-light input image and its corresponding well-exposed reference image.

## Performance and Results
We tried varying the number of MRBs(Multi-scale Residual Blocks) and RRGs(Recursive Residual Groups) in the MIRNet Architecture and tested their performances.The results are as follows:

Baseline Model: 3 RRGs and 2 MRBs
![Baseline](https://user-images.githubusercontent.com/122466008/227175436-f54a6ecc-076e-4038-a61d-8c890f37507a.jpg)

Model 2: 3 MRBs and 3 RRGs
![image](https://user-images.githubusercontent.com/122466008/227177085-5662a6a2-f33f-4953-9697-23b078c3e6c5.png)

Model 3: 1 MRB and 3 RRGs
![image](https://user-images.githubusercontent.com/122466008/227177414-dc5f5c3b-485d-423c-aa9d-857951acb40a.png)

Model 4: 1 MRB and 1 RRG
![image](https://user-images.githubusercontent.com/122466008/227177600-c76c4cb2-fa21-42ff-bf18-3950a985b700.png)


## References
1. [Learning Enriched Features for Real Image Restoration and Enhancement](https://arxiv.org/pdf/2003.06792.pdf)
2. https://github.com/swz30/MIRNet
3. https://github.com/soumik12345/MIRNet
4. https://keras.io/examples/vision/mirnet/

## Project Mentors:
1. [Pranav Koundinya](https://github.com/pranavmkoundinya)
2. [Ashrith D R](https://github.com/ashrithdr)

## Project Mentees:
1. [Dev Goti](https://github.com/devgoti16)
2. [K V Srinanda](https://github.com/Srinandakv2004)
3. [Shubham Swadi](https://github.com/shubham-swadi)
4. Sushree Shivani Sethi
5. D Jagannadha Reddy

