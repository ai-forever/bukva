# Bukva: Russian Sign Language Alphabet Dataset

We introduce a video dataset **Bukva** for Russian Dactyl Recognition task. Bukva dataset size is about **27 GB**, and it contains **3757** RGB videos with more than 101 samples for each RSL alphabet sign, including dynamic ones. The dataset is divided into training set and test set by subject `user_id`. The training set includes 3097 videos, and the test set includes 660 videos. The total video recording time is ~4 hours. About 17% of the videos are recorded in HD format, and 70% of the videos are in FullHD resolution.

![gif](images/bukva.gif)

## Downloads
|                                                                                               Downloads | Size (GB) | Comment                                                              |
|--------------------------------------------------------------------------------------------------------:|:----------|:---------------------------------------------------------------------|
|[dataset](https://n-ws-620xz-pd11.s3pd11.sbercloud.ru/b-ws-620xz-pd11-jux/bukva/bukva.zip) | ~27       | Original HD+, Trimmed HD+, annotations                     |

Annotation file is easy to use and contains some useful columns, see `annotations.tsv` file:

|    | attachment_id | user_id | text | begin | end |  height  | width   | train | length |
|---:|:--------------|:--------|------:|-------:|-------:|-------:|:--------|:------|:----|
|  0 | df5b08f0-...  | 18...   |  А |   36 |     76 | 1920 | 1080    | False    | 150  |
|  1 | 3d2b6a08-...  | 9a...   |  А |   31 |     63 |   1920 | 1080   | True    | 78  |
|  2 | 1915f996-...  | ca...   |  А |   25 |     81 |  1920 | 1080   | True    | 98  |

where:
- `attachment_id` - video file name
- `user_id` - unique anonymized user ID
- `text` - gesture class in Russian Langauge
- `begin` - start of the gesture (for original dataset)
- `end` - end of the gesture (for original dataset)
- `height` - video height
- `width` - video width
- `train` - train or test boolean flag
- `length` - video length

After downloading, you can unzip the archive by running the following command:
```bash
unzip <PATH_TO_ARCHIVE> -d <PATH_TO_SAVE>
```
The structure of the dataset is as follows:
```
├── original
│   ├── 0a1b79d6-...
│   ├── 0a53c65e-...
│   ├── ...
├── trimmed
│   ├── 0a1b79d6-...
│   ├── 0a53c65e-...
│   ├── ...
├── annotations.tsv
```

## Models
We provide some pre-trained models as the baseline for Russian Dactyl Recognition.


| Model Name        | Model Size (MB) | Metric | ONNX|
|-------------------|-----------------|--------|-----|
| MobileNetV2_TSM | 9.1          | 83.6  | [weights](https://n-ws-620xz-pd11.s3pd11.sbercloud.ru/b-ws-620xz-pd11-jux/bukva/models/MobileNetV2_TSM.onnx)|

## Training
To train models from scratch you need to follow the instructions below.

1. Download dataset using link from section [Download](#downloads)
2. Convert annotations to txt format using [constants.py](constants.py)
   ```
   <path_to_video> <class_id>
   <path_to_video> <class_id>
   ...
   ```
3. Using [mmaction2](https://github.com/open-mmlab/mmaction2/tree/main) framework to train models, prepare the environment.
4. Add the path to your train and test txt files to the [training_pipeline_tsm.py](configs/training_pipeline_tsm.py) config.
5. Choose model config from the configs folder and start training.

## Demo
```console
usage: demo.py [-h] -p CONFIG [--mp] [-v] [-l LENGTH]

optional arguments:
  -h, --help            show this help message and exit
  -p CONFIG, --config CONFIG
                        Path to config
  --mp                  Enable multiprocessing
  -v, --verbose         Enable logging
  -l LENGTH, --length LENGTH
                        Deque length for predictions


python demo.py -p <PATH_TO_CONFIG>
```
## Dataset example

![image](images/gestures.png)

## Authors and Credits
- [Kvanchiani Karina](https://www.linkedin.com/in/kvanchiani)
- [Surovtsev Petr](https://www.linkedin.com/in/petros000)
- [Nagaev Alexander](https://www.linkedin.com/in/nagadit/)
- [Petrova Elizaveta](https://www.linkedin.com/in/elizaveta-petrova-248135263/)
- [Kapitanov Alexander](https://www.linkedin.com/in/hukenovs)
