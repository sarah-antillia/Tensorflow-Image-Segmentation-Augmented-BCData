<h2>Tensorflow-Image-Segmentation-Augmented-BCData (2024/07/04)</h2>

This is the first experiment of Image Segmentation for BCData (A Large-Scale Dataset and Benchmark for Cell Detection and Counting 
) Images based on
the <a href="https://github.com/sarah-antillia/Tensorflow-Image-Segmentation-API">Tensorflow-Image-Segmentation-API</a>, and
<a href="https://drive.google.com/file/d/1J62EHi0JLDfL-lVPkN_W7KXaeOEVOrWC/view?usp=sharing">
BCData-ImageMask-Dataset-V1.zip</a>
, which was derived by us from the original <a href="https://drive.google.com/file/d/16W04QOR1E-G3ifc4061Be4eGpjRYDlkA/view?usp=sharing">BCData.zip</a>.
<br><br>

On BCData-ImageMask-Dataset, please refer to the repository <a href="https://github.com/sarah-antillia/ImageMask-Dataset-BCData">ImageMask-Dataset-BCData</a>.
As mentioned in the repository, the original h5 annotation files of BCData contain many points representing the center-like points of 
the cells, rather than polygons surrounding the whole cells. 
Consequently, all mask files in the BCData-ImageMask-Dataset were automatically generated by drawing white filled circles centered 
on these points defined in the h5 annotation files. While these masks are not precise and are considered pseudo annotations, 
they can still be used as the first step to train a BCData segmentation model.<br>
Please see also <a href="https://github.com/sarah-antillia/ImageMask-Dataset-BCData/blob/main/H5AnnotationParser.py">H5AnnotationParser.py</a>.<br>
  
 
<br>
<hr>
<b>Actual Image Segmentation for 640x640 images</b><br>
As shown below, the <b>Circled pointwise masks</b>, which were created by us using  
<a href="https://github.com/sarah-antillia/ImageMask-Dataset-BCData/blob/main/ImageMaskDatasetGenerator.py">
ImageMaskDatasetGenerator.py</a>, are not precise filled polygonal annotations for the black cells in the <b>Input images</b>.
However, the white regions of the inferred masks predicted by our segmentation model look slightly better approximations than the pointwise masks 
to the black cells in the images. 
Probably, we are able to replace the original pseudo annotations (circled pointwise masks) with the inferred masks   
to get more precise annotations.<br>
  
   
<br>
<table>
<tr>
<th>Input image</th>
<th>Circled pointwise mask</th>
<th>Prediction: inferred_mask</th>
</tr>
<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/images/3.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/masks/3.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test_output/3.jpg" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/images/5.jpg" width="320" height="auto"></td>

<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/masks/5.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test_output/5.jpg" width="320" height="auto"></td>
</tr>
</table>

<hr>
<br>
In this experiment, we used the simple UNet Model 
<a href="./src/TensorflowUNet.py">TensorflowSlightlyFlexibleUNet</a> for this BCData Segmentation.<br>
As shown in <a href="https://github.com/sarah-antillia/Tensorflow-Image-Segmentation-API">Tensorflow-Image-Segmentation-API</a>.
you may try other Tensorflow UNet Models:<br>

<li><a href="./src/TensorflowSwinUNet.py">TensorflowSwinUNet.py</a></li>
<li><a href="./src/TensorflowMultiResUNet.py">TensorflowMultiResUNet.py</a></li>
<li><a href="./src/TensorflowAttentionUNet.py">TensorflowAttentionUNet.py</a></li>
<li><a href="./src/TensorflowEfficientUNet.py">TensorflowEfficientUNet.py</a></li>
<li><a href="./src/TensorflowUNet3Plus.py">TensorflowUNet3Plus.py</a></li>
<li><a href="./src/TensorflowDeepLabV3Plus.py">TensorflowDeepLabV3Plus.py</a></li>

<br>


<h3>1. Dataset Citation</h3>
<a href="https://link.springer.com/chapter/10.1007/978-3-030-59722-1_28">
BCData: A Large-Scale Dataset and Benchmark for Cell Detection and Counting</a><br>
Medical Image Computing and Computer Assisted Intervention – MICCAI 2020, 2020, Volume 12265<br>
ISBN : 978-3-030-59721-4<br>

Zhongyi Huang, Yao Ding, Guoli Song, Lin Wang, Ruizhe Geng, Hongliang He, Shan Du, Xia Liu, <br>
Yonghong Tian, Yongsheng Liang, S. Kevin Zhou & Jie Chen<br>

<br>

<h3>
<a id="2">
2 BCData ImageMask Dataset
</a>
</h3>
 If you would like to train this BCData Segmentation model by yourself,
 please download the dataset from the google drive 
