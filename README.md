# Video Object Segmentation with Re-identification(VS-ReID) Pre-release

<div align="center">
    <img src="resource/pipeline.png">
</div>

This repository holds the codes and models for the paper
> 
**Video Object Segmentation with Re-identification**,
Xiaoxiao Li, Yuankai Qi, Zhe Wang, Kai Chen, Ziwei Liu, Jianping Shi, Ping Luo, Xiaoou Tang, and Chen Change Loy  
*CVPR 2017 Workshop DAVIS Challenge on Video Object Segmentation 2017 (Winning Entry)*, Honolulu, Hawaii.
>
[[Arxiv Preprint](http://arxiv.org/abs/1708.00197)]

## Prerequisites
----------------
- Python3
- [PyTorch](http://pytorch.org/) (Release version 0.4.0)

## Get the code
----------------
Use git to clone this repository

```
git clone https://github.com/lxx1991/VS-ReID.git
```
## Get the data, trained model, and pre-computed results
----------------
VS-Reid experiments on [DAVIS datasets](http://davischallenge.org/). After download, you need to remove the color-map from annotations.

It also needs the optical flow as input.
In our paper, We use [FlowNet2.0](http://github.com/lmb-freiburg/flownet2) to extract the optical flow for the whole dataset.
For each pair of adjacent frames, we extract bidirectional optical flow, named as `i.flo` and `(i+1).rflo`.

Download the test-dev online finetuned [propagation model](https://drive.google.com/file/d/1TcBD1MuB7aRExyM3dvUegU2lrxoRsOJb/view?usp=sharing).

We also provide the pre-computed classification and reid results for our model.

* [classification result](https://drive.google.com/drive/folders/1UHIEnbSPp16FQJI9IwDJnCQ8861MoLIm?usp=sharing)
* [person-reid search result](https://drive.google.com/drive/folders/1peGJwiD6MSpbCNiMj9O_8p50IwzHvhcJ?usp=sharing)
* [object-reid search result](https://drive.google.com/drive/folders/197d8kACJsAwJCQCznE110lH3y7Q9vdbh?usp=sharing)

The classification result is the ImageNet classification score of each foreground object generated by [ResNet-101](https://github.com/KaimingHe/deep-residual-networks)

The person-reid search result is pre-computed by [Person Search](https://github.com/ShuangLI59/person_search), and object-reid search result is generated by a Faster R-CNN detector and retrained "Person Search-Similar" network.


## Documentation
----------------
The directory is structured as follows:

    .
    ├── data
    |   └── DAVIS
    │       ├── Annotations
    |       |   └── ... 
    │       ├── JPEGImages
    |       |   └── ... 
    |       ├── Flow
    │       │   └── 480p
    |       |       ├── aerobatics
    |       |       |   ├── 00000.flo
    |       |       |   ├── 00001.rflo
    |       |       |   ├── 00001.flo
    |       |       |   └── ... 
    |       |       └── ... 
    │       ├── ObjectSearch
    │       │   └── 480p
    |       |       └──test-dev.pkl
    │       ├── PersonSearch
    │       │   └── 480p
    |       |       └──test-dev.pkl
    │       ├── Class
    │       │   └── 480p
    |       |       └──test-dev.pkl      
    │       └── ...
    ├── models                  
    │   └── MP2S.pth.tar
    └── ...

## Usage
----------------
Single gpu
```
python3 davis_test.py test-dev configs/test_config.py --output OUT_DIR_NAME --cache CACHE_DIR_NAME --gpu 0
```

Multiple gpus
```
./run.sh OUT_DIR_NAME CACHE_DIR_NAME GPU_NUM
```

## Citation
Please cite the following paper if you feel this repository useful.
```
@inproceedings{li2017video,
  author    = {Li, Xiaoxiao and Qi, Yuankai and Wang, Zhe and Chen, Kai and Liu, Ziwei and Shi, Jianping and Luo, Ping and Tang, Xiaoou and Loy, Chen Change},
  title     = {Video Object Segmentation with Re-identification},
  booktitle   = {The 2017 DAVIS Challenge on Video Object Segmentation - CVPR Workshops},
  year      = {2017},
}
```

## TODOs
----------------
  - [ ] Update README
  - [ ] ReID evaluation script
  - [ ] Training Code


## Contact
----------------
For any question, feel free to contact
```
Xiaoxiao Li : lxx1991@gmail.com
```