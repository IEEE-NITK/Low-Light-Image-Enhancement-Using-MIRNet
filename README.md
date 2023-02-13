# Low-Light-Image-Enhancement-Using-MIRNet
The project entails two main objectives: to understand the entire architecture of the underlying neural network, and to implement a deep learning based image processing algorithm on an embedded device, namely the Arduino Nano 33 BLE Sense.


Updates:

MIRNet_v1.ipynb - A full working pipeline of the MIRNet model

tf_lite_convert.ipynb - Code to convert tf code to tf_lite

## MIRNet Architecture
Recently CNNs(Convolutional Neural Networks) have played a key role in various image processing tasks.Existing CNN-based methods typically operate either on full-resolution or on progressively low-resolution representations.In the former case, spatially precise but contextually less robust results are achieved, while in the latter case, semantically reliable but spatially less accurate outputs are generated. MIRNet Architecture has been designed in such a manner that it achieve both the goals collectively: **Maintaining spatially precise high-resolution representations through the entire network and receive strong contextual information from low resolution representations.**. We have adopted the MIRNet architecture for this project and have referred to the following research paper for the same:
