# Semantic segmentation reference training scripts

This folder contains reference training scripts for semantic segmentation.
They serve as a log of how to train specific models, as provide baseline
training and evaluation scripts to quickly bootstrap research.

All models have been trained on 8x V100 GPUs.

You must modify the following flags:

`--data-path=/path/to/dataset`

`--nproc_per_node=<number_of_gpus_available>`

## fcn_resnet50
```
torchrun --nproc_per_node=8 train.py --lr 0.02 --dataset coco -b 4 --model fcn_resnet50 --aux-loss --weights-backbone ResNet50_Weights.IMAGENET1K_V1
```

## fcn_resnet101
```
torchrun --nproc_per_node=8 train.py --lr 0.02 --dataset coco -b 4 --model fcn_resnet101 --aux-loss --weights-backbone ResNet101_Weights.IMAGENET1K_V1
```

## deeplabv3_resnet50
```
torchrun --nproc_per_node=8 train.py --lr 0.02 --dataset coco -b 4 --model deeplabv3_resnet50 --aux-loss --weights-backbone ResNet50_Weights.IMAGENET1K_V1
```

## deeplabv3_resnet101
```
torchrun --nproc_per_node=8 train.py --lr 0.02 --dataset coco -b 4 --model deeplabv3_resnet101 --aux-loss --weights-backbone ResNet101_Weights.IMAGENET1K_V1
```

## deeplabv3_mobilenet_v3_large
```
torchrun --nproc_per_node=8 train.py --dataset coco -b 4 --model deeplabv3_mobilenet_v3_large --aux-loss --wd 0.000001 --weights-backbone MobileNet_V3_Large_Weights.IMAGENET1K_V1
```

## lraspp_mobilenet_v3_large
```
torchrun --nproc_per_node=8 train.py --dataset coco -b 4 --model lraspp_mobilenet_v3_large --wd 0.000001 --weights-backbone MobileNet_V3_Large_Weights.IMAGENET1K_V1
```
# NetsPresso Compress Tutorial
## Step 1.  train model
Support models: fcn_resnet50, fcn_resnet101
```
torchrun --nproc_per_node=8 train.py --lr 0.02 --dataset coco -b 4 --model fcn_resnet50 --aux-loss --weights-backbone ResNet50_Weights.IMAGENET1K_V1
```

## Step 2. compress the model
Visit [netspresso.ai](https://netspresso.ai/) and compress the model. You can get step by step guide from [here](https://docs.netspresso.ai/docs/mc-step1-prepare-model).

## Step 3. fine-tune the model
You need to set the compressed model path using `--model` and use `--netspresso` to train the compressed model.
```
torchrun --nproc_per_node=8 train.py --lr 0.002 --dataset coco -b 4 --model path_to_compressed_model_file --aux-loss --netspresso
```