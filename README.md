# ADE20k Semantic segmentation with MAE

## Getting started 

1. Install the [mmsegmentation](https://github.com/open-mmlab/mmsegmentation) library and some required packages.

```bash
pip install mmcv-full==1.3.0 mmsegmentation==0.11.0
pip install scipy timm==0.3.2
```

2. Install [apex](https://github.com/NVIDIA/apex) for mixed-precision training

```bash
git clone https://github.com/NVIDIA/apex
cd apex
pip install -v --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./
```

3. Follow the guide in [mmseg](https://github.com/open-mmlab/mmsegmentation/blob/master/docs/dataset_prepare.md) to prepare the ADE20k dataset.


## Fine-tuning for Reproducing Results of MAE ViT-Base

Command:
```
tools/dist_train.sh configs/mae/upernet_mae_base_12_512_slide_160k_ade20k.py 8 --seed 0  --options model.pretrained=https://dl.fbaipublicfiles.com/mae/pretrain/mae_pretrain_vit_base.pth
```

Expected results (paper results: 48.1 mIoU):
```
+--------+-------+-------+-------+
| Scope  | mIoU  | mAcc  | aAcc  |
+--------+-------+-------+-------+
| global | 48.15 | 58.99 | 83.05 |
+--------+-------+-------+-------+
```

## Evaluation

Command format:
```
tools/dist_test.sh  <CONFIG_PATH> <CHECKPOINT_PATH> <NUM_GPUS> --eval mIoU
```

---

## Acknowledgment 

This code is built using the [mmsegmentation](https://github.com/open-mmlab/mmsegmentation) library, [Timm](https://github.com/rwightman/pytorch-image-models) library, the [Swin](https://github.com/microsoft/Swin-Transformer) repository, [XCiT](https://github.com/facebookresearch/xcit), [SETR](https://github.com/fudan-zvg/SETR), [BEiT](https://github.com/microsoft/unilm/tree/master/beit/semantic_segmentation) and the [MAE](https://github.com/facebookresearch/mae) repository.
