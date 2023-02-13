# YOLOv5-v6.1
YOLOv5🚀是一个在COCO数据集上预训练的目标检测模型，代表了<a href="https://ultralytics.com">Ultralytics公司</a>对未来视觉AI方法的开源研究，该模型结合了在数千小时的研究和开发中吸取的经验教训和最佳实践，目前被广泛应用于计算机视觉领域。本仓库在原有YOLOV5（版本为v6.1）的基础上进行修改，用于面向智能座舱场景下的目标检测（如：乘员数量检测、贵重物品遗留检测、安全带检测等）。


## YOLOv5教程

有关YOLOv5模型训练、测试、部署的完整教程，请参阅： [YOLOv5 官方教程](https://docs.ultralytics.com) 。

## 快速使用指南

### 环境安装

**环境要求：**

- [**Python>=3.7.0**](https://www.python.org/)
- [**PyTorch>=1.7**](https://pytorch.org/get-started/locally/)

**安装步骤：** 克隆仓库、安装requirements.txt中的依赖库（建议使用Anaconda部署环境）。

```shell
git clone https://github.com/Allenpandas/yolov5-v6.1.git  # clone
cd yolov5-v6.1
pip install -r requirements.txt  # install
```

### 模型推理

运行根目录下的`detect.py`文件进行模型推理，推理结果保存在`runs/detect`目录下。

```shell
python detect.py
```

## 扩展阅读

YOLOv5系列各个模型比较，如下图所示：

<p align="left"><img width="800" src="https://user-images.githubusercontent.com/26833433/155040763-93c22a27-347c-4e3c-847a-8094621d3f4e.png"></p>
<details>


<p align="left"><img width="800" src="https://user-images.githubusercontent.com/26833433/155040757-ce0934a3-06a6-43dc-a979-2edbbd69ea0e.png"></p>

<details>
  <summary>Figure Notes (click to expand)</summary>

* **COCO AP val** denotes mAP@0.5:0.95 metric measured on the 5000-image [COCO val2017](http://cocodataset.org) dataset over various inference sizes from 256 to 1536.
* **GPU Speed** measures average inference time per image on [COCO val2017](http://cocodataset.org) dataset using a [AWS p3.2xlarge](https://aws.amazon.com/ec2/instance-types/p3/) V100 instance at batch-size 32.
* **EfficientDet** data from [google/automl](https://github.com/google/automl) at batch size 8.
* **Reproduce** by `python val.py --task study --data coco.yaml --iou 0.7 --weights yolov5n6.pt yolov5s6.pt yolov5m6.pt yolov5l6.pt yolov5x6.pt`
</details>

### Pretrained Checkpoints

[assets]: https://github.com/ultralytics/yolov5/releases

[TTA]: https://github.com/ultralytics/yolov5/issues/303

|Model |size<br><sup>(pixels) |mAP<sup>val<br>0.5:0.95 |mAP<sup>val<br>0.5 |Speed<br><sup>CPU b1<br>(ms) |Speed<br><sup>V100 b1<br>(ms) |Speed<br><sup>V100 b32<br>(ms) |params<br><sup>(M) |FLOPs<br><sup>@640 (B)
|---                    |---  |---    |---    |---    |---    |---    |---    |---
|[YOLOv5n][assets]      |640  |28.0   |45.7   |**45** |**6.3**|**0.6**|**1.9**|**4.5**
|[YOLOv5s][assets]      |640  |37.4   |56.8   |98     |6.4    |0.9    |7.2    |16.5
|[YOLOv5m][assets]      |640  |45.4   |64.1   |224    |8.2    |1.7    |21.2   |49.0
|[YOLOv5l][assets]      |640  |49.0   |67.3   |430    |10.1   |2.7    |46.5   |109.1
|[YOLOv5x][assets]      |640  |50.7   |68.9   |766    |12.1   |4.8    |86.7   |205.7
|                       |     |       |       |       |       |       |       |
|[YOLOv5n6][assets]     |1280 |36.0   |54.4   |153    |8.1    |2.1    |3.2    |4.6
|[YOLOv5s6][assets]     |1280 |44.8   |63.7   |385    |8.2    |3.6    |16.8   |12.6
|[YOLOv5m6][assets]     |1280 |51.3   |69.3   |887    |11.1   |6.8    |35.7   |50.0
|[YOLOv5l6][assets]     |1280 |53.7   |71.3   |1784   |15.8   |10.5   |76.8   |111.4
|[YOLOv5x6][assets]<br>+ [TTA][TTA]|1280<br>1536 |55.0<br>**55.8** |72.7<br>**72.7** |3136<br>- |26.2<br>- |19.4<br>- |140.7<br>- |209.8<br>- 

<details>
  <summary>Table Notes (click to expand)</summary>

* All checkpoints are trained to 300 epochs with default settings. Nano and Small models use [hyp.scratch-low.yaml](https://github.com/ultralytics/yolov5/blob/master/data/hyps/hyp.scratch-low.yaml) hyps, all others use [hyp.scratch-high.yaml](https://github.com/ultralytics/yolov5/blob/master/data/hyps/hyp.scratch-high.yaml).
* **mAP<sup>val</sup>** values are for single-model single-scale on [COCO val2017](http://cocodataset.org) dataset.<br>Reproduce by `python val.py --data coco.yaml --img 640 --conf 0.001 --iou 0.65`
* **Speed** averaged over COCO val images using a [AWS p3.2xlarge](https://aws.amazon.com/ec2/instance-types/p3/) instance. NMS times (~1 ms/img) not included.<br>Reproduce by `python val.py --data coco.yaml --img 640 --task speed --batch 1`
* **TTA** [Test Time Augmentation](https://github.com/ultralytics/yolov5/issues/303) includes reflection and scale augmentations.<br>Reproduce by `python val.py --data coco.yaml --img 1536 --iou 0.7 --augment`

</details>

