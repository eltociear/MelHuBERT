# MelHuBERT: A simplified HuBERT on Mel spectrogram
This is the official implementation of ASRU 2023 accepted paper. \
https://arxiv.org/abs/2211.09944

## Environment 
python=3.9
```
pip install -r requirement.txt
```

## Data Preparing
First, please execute the following command to prepare LibriSpeech 360 horus and paired cluster labels (K-means on log Mel feature)
```
bash preprocess.sh [DATA_DIR]
```

Then, please adjust **datarc.sets** in ./config/config_runner_20ms.yaml and ./config/config_runner_10ms.yaml to [ DATA_DIR/libri-360-data-cluster-pair.csv ]

The mean and std of LibriSpeech 360 hours is saved at DATA_DIR/mean-std.npy
(You won't need it during pre-training, but you might need it when fine-tuning on downstream.)

## Pre-training MelHuBERT from scratch
Execute the following command to pretrain MelHuBERT from scratch with default configuration

- 20 ms frame period:
```
python3 train.py -f 20 -g ./config/config_model_20ms.yaml -c ./config/config_runner_20ms.yaml -n EXP_DIR_PATH 
```
- 10 ms frame period:

```
python3 train.py -f 10 -g ./config/config_model_10ms.yaml -c ./config/config_runner_10ms.yaml -n EXP_DIR_PATH 
```

-f: frame period \
-g: Model config \
-c: Runner config \
-n: The model checkpoints, log file, and the pre-training config you used will be saved at this directory 

## Pretrained Models 
- [MelHuBERT-20ms 360-hour stage 1](https://drive.google.com/file/d/1mSR40Vdl2gT1rlZORleKPb2gcryQHW5m/view?usp=sharing)
- [MelHuBERT-20ms 360-hour stage 2](https://drive.google.com/file/d/11wzYf8u9pXPvQyQU2Wodx79W31Ka2e0Z/view?usp=sharing)
- [MelHuBERT-10ms 360-hour stage 1](https://drive.google.com/file/d/1YZP9nBSRaQ_Z2cFaFLmLkGilEYsEHb2b/view?usp=sharing)
- [MelHuBERT-20ms 100-hour stage 1](https://drive.google.com/file/d/1ppz5w5eTGOL81QjYqwxRwFFmq-hqInD6/view?usp=sharing)
## Extracting feature 
Please execute the following command to extract feature from two example waveforms
```
python3 extract_feature.py -c [CHECKPOINT] -f [FRAME_PERIOD]
```

-c: Model checkpoint path
-f: Choice from 20 or 10 (ms)

## Acknowledgement 
Our implementation of pre-training interface is based on [S3PRL toolkit](https://github.com/s3prl/s3prl)