<a href="https://drive.google.com/file/d/1J62EHi0JLDfL-lVPkN_W7KXaeOEVOrWC/view?usp=sharing">
BCData-ImageMask-Dataset-V1.zip</a>
<br>
<br>

Please expand the downloaded ImageMaskDataset and place them under <b>./dataset</b> folder to be
<pre>
./dataset
└─BCData
    ├─test
    │   ├─images
    │   └─masks
    ├─train
    │   ├─images
    │   └─masks
    └─valid
        ├─images
        └─masks
</pre>
<br>

<b>BCData Dataset Statistics</b><br>
<img src ="./projects/TensorflowSlightlyFlexibleUNet/BCData/BCData-ImageMask-Dataset-V1_Statistics.png" width="512" height="auto"><br>
<br>
As shown above, the number of images of train and valid dataset is not necessarily large. Therefore, probably an online augmentation strategy to
train this model may be effective to improve segmentation accuracy.
<br>

<br>
<b>Train_images_sample</b><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/asset/train_images_sample.png" width="1024" height="auto">
<br>
<b>Train_masks_sample</b><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/asset/train_masks_sample.png" width="1024" height="auto">
<br>

<h3>
4 Train TensorflowUNet Model
</h3>
 We have trained BCData TensorflowUNet Model by using the following
<a href="./projects/TensorflowSlightlyFlexibleUNet/BCData/train_eval_infer.config"> <b>train_eval_infer.config</b></a> file. <br>
Please move to <i>./projects/TensorflowSlightlyFlexibleUNet/BCData/</i> and run the following bat file.<br>
<pre>
>1.train.bat
</pre>
, which simply runs the following command.<br>
<pre>
>python ../../../src/TensorflowUNetTrainer.py ./train_eval_infer.config
</pre>
<pre>
; train_eval_infer.config
; 2024/07/04 (C) antillia.com

[model]
model         = "TensorflowUNet"
generator     = True
image_width    = 640
image_height   = 640
image_channels = 3
input_normalize = False
normalization  = False
num_classes    = 1
base_filters   = 16
base_kernels   = (5,5)
num_layers     = 7
dropout_rate   = 0.05
learning_rate  = 0.0001
clipvalue      = 0.5
dilation       = (2,2)
;loss           = "bce_iou_loss"
loss           = "bce_dice_loss"
metrics        = ["binary_accuracy"]
show_summary   = False

[train]
epochs        = 100
batch_size    = 2
steps_per_epoch  = 200
validation_steps = 80
patience      = 10

;metrics       = ["iou_coef", "val_iou_coef"]
metrics       = ["binary_accuracy", "val_binary_accuracy"]
model_dir     = "./models"
eval_dir      = "./eval"
image_datapath = "../../../dataset/BCData/train/images/"
mask_datapath  = "../../../dataset/BCData/train/masks/"

;Inference execution flag on epoch_changed
epoch_change_infer     = True

; Output dir to save the inferred masks on epoch_changed
epoch_change_infer_dir =  "./epoch_change_infer"

;Tiled-inference execution flag on epoch_changed
epoch_change_tiledinfer     = False

; Output dir to save the tiled-inferred masks on epoch_changed
epoch_change_tiledinfer_dir =  "./epoch_change_tiledinfer"

; The number of the images to be inferred on epoch_changed.
num_infer_images       = 1
create_backup  = False

learning_rate_reducer = True
reducer_factor     = 0.3
reducer_patience   = 4
save_weights_only  = True

[eval]
image_datapath = "../../../dataset/BCData/validation/images/"
mask_datapath  = "../../../dataset/BCData/validation/masks/"

[test] 
image_datapath = "../../../dataset/BCData/test/images/"
mask_datapath  = "../../../dataset/BCData/test/masks/"

[infer] 
images_dir    = "./mini_test/images"
output_dir    = "./mini_test_output"
merged_dir    = "./mini_test_output_merged"
;blur          = True

[tiledinfer] 
overlapping   = 128
images_dir    = "./mini_test/Metaplastic/images"
output_dir    = "./tiled_mini_test_output"
merged_dir    = "./tiled_mini_test_output_merged"
bitwise_blending = False

;binarize      = True
mask_colorize = True


[segmentation]
colorize      = False
black         = "black"
white         = "green"
blursize      = None

[mask]
blur      = True
blur_size = (3,3)
binarize  = False
;threshold = 128
threshold = 80

[generator]
debug        = False
augmentation = True

[augmentor]
vflip    = True
hflip    = True
rotation = True
angles   = [30, 60, 90, 120, 150, 180, 210, 240, 270, 300, 330]
shrinks  = [0.6, 0.8]
shears   = [0.1]

deformation = True
distortion  = True
sharpening  = False
brightening = False
; 2024/07/04
barrdistortion = True

[deformation]
alpah     = 1300
sigmoids  = [8.0]

