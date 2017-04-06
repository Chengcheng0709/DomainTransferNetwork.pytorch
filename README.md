# Domain Transfer Networks (DTN)
- [UNSUPERVISED CROSS-DOMAIN IMAGE GENERATION](https://arxiv.org/abs/1611.02200), ICLR 2017
# Install
- install [pytorch](https://github.com/pytorch/pytorch) and [pytorch.vision](https://github.com/pytorch/vision)

# Run
- **Train function f in source domain(SVHN), first**
 - ```CUDA_VISIBLE_DEVICES=x python main_recog.py --dataset svhn --dataroot /path/to/svhn/extra/ --valDataroot /path/to/svhn/test/ --exp recog_svhn```
 - Resulting model is saved in recog_svhn directory named like netE_epoch_xx.pth
 - You will reach at ~95.xx % of accuracy.


- **And then, train DTN**
 - ```CUDA_VISIBLE_DEVICES=x python main_dtnetgan.py --datasetA svhn --datarootA /path/to/svhn/extra/ --valDatarootA /path/to/svhn/test/ --datasetB mnist --datarootB /path/to/mnist/train/ --valDatarootB /path/to/test/ --netE /path/to/previously/trained/model/netE_epoch_xx.pth --exp S2M --crossentropy```

# Results
- Randomly selected samples in **source domain**
![source domain](https://github.com/taey16/DomainTransferNetwork.pytorch/blob/master/imgs/samples_real_source.png)

- **Domain transferred samples from corresponding inputs**
![generated](https://github.com/taey16/DomainTransferNetwork.pytorch/blob/master/imgs/generated_epoch_00000007_iter00113000.png)

# NOTE
- **We used crossentropy loss computing L_CONST (i.e. Eq.5 in the paper)** which seems to generate better images.
- You can easily change direction of domain transfer such that MNIST to SVHN
- ```CUDA_VISIBLE_DEVICES=x python main_recog.py --dataset mnist --dataroot /path/to/mnist/train/ --valDataroot /path/to/mnist/test/ --exp recog_mnist```
- ```CUDA_VISIBLE_DEVICES=x python main_dtnetgan.py --datasetA mnist --datarootA /path/to/mnist/train/ --valDatarootA /path/to/mnist/test/ --datasetB svhn --datarootB /path/to/svhn/extra/ --valDatarootB /path/to/svhn/test/ --netE /path/to/pretrained/model/netE_epoch_xx.pth --exp M2S```

# Reference
- [dcgan.pytorch](https://github.com/pytorch/examples/tree/master/dcgan)
- FANTASTIC [pytorch](https://github.com/pytorch/pytorch)
