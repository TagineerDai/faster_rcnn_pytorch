# Faster RCNN with PyTorch

This is a [PyTorch](https://github.com/pytorch/pytorch)
implementation of Faster RCNN. Forked from [longcw/faster_rcnn_pytorch](https://github.com/longcw/faster_rcnn_pytorch).

- [x] Compatible to python3.6 and pytorch 4.0.
- [ ] Refactor as a model module.
- [ ] Json meta configuable.
- [ ] Several datasets.

## Origin doc below

### Installation and demo
0. Install the requirements (you can use pip or [Anaconda](https://www.continuum.io/downloads)):

    ```
    pip3 install menpo pyyaml sympy h5py cython numpy scipy easydict
    ```


1. Clone the Faster R-CNN repository
    ```bash
    git clone git@github.com:tagineerdai/faster_rcnn_pytorch.git
    ```

2. Build the Cython modules for nms and the roi_pooling layer
    ```bash
    cd faster_rcnn_pytorch/faster_rcnn
    ./make.sh
    ```
3. Download the trained model [VGGnet_fast_rcnn_iter_70000.h5](https://drive.google.com/open?id=0B4pXCfnYmG1WOXdpYVFybWxiZFE) 
and put it in to `faster_rcnn_pytorch/model`
3. Run demo `python demo.py`

### Training on Pascal VOC 2007

Follow [this project (TFFRCNN)](https://github.com/CharlesShang/TFFRCNN)
to download and prepare the training, validation, test data 
and the VGG16 model pre-trained on ImageNet. 

Since the program loading the data in `faster_rcnn_pytorch/data` by default,
you can set the data path as following.
```bash
cd faster_rcnn_pytorch
mkdir data
cd data
ln -s $VOCdevkit VOCdevkit2007
```

Then you can set some hyper-parameters in `train.py` and training parameters in the `.yml` file.

Now I got a 0.661 mAP on VOC07 while the origin paper got a 0.699 mAP.
You may need to tune the loss function defined in `faster_rcnn/faster_rcnn.py` by yourself.

### Training with TensorBoard
With the aid of [Crayon](https://github.com/torrvision/crayon),
we can access the visualisation power of TensorBoard for any 
deep learning framework.

To use the TensorBoard, install Crayon (https://github.com/torrvision/crayon)
and set `use_tensorboard = True` in `faster_rcnn/train.py`.

### Evaluation
Set the path of the trained model in `test.py`.
```bash
cd faster_rcnn_pytorch
mkdir output
python test.py
```