[distortion]
gaussian_filter_rsigma= 40
gaussian_filter_sigma = 0.5
distortions           = [0.02, 0.03]

[barrdistortion]
radius = 0.3
amount = 0.3
centers =  [(0.3, 0.3), (0.7, 0.3), (0.5, 0.5), (0.3, 0.7), (0.7, 0.7)]

[sharpening]
k        = 1.0

[brightening]
alpha  = 1.2
beta   = 10  
</pre>
In this configuration file above, we added the following parameters to enable <b>epoch_change_infer</b> callback in [train] section.<br>
<pre>
[train]
;Inference execution flag on epoch_changed
epoch_change_infer     = True
; Output dir to save the inferred masks on epoch_changed
epoch_change_infer_dir =  "./epoch_change_infer"

; The number of the images to be inferred on epoch_changed.
num_infer_images       = 1
</pre>

By using this callback, on every epoch_change, the inference procedures can be called
 for an image in <b>mini_test</b> folder.<br><br>
<b>Epoch_change_inference output</b><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/asset/epoch_change_infer.png" width="1024" height="auto"><br>
<br>
<br>
The training process has just been stopped at epoch 35 by an early-stopping callback as shown below.<br><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/asset/train_console_output_at_epoch_35.png" width="720" height="auto"><br>
<br>
<br>
<a href="./projects/TensorflowSlightlyFlexibleUNet/BCData/eval/train_metrics.csv">train_metrics.csv</a><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/eval/train_metrics.png" width="520" height="auto"><br>

<br>
<a href="./projects/TensorflowSlightlyFlexibleUNet/BCData/eval/train_losses.csv">train_losses.csv</a><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/eval/train_losses.png" width="520" height="auto"><br>
<br>

<h3>
5 Evaluation
</h3>
Please move to a <i>./projects/TensorflowSlightlyFlexibleUNet/BCData</i> folder,<br>
and run the following bat file to evaluate TensorflowUNet model for BCData.<br>
<pre>
./2.evaluate.bat
</pre>
<pre>
python ../../../src/TensorflowUNetEvaluator.py ./train_eval_infer_aug.config
</pre>
Evaluation console output:<br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/asset/evaluate_console_output_at_epoch_35.png" width="720" height="auto">
<br><br>
<a href="./projects/TensorflowSlightlyFlexibleUNet/BCData/evaluation.csv">evaluation.csv</a><br>
The loss (bce_dice_loss) for the <a href="./dataset/BCData/test">test</a> dataset is not so low.<br>
<pre>
loss,0.2234
binary_accuracy,0.9264
</pre>

<br>
<h3>
6 Inference
</h3>
Please move to a <i>./projects/TensorflowSlightlyFlexibleUNet/BCData</i> folder
, and run the following bat file to infer segmentation regions for the images 
in <a href="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/images"><b>mini_test/images</b></a> by the Trained-TensorflowUNet model for Camelyon.<br>
<pre>
./3.infer.bat
</pre>
<pre>
python ../../../src/TensorflowUNetInferencer.py ./train_eval_infer_aug.config
</pre>
The <a href="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/"><b>mini_test</b></a>
folder contains some large image and mask files taken from the original BCSS dataset.<br><br>
<hr>
<b>mini_test_images</b><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/asset/mini_test_images.png" width="1024" height="auto"><br>
<br>
<b>mini_test_mask(circled-pointwise-mask)</b><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/asset/mini_test_masks.png" width="1024" height="auto"><br>

<hr>
<b>inferred mini_test masks</b><br>
<img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/asset/mini_test_output.png" width="1024" height="auto"><br>
<br>


<hr>
<b>Enlarged Masks Comparison</b><br>

<table>
<tr>
<th>Image</th>
<th>Mask (ground_truth)</th>
<th>Inferred-mask</th>
</tr>

<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/images/0.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/masks/0.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test_output/0.jpg" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/images/3.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/masks/3.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test_output/3.jpg" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/images/7.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/masks/7.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test_output/7.jpg" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/images/11.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/masks/11.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test_output/11.jpg" width="320" height="auto"></td>
</tr>

<tr>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/images/15.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test/masks/15.jpg" width="320" height="auto"></td>
<td><img src="./projects/TensorflowSlightlyFlexibleUNet/BCData/mini_test_output/15.jpg" width="320" height="auto"></td>
</tr>
</table>
<br>

<h3>
References
</h3>
<b>1. BCData: A Large-Scale Dataset and Benchmark for Cell Detection and Counting </b><br>
<pre>
https://sites.google.com/view/bcdataset
</pre>

<br>
<b>2. Image-MaskDataset-BCData</b><br>
Toshiyuki Arai @antillia.com <br>
<pre>

https://github.com/sarah-antillia/ImageMask-Dataset-BCData
</pre>

