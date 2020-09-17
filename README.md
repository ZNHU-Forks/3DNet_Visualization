# 3D Net Visualization Tools (PyTorch)

## Demo

**This project is to show which space-time region that the model focus on, supported supervised or unsupervised. For an input video, this project will show attention map in video and frames.**

### saved video

Video can't be show here, there are some gif.

**supervised with label**

![gif](https://github.com/FingerRec/3DNet_Visualization/raw/master/resources/supervised.gif)

**unsupervised**

![gif_2](https://github.com/FingerRec/3DNet_Visualization/raw/master/resources/unsupervised.gif)


### saved img

**heatmap**

![heatmap_image](https://github.com/FingerRec/3DNet_Visualization/raw/master/resources/heatmap_1.png)

**focus map**

![focus_image](https://github.com/FingerRec/3DNet_Visualization/raw/master/resources/focusimg_1.png)

### feature map average(without label)
In some case, the real label of video/action can't access. We average all filters
and visualize the heatmap.

![averaage feature map scratch](https://github.com/FingerRec/3DNet_Visualization/raw/master/resources/heatmap_000_sc.png)
![averaage feature map supervised](https://github.com/FingerRec/3DNet_Visualization/raw/master/resources/heatmap_000.png)



## Require:
- pytorch0.4
- opencv
- numpy
- skvideo
- ffmpeg

## Run:
### 1.create pretrain_model dir
```bash
git clone https://github.com/FingerRec/3DNet_Visualization.git
cd 3DNet_Visualization
mkdir pretrained_model
```

### 2.download pretrained model
#### MF-Net
download pretrained MFNet on UCF101 from [google_drive](https://goo.gl/mML2gv) and put it into directory pretrained_model,
which is from [MFNet](https://github.com/cypw/PyTorch-MFNet)
#### I3d
[google_drive](https://drive.google.com/open?id=1feHEql9XhoV2pwXb5dTs4TFuaqsa1ajX)

#### R3D 

[To be add]()

#### C3D
[To be add]()

### 3.run demo

pretrained I3d on HMDB51
```bash
bash scripts/demo.sh
```
#### c3d
```bash
bash scripts/c3d_unsupervised_demo.sh
```

#### r3d
```bash
bash scripts/r3d_unsupervised_demo.sh
```

The generate video and imgs will be put in dir output/imgs and output/video.

Tip: in main.py, if set clip_steps is 1, will generate a video the same length as origin.

### 4.test own video

the details in demo.sh as follow, change --video and --label accorading to your video, please refer to resources/classInd.txt for label information for UCF101 videos.

```bash
python main.py --num_classes 101 \
--classes_list resources/classInd.txt \
--model_weights pretrained_model/MFNet3D_UCF-101_Split-1_96.3.pth \
--video test_videos/v_ApplyEyeMakeup_g01_c01.avi \
--frames_num 16 --label 0 --clip_steps 16 \
--output_dir output
```

Tip:UCF101/HMDB51 dataset is support now, for Kinetics et al. Just download a pretrained model and change --classes_list

## To Do List
- [X] support i3d, mpi3d
- [X] support multi fc layers or full convolution networks
- [X] support feature map average without label
- [X] support r3d and c3d
- [ ] support Slow-Fast Net
- [ ] visualize filters
- [ ] grad-cam

## More information

Support your own network:

> 1. pretrained model; 2. update load_model() in main.py; 3. modify last linear layer name in generate_supervised_cam in action_recognition.py

**Notice C3D and R3D are pretrained on Sports/Kinetics, for better visualization, you may need to finetune these networks on UCF/HMDB**


## Acknowledgment
This project is highly based on [SaliencyTubes](https://github.com/alexandrosstergiou/Saliency-Tubes-Visual-Explanations-for-Spatio-Temporal-Convolutions) 
, [MF-Net](https://github.com/cypw/PyTorch-MFNet) and [st-gcn](https://github.com/yysijie/st-gcn).