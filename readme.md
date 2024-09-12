# SpikingResformer: Bridging ResNet and Vision Transformer in Spiking Neural Networks

## Installing Dependencies

```bash
pip3 install torch torchvision
pip3 install tensorboard thop cupy-cuda11x timm
```

## spikingjelly

spikingjelly은 pip install spikingjelly 하면 나중에 오류남 

아래와 같이 해주자 

```
git clone https://github.com/fangwei123456/spikingjelly.git
cd spikingjelly
python setup.py install
```


## 대모 코랩 

https://colab.research.google.com/drive/1cBVD9gYJ7Pm8BCnBX4-WOVetNqkxb3tl?usp=sharing



## Usage

### Experiments on ImageNet

To reproduce the experiments on ImageNet in the paper, you need to first organize the dataset as follows

```bash
/path/to/your/dataset
|-- train
|   |-- n01440764
|   |-- n01443537
|   `-- ...
`-- val
    |-- n01440764
    |-- n01443537
    `-- ...
```

Then run the following command to reproduce the experiment of SpikingResformer-S

```bash
torchrun \
    --standalone \
    --nnodes=1 \
    --nproc-per-node=8 \
main.py \
    -c configs/main/spikingresformer_s.yaml \
    --data-path /path/to/your/dataset \
    --output-dir /path/to/your/output \
    ;
```

Experimental setups of SpikingResformer-Ti, M, L can be found in `configs/main`.

### Transfer Learning

Run the following command to transfer the pretrained SpikingResformer-S to CIFAR10

```bash
python \
main.py \
    -c configs/transfer/cifar10.yaml \
    --data-path /path/to/your/dataset \
    --output-dir /path/to/your/output \
    --transfer /path/to/your/checkpoint \
    ;
```

Experimental setups on other datasets can be found in `configs/transfer`.

### Direct Training

Run the following command to directly train SpikingResformer-Ti* on CIFAR10

```bash
python \
main.py \
    -c configs/direct_training/cifar10.yaml \
    --data-path /path/to/your/dataset \
    --output-dir /path/to/your/output \
    ;
```

Experimental setups on other datasets can be found in `configs/direct_training`.

## Citation

```bibtex
@inproceedings{shi2024spikingresformer,
    title={SpikingResformer: Bridging ResNet and Vision Transformer in Spiking Neural Networks}, 
    author={Shi, Xinyu and Hao, Zecheng and Yu, Zhaofei},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
    year={2024}
}
```
