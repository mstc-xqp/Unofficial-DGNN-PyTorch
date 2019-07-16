# DGNN-PyTorch

(In Progress)

An unofficial PyTorch implementation of the paper "Skeleton-Based Action Recognition with Directed Graph Neural Networks" in CVPR 2019.

- Paper: [PDF](http://openaccess.thecvf.com/content_CVPR_2019/papers/Shi_Skeleton-Based_Action_Recognition_With_Directed_Graph_Neural_Networks_CVPR_2019_paper.pdf)
- Code is based on 2s-AGCN: [GitHub](https://github.com/lshiwjx/2s-AGCN)

## Dependencies

- Python >= 3.5
- scipy >= 1.3.0
- numpy >= 1.16.4
- PyTorch >= 1.1.0
- tensorboardX >= 1.8   (For logging)

## Downloading & Generating Data

### NTU RGB+D

1. The [NTU RGB+D dataset](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Shahroudy_NTU_RGBD_A_CVPR_2016_paper.pdf) can be downloaded from [here](http://rose1.ntu.edu.sg/Datasets/actionRecognition.asp). We'll only need the Skeleton data (~ 5.8G).

2. After downloading, unzip it and put the folder `nturgb+d_skeletons` to `./data/nturgbd_raw/`.

3. Generate the joint dataset first:

```bash
cd data_gen
python3 ntu_gen_joint_data.py
```

Specify the data location if the raw skeletons data are placed somewhere else. The default looks at `./data/nturgbd_raw/`.

4. Then, in `data_gen/`, generate the bone dataset:

```bash
python3 ntu_gen_bone_data.py
```

5. Finally, generate the motion data from joints/bones:

```bash
python3 ntu_gen_motion_data.py
```

The generation scripts look for generated data in previous step. By default they look at `./data`; change dir configs if needed.

### Kinetics

TODO TODO TODO TODO TODO TODO TODO TODO

## Training

### 1st Stream: Spatial

To start training the network with the spatial stream, use the following command:

```bash
python3 main.py --config ./config/<dataset>/train_spatial.yaml
```

Here, `<dataset>` should be one of `nturgbd-cross-subject`, `nturgbd-cross-view`, or `kinetics-skeleton` depending on the dataset/task on which to train the model.

**Note:** At the moment, only `nturgbd-cross-subject` is supported. More config files will be added later, or you could write your own config file.

### 2nd Stream: Motion

Similarly, to train on the motion stream data, do:

```bash
python3 main.py --config ./config/nturgbd-cross-subject/train_motion.yaml
```

and change the config file path for other datasets if needed.

## Testing

### Test individual streams

To test some model weights (by default saved in `./runs/`), do:

```bash
python3 main.py --config ./config/<dataset>/test_spatial.yaml
```

Similarly, change the paths in config file, or change the config files (`<dataset>`) for different datasets as needed.

### Ensemble results

Combine the generated scores with:

```bash
python ensemble.py --datasets <dataset>
```

where `<dataset>` is one of `kinetics`, `ntu/xsub`, `ntu/xview`

## Results

Results are being reproduced...

## TODO

- Try to reproduce results
- Kinetics
    - Handling datasets
    - Config files
- NTU Cross View
    - Config files
