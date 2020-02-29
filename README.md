Egoshots dataset and Semantic Fidelity metric
=====
This repo contains code for our paper "Egoshots, an ego-vision life-logging dataset and semantic fidelity metric to evaluate diversity in image captioning models" accepted at ICLR-2020, MACHINE LEARNING IN REAL LIFE (ML-IRL) workshop.
## Dataset
Egoshots consists of real-life ego-vision images captioned using state of the art image captioning models, and aims at evaluating the robustness, diversity, and sensitivity of these models, as well as providing a real life-logging setting on-the-wild dataset that can aid the task of evaluating real settings. It consists of images from two computer science interns
for 1 month each. Egoshots images are availaible to download at "link" with corresponding captions "link".
## Captioning Egoshots
Unlabelled images of the Egoshots dataset are captioned by exploiting different image captioning models. We limit our work to three models namely:- 
1. [Show, Attend and Tell: Neural Image Caption Generation with Visual Attention](https://arxiv.org/pdf/1502.03044.pdf)
2. [nocaps: novel object captioning at scale](https://arxiv.org/pdf/1812.08658.pdf)
3. [Decoupled Novel Object Captioner](https://arxiv.org/pdf/1804.03803.pdf)
### Show, Attend and Tell: Neural Image Caption Generation with Visual Attention
    cd ShowAttendAndTell
The images to be captioned are put in the folder `test/images/`. The pretrained weigths of the network is extracted from this [link](https://app.box.com/s/xuigzzaqfbpnf76t295h109ey9po5t8p) and extracted in the current folder.

The pre-trained model can be used to caption the dataset by running the following command.
```shell
python main.py --phase=test \
    --model_file='./models/289999.npy' \
    --beam_size=3
```
* All the generated captions are saved in the `test` folder as `results.csv` 
* To caption the Egoshots images and to extract the pre-trained weights the codes are built upon this [repository](https://github.com/coldmanck/show-attend-and-tell).
### nocaps: novel object captioning at scale
    cd nocaps
The image to be captioned are put in the folder `images/`. The pre-trained weights are downloaded using
```shell
./download_models.sh
```
Images are captioned by 
```shell
python noc_captioner.py
```
* The generated captions are saved in the `results` folder.
* The code for captioning the images and pre-trained weights are built upon this [repository](https://github.com/vsubhashini/noc).
### Decoupled Novel Object Captioner
    cd dnoc
The images to be captioned are put in the folder `prepare_data\mscoco\val2014\`. All the images are pre-processed using the following command.
```shell
cd prepare_data
sh step2_detection.sh
sh step3_image_feature_extraction.sh
sh step4_transfer_coco_to_noc.sh
python run.py
cd ..
```
The pre-processed images are captioned using
```shell
python run.py --stage test
```
* The captioned images are saved as `dnoc_ego.txt`.
* The code for preparing the data and captioning the images are built upon this [repository](https://github.com/Yu-Wu/Decoupled-Novel-Object-Captioner)
