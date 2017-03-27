# Temporal-ConvNet
This folder contains codes to train Temporal-ConvNet using the beforehand generated feature vectors for video classification.

---
## Requirement
### Inputs
Temporal-ConvNet takes the **feature vectors** generated by the first stage spatial CNN as input for training. You can generate the features using our codes under "/CNN_Spatial/". You can also download the feature vectors generated by ourselves. (please refer to the Dropbox link below) We followed the first training/testing split from [UCF-101](http://crcv.ucf.edu/data/UCF101.php). If you would like to compare with our results, please use the same training and testing list, as it will affect your overall performance a lot.



* Features for training:
|                 | UCF101          | HMDB51      |
|:-------------:|:-------------:|:---------:|
| RGB      | [sp1](https://www.dropbox.com/s/lxz10lijnh1gb6i/data_feat_train_RGB_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/0pqodpr7btj93m5/data_feat_train_RGB_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/nnljsen7xwxbfm1/data_feat_train_RGB_centerCrop_25f_sp3.t7?dl=0) | [sp1](https://www.dropbox.com/s/qvko5we5ccr16a3/data_feat_train_RGB_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/xna1c9travtgp7p/data_feat_train_RGB_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/nb5rpnc47rs6eia/data_feat_train_RGB_centerCrop_25f_sp3.t7?dl=0) |
| TV-L1       | [sp1](https://www.dropbox.com/s/fug14kobliewgb2/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/ju1v4bymtwbgrdp/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/343oko45z0xauz7/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp3.t7?dl=0)      |  [sp1](https://www.dropbox.com/s/nnzru9rkwaozw32/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/vk53sr16x3mo6pz/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/zt09zfnw2q97qop/data_feat_train_FlowMap-TVL1-crop20_centerCrop_25f_sp3.t7?dl=0)  |



* Features for testing:
|                 | UCF101          | HMDB51      |
|:-------------:|:-------------:|:---------:|
| RGB      | [sp1](https://www.dropbox.com/s/x5slrzhos937bnv/data_feat_test_RGB_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/83hmoaezad8j8mj/data_feat_test_RGB_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/t0lqrehejzjomqu/data_feat_test_RGB_centerCrop_25f_sp3.t7?dl=0) | [sp1](https://www.dropbox.com/s/7vxs1n7id9x98jt/data_feat_test_RGB_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/x630x0x0mf1s1fx/data_feat_test_RGB_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/ot65vzgvz9f37dy/data_feat_test_RGB_centerCrop_25f_sp3.t7?dl=0) |
| TV-L1       | [sp1](https://www.dropbox.com/s/p48731hdg8m0fjo/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/9w0250idyysy99d/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/7xx5aqu0j79y4qt/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp3.t7?dl=0)      | [sp1](https://www.dropbox.com/s/zj4neexynd1lt0g/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp1.t7?dl=0) [sp2](https://www.dropbox.com/s/fvfp1943ctuq6ya/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp2.t7?dl=0) [sp3](https://www.dropbox.com/s/egfwm4rbdqay46q/data_feat_test_FlowMap-TVL1-crop20_centerCrop_25f_sp3.t7?dl=0)   |

You may also need to modify the code in *./data.lua* to the director where you put your feature vector files. (around line 21)
```bash
dirDatabase = '/home/cmhung/Desktop/Dataset/Features/'
dirFeature = dirDatabase..'Res/'
```

---
## Usage
### Training and Testing
```bash
$ qlua run.lua -r 15e-5
```
There are lots of tunable parameters for training. Please check *run.lua*.

#### Outputs
1. In the folder *./results/*, there are training and testing results.
2. *labels.txt*, *prob.txt*: inputs for *namelist.lua* to generate the text file for demo.

### Generate the outputs for demo
```bash
$ th namelist.lua > labels_tcnn.txt
```
The output text file has contains the Top N prediction labels and probabilities.

#### Outputs
*labels_tcnn.txt*: labels and probabilities for demo. (You can change the file name)

---
## Current Performance
We use a 2-layer architecture. Each layer includes one convolution layer and one max-pooling layer. Before the final softmax layer, there are two full-connected linear layers.

### model
* hidden state #: 16 --> 32 --> 256
* convolution kernel size: 3 --> 11
* pooling size: 2 --> 2

### results
* training time: 53 epochs
* training accuracy: 100%
* testing accuracy: **77.47%**

---
#### Contact
[Min-Hung Chen](https://www.linkedin.com/in/chensteven) at <cmhungsteve@gatech.edu>

Last updated: 05/05/2016