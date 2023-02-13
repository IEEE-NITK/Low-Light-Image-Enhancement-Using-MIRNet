# Low-Light-Image-Enhancement-Using-MIRNet
The project entails two main objectives: to understand the entire architecture of the underlying neural network, and to implement a deep learning based image processing algorithm on an embedded device, namely the Arduino Nano 33 BLE Sense.


Updates:

MIRNet_v1.ipynb - A full working pipeline of the MIRNet model

tf_lite_convert.ipynb - Code to convert tf code to tf_lite

## Introduction
Recently CNNs(Convolutional Neural Networks) have played a key role in various image processing tasks.Existing CNN-based methods typically operate either on full-resolution or on progressively low-resolution representations.In the former case, spatially precise but contextually less robust results are achieved, while in the latter case, semantically reliable but spatially less accurate outputs are generated. MIRNet Architecture has been designed in such a manner that it achieve both the goals collectively: **Maintaining spatially precise high-resolution representations through the entire network and receive strong contextual information from low resolution representations.** We have adopted the MIRNet architecture for this project and have referred to a research paper for the same.

## Technologies Used
1. Python
2. TensorFlow
3. Arduino
4. TensorFlow Lite

## MIRNet Architecture
The core of the MIRNet Architecture is a multi-scale residual block containing several key elements: <br>
(a) parallel multi-resolution convolution streams for extracting multi-scale features.<br>
(b) information exchange across the multi-resolution streams.<br>
(c) spatial and channel attention mechanisms for capturing contextual information.<br>
(d) attention based multi-scale feature aggregation.

![MIRNet Arch](https://user-images.githubusercontent.com/122466008/218511835-13eee4cc-252b-40b6-aeaf-b6e7c6c9bad0.jpg)
<p align="center">Framework of the MIRNet Architecture</p>

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

