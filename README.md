# Review of Image Captioning Algorithms

# 1. Benchmark Algorithms

Benchmark on COCO with Karpathy's split, as reported in original paper [[Source]](https://cs.stanford.edu/people/karpathy/deepimagesent/):

| Algorithm                         | Year | B4   |METEOR| ROUGE| CIDEr | SPICE| NW   |
| -------------                     |:----:|-----:| ----:|-----:|------:|-----:|-----:|
| Kaparthy                          | 2015 | 23.0 | 19.5 |      | 66.0  |      |      |
| Show attend and tell *            | 2015 | 25.0*| 23.04*|  |  |  |  |
| Semantic Attention [[Source]](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/You_Image_Captioning_With_CVPR_2016_paper.pdf)[[Github]](https://github.com/chapternewscu/image-captioning-with-semantic-attention)| 2016 | 30.4| 24.3|  |  |  |  |
| Knowing When to Look [[Source]](https://github.com/yufengm/Adaptive)| 2017 | 33.2| 26.6|  |108.5  |  |  |
| Self Critical [[Source]](http://openaccess.thecvf.com/content_cvpr_2017/papers/Rennie_Self-Critical_Sequence_Training_CVPR_2017_paper.pdf)| 2017 | 31.9 | 25.5 | 54.3 | 106.3 |  |      |
| Convolutional Image Captioning    | 2018 | 28.1 | 24.1 | 51.9 | 89.0  | 17.1 |      |
| Bottom-Up Top-Down                | 2018 | 36.2 | 27.0 | 56.4 | 113.5 | 20.3 |      |
| Bottom-Up Top-Down, CIDEr loss    | 2018 | **36.3** | **27.7** | **56.9** | **120.1** | **21.4** |      |
| NBT                               | 2018 | 34.9 | 27.4 |      | 108.9 | 20.4 |      |
| Name                              | 2019 |  |  |  |  |  |  |

Controllability [[Source]](https://arxiv.org/abs/1811.10652)

| Algorithm                         | Year | B4   |METEOR| ROUGE| CIDEr | SPICE| NW   |
| -------------                     |:----:|-----:| ----:|-----:|------:|-----:|-----:|
| Kaparthy                          | 2015 | 23.0 | 19.5 |      | 66.0  |      |      |
| NBT                               | 2018 | 34.9 | 27.4 |      | 108.9 | 20.4 |      |
| Show Control and Tell             | 2019 | 20.9 | 24.4 | 52.5 | 193.0 | 45.3 | 0.508|
| Show Control and Tell, CIDEr+NW   | 2019 | 22.3 | 25.6 | 55.3 | **209.7** | 48.5 | 0.649|
| Name                              | 2019 |  |  |  |  |  |  |


*: not sure if use the same split


## 2.1 Experiment Setup
### Dataset
* [MS COCO](http://cocodataset.org/), LANG: `English`.

Following Karpathy's split [[Source]](https://cs.stanford.edu/people/karpathy/deepimagesent/):
You can also download the JSON blobs for all three datasets (but without the VGG CNN features) [here](./data/caption_datasets.zip)(35MB). See our Github repo for more instructions. 

* [Flickr 8k](https://forms.illinois.edu/sec/1713398), LANG: `English`.
* [Flickr 30k](http://shannon.cs.illinois.edu/DenotationGraph/), LANG: `English`.
* [AI Challenger](https://challenger.ai/dataset/caption), LANG: `Chinese`.
* [Visual Genome](http://visualgenome.org/), LANG: `English`.
* [SBUCaptionedPhotoDataset](http://www.cs.virginia.edu/~vicente/sbucaptions/), LANG: `English`.
* [IAPR TC-12](https://www.imageclef.org/photodata), LANG: `English, German and Spanish`.

### Image Captioning Challenge
* [Microsoft COCO Image Captioning](https://competitions.codalab.org/competitions/3221)
* [Google AI Blog: Conceptual Captions](http://ai.googleblog.com/2018/09/conceptual-captions-new-dataset-and.html)


### Metric

[[SPICE]](https://panderson.me/spice/): Semantic Propositional Image Caption Evaluation. Peter Anderson, Basura Fernando, Mark Johnson and Stephen Gould. the European Conference on Computer Vision (ECCV), Amsterdam, the Netherlands, October 2016.

[[CIDEr]](https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Vedantam_CIDEr_Consensus-Based_Image_2015_CVPR_paper.pdf): Consensus-based Image Description Evaluation, CVPR 2015

[[ROUGE-L]](https://en.wikipedia.org/wiki/ROUGE_(metric)): Longest Common Subsequence (LCS) based statistics [[Source]](http://aclweb.org/anthology-new/P/P04/P04-1077.pdf). Longest common subsequence problem takes into account sentence level structure similarity naturally and identifies longest co-occurring in sequence n-grams automatically.

[[METEOR]](https://en.wikipedia.org/wiki/METEOR) (Metric for Evaluation of Translation with Explicit ORdering) is a metric for the evaluation of machine translation output. The metric is based on the harmonic mean of unigram precision and recall, with recall weighted higher than precision.

[[BLEU]](https://en.wikipedia.org/wiki/BLEU) (bilingual evaluation understudy) is an algorithm for evaluating the quality of text which has been machine-translated from one natural language to another. 



---
# 3. Algorithm Summary
## 3.1 General
- Bottom-Up and Top-Down Attention for Image Captioning and Visual Question Answering, 

Peter Anderson, Xiaodong He, Chris Buehler, Damien Teney, Mark Johnson, Stephen Gould, Lei Zhang; The IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2018, pp. 6077-6086

- Convolutional Image Captioning, 

Jyoti Aneja, Aditya Deshpande, Alexander G. Schwing; The IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2018, pp. 5561-5570


- SC: self critical

https://github.com/ruotianluo/self-critical.pytorch

- reconstruction-network

## 3.2 Detection based

- NBT: neural baby talk [[code]](https://github.com/jiasenlu/NeuralBabyTalk)

```
@inproceedings{Lu2018Neural,
author = {Lu, Jiasen and Yang, Jianwei and Batra, Dhruv and Parikh, Devi},
title = {Neural Baby Talk},
booktitle = {CVPR},
year = {2018}
}
```

- Show control and tel [[code]](https://github.com/aimagelab/show-control-and-tell)

```
@inproceedings{cornia2019show,
  title={{Show, Control and Tell: A Framework for Generating Controllable and Grounded Captions}},
  author={Cornia, Marcella and Baraldi, Lorenzo and Cucchiara, Rita},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  year={2019}
}
```

## 3.3 MILA Lab
- SAT: show attend and tell [[code]](https://github.com/karpathy/neuraltalk) [[code]](https://github.com/zsdonghao/Image-Captioning)

https://github.com/sgrvinod/a-PyTorch-Tutorial-to-Image-Captioning

https://github.com/yunjey/show-attend-and-tell

```
@article{Xu2015show,
    title={Show, Attend and Tell: Neural Image Caption Generation with Visual Attention},
    author={Xu, Kelvin and Ba, Jimmy and Kiros, Ryan and Cho, Kyunghyun and Courville, Aaron and Salakhutdinov, Ruslan and Zemel, Richard and Bengio, Yoshua},
    journal={arXiv preprint arXiv:1502.03044},
    year={2015}
} 
```

## 3.4 Feifei Li
- Andrej Karpathy, Li Fei-Fei, Deep Visual-Semantic Alignments for Generating Image Descriptions, CVPR 2015 Paper

https://cs.stanford.edu/people/karpathy/deepimagesent/


# References
[[Git Repo]](https://github.com/zhjohnchan/awesome-image-captioning)
## Survey
* [A Comprehensive Survey of Deep Learning for Image Captioning](https://arxiv.org/abs/1810.04020) - Hossain M et al, `arXiv preprint 2018`.
### Before
* [I2t: Image parsing to text description](https://ieeexplore.ieee.org/abstract/document/5487377/) - Yao B Z et al, `P IEEE 2011`.
* [Im2Text: Describing Images Using 1 Million Captioned Photographs](http://tamaraberg.com/papers/generation_nips2011.pdf) - Ordonez V et al, `NIPS 2011`. [[project web]](http://vision.cs.stonybrook.edu/~vicente/sbucaptions/)
* [Deep Captioning with Multimodal Recurrent Neural Networks](http://arxiv.org/abs/1412.6632) - Mao J et al, `arXiv preprint 2014`.

### 2015
* [Show and Tell: A Neural Image Caption Generator](http://arxiv.org/abs/1411.4555) - Vinyals O et al, `CVPR 2015`. [[code]](https://github.com/karpathy/neuraltalk) [[code]](https://github.com/zsdonghao/Image-Captioning)
* [Deep Visual-Semantic Alignments for Generating Image Descriptions](http://arxiv.org/abs/1412.2306) - Karpathy A et al, `CVPR 2015`. [[project web]](http://cs.stanford.edu/people/karpathy/deepimagesent/) [[code]](https://github.com/karpathy/neuraltalk)
* [Mind’s Eye: A Recurrent Visual Representation for Image Caption Generation](http://www.cs.cmu.edu/~xinleic/papers/cvpr15_rnn.pdf) - Chen X et al, `CVPR 2015`.
* [Long-term Recurrent Convolutional Networks for Visual Recognition and Description](http://arxiv.org/abs/1411.4389) - Donahue J et al, `CVPR 2015`. [[code]](https://github.com/BVLC/caffe/pull/2033) [[project web]](http://jeffdonahue.com/lrcn/)
* [Guiding the Long-Short Term Memory Model for Image Caption Generation](https://arxiv.org/abs/1509.04942) - Jia X et al, `ICCV 2015`.
* [Learning like a Child: Fast Novel Visual Concept Learning from Sentence Descriptions of Images](http://arxiv.org/abs/1504.06692) - Mao J et al, `ICCV 2015`. [[code]](https://github.com/mjhucla/NVC-Dataset)
* [Expressing an Image Stream with a Sequence of Natural Sentences](http://papers.nips.cc/paper/5776-expressing-an-image-stream-with-a-sequence-of-natural-sentences.pdf) - Park C C et al, `NIPS 2015`. [[code]](https://github.com/cesc-park/CRCN)
* [Show, Attend and Tell: Neural Image Caption Generation with Visual Attention](http://arxiv.org/abs/1502.03044) - Xu K et al, `ICML 2015`. [[project]](http://kelvinxu.github.io/projects/capgen.html) [[code]](https://github.com/yunjey/show-attend-and-tell-tensorflow) [[code]](https://github.com/kelvinxu/arctic-captions)
* [Order-Embeddings of Images and Language](http://arxiv.org/abs/1511.06361) - Vendrov I et al, `arXiv preprint 2015`. [[code]](https://github.com/ivendrov/order-embedding)
* [Generating Images from Captions with Attention](http://arxiv.org/abs/1511.02793) - Mansimov E et al, `arXiv preprint 2015`. [[code]](https://github.com/emansim/text2image)
* [Learning FRAME Models Using CNN Filters for Knowledge Visualization](http://arxiv.org/abs/1509.08379) - Lu Y, et al, `arXiv preprint 2015`. [[code]](http://www.stat.ucla.edu/~yang.lu/project/deepFrame/doc/deepFRAME_1.1.zip) 
* [Aligning where to see and what to tell: image caption with region-based attention and scene factorization](http://arxiv.org/abs/1506.06272) - Jin J et al, `arXiv preprint 2015`.

### 2016
* [Grounding of textual phrases in images by reconstruction, ECCV, 2016](http://www.eccv2016.org/files/posters/O-1B-02.pdf)[[code]](https://github.com/kanchen-usc/GroundeR)
* [Image captioning with semantic attention](https://arxiv.org/abs/1603.03925) - You Q et al, `CVPR 2016`. [[code]](https://github.com/chapternewscu/image-captioning-with-semantic-attention)
* [DenseCap: Fully Convolutional Localization Networks for Dense Captioning](http://arxiv.org/abs/1511.07571) - Johnson J et al, `CVPR 2016`. [[code]](https://github.com/jcjohnson/densecap)
* [What value do explicit high level concepts have in vision to language problems?](http://arxiv.org/abs/1506.01144) - Wu Q et al, `CVPR 2016`.
* [SPICE: Semantic Propositional Image Caption Evaluation](http://www.panderson.me/images/SPICE.pdf) - Anderson P et al, `ECCV 2016`. [[code]](https://github.com/peteanderson80/SPICE)
* [Image Captioning with Deep Bidirectional LSTMs](http://arxiv.org/abs/1604.00790) - Wang C et al, `ACMMM 2016`. [[code]](https://github.com/deepsemantic/image_captioning)
* [Multimodal Pivots for Image Caption Translation](http://arxiv.org/abs/1511.02793) - Hitschler J et al, `ACL 2016`.
* [Image Caption Generation with Text-Conditional Semantic Attention](https://arxiv.org/abs/1606.04621) - Zhou L et al, `arXiv preprint 2016`. [[code]](https://github.com/LuoweiZhou/e2e-gLSTM-sc)
* [DeepDiary: Automatic Caption Generation for Lifelogging Image Streams](http://arxiv.org/abs/1608.03819) - Fan C et al, `arXiv preprint 2016`.
* [Learning to generalize to new compositions in image understanding](http://arxiv.org/abs/1608.07639) - Atzmon Y et al, `arXiv preprint 2016`.
* [Generating captions without looking beyond objects](https://arxiv.org/abs/1610.03708) - Heuer H et al, `arXiv preprint 2016`.
* [Bootstrap, Review, Decode: Using Out-of-Domain Textual Data to Improve Image Captioning](https://arxiv.org/abs/1611.05321) - Chen W et al, `arXiv preprint 2016`. [[code]](https://github.com/wenhuchen/Semi-Supervised-Image-Captioning)
* [Recurrent Image Captioner: Describing Images with Spatial-Invariant Transformation and Attention Filtering](https://arxiv.org/abs/1612.04949) - Liu H et al, `arXiv preprint 2016`.
* [Recurrent Highway Networks with Language CNN for Image Captioning](https://arxiv.org/abs/1612.07086) - Gu J et al, `arXiv preprint  2016`.

### 2017
* [Captioning Images with Diverse Objects](http://arxiv.org/abs/1606.07770) - Venugopalan S et al, `CVPR 2017`. [[code]](https://github.com/vsubhashini/noc)
* [Top-down Visual Saliency Guided by Captions](https://arxiv.org/abs/1612.07360) - Ramanishka V et al, `CVPR 2017`. [[code]](https://github.com/VisionLearningGroup/caption-guided-saliency)
* [Self-Critical Sequence Training for Image Captioning](https://arxiv.org/abs/1612.00563) - Steven J et al, `CVPR 2017`. [[code]](https://github.com/ruotianluo/self-critical.pytorch)
* [Dense Captioning with Joint Inference and Visual Context](https://arxiv.org/abs/1611.06949) - Yang L et al, `CVPR 2017`. [[code]](https://github.com/linjieyangsc/densecap)
* [Skeleton Key: Image Captioning by Skeleton-Attribute Decomposition](https://arxiv.org/abs/1704.06972) - Yufei W et al, `CVPR 2017`. [[code]](https://github.com/feiyu1990/Skeleton-key)
* [A Hierarchical Approach for Generating Descriptive Image Paragraphs](https://arxiv.org/abs/1611.06607) - Krause J et al, `CVPR 2017`. [[code]](https://github.com/InnerPeace-Wu/im2p-tensorflow)
* [Deep Reinforcement Learning-based Image Captioning with Embedding Reward](https://arxiv.org/abs/1704.03899) - Ren Z et al, `CVPR 2017`.
* [Incorporating Copying Mechanism in Image Captioning for Learning Novel Objects](https://arxiv.org/abs/1708.05271) - Ting Y et al, `CVPR 2017`.
* [Knowing When to Look: Adaptive Attention via A Visual Sentinel for Image Captioning](https://arxiv.org/abs/1612.01887) - Lu J et al, `CVPR 2017`. [[code]](https://github.com/jiasenlu/AdaptiveAttention)
* [Attend to You: Personalized Image Captioning with Context Sequence Memory Networks](https://arxiv.org/abs/1704.06485) - CC Park et al, `CVPR 2017`. [[code]](https://github.com/cesc-park/attend2u)
* [SCA-CNN: Spatial and channel-wise attention in convolutional networks for image captioning](https://arxiv.org/abs/1611.05594) - Chen L et al, `CVPR 2017`. [[code]](https://github.com/zjuchenlong/sca-cnn.cvpr17)
* [Bidirectional Beam Search: Forward-Backward Inference in Neural Sequence Models for Fill-In-The-Blank Image Captioning](https://arxiv.org/abs/1705.08759) - Qing S et al, `CVPR 2017`.
* [Areas of Attention for Image Captioning](https://arxiv.org/abs/1612.01033) - Pedersoli M et al, `ICCV 2017`.
* [Boosting Image Captioning with Attributes](https://arxiv.org/abs/1611.01646) - Yao T et al, `ICCV 2017`.
* [An Empirical Study of Language CNN for Image Captioning](https://arxiv.org/abs/1612.07086) - Gu J et al, `ICCV 2017`.
* [Improved Image Captioning via Policy Gradient Optimization of SPIDEr](https://arxiv.org/abs/1612.00370) - Liu S et al, `ICCV 2017`.
* [Towards Diverse and Natural Image Descriptions via a Conditional GAN](http://openaccess.thecvf.com/content_ICCV_2017/papers/Dai_Towards_Diverse_and_ICCV_2017_paper.pdf) - Dai B et al, `ICCV 2017`. [[code]](https://github.com/doubledaibo/gancaption_iccv2017)
* [Paying Attention to Descriptions Generated by Image Captioning Models](https://arxiv.org/abs/1704.07434) - Tavakoliy H R et al, `ICCV 2017`.
* [Show, Adapt and Tell: Adversarial Training of Cross-domain Image Captioner](https://arxiv.org/abs/1705.00930) - Chen T H et al, `ICCV 2017`. [[code]](https://github.com/tsenghungchen/show-adapt-and-tell)
* [Image Caption with Global-Local Attention](https://www.aaai.org/ocs/index.php/AAAI/AAAI17/paper/download/14880/14291) - Li L et al, `AAAI 2017`.
* [Reference Based LSTM for Image Captioning](https://aaai.org/ocs/index.php/AAAI/AAAI17/paper/download/14249/14270) - Chen M et al, `AAAI 2017`.
* [Attention Correctness in Neural Image Captioning](https://arxiv.org/abs/1605.09553) - Liu C et al, `AAAI 2017`.
* [Text-guided Attention Model for Image Captioning](https://arxiv.org/abs/1612.03557) - Mun J et al, `AAAI 2017`. [[code]](https://github.com/JonghwanMun/TextguidedATT)
* [Contrastive Learning for Image Captioning](https://arxiv.org/abs/1710.02534) - Dai B et al, `NIPS 2017`. [[code]](https://github.com/doubledaibo/clcaption_nips2017)
* [Show and Tell: Lessons learned from the 2015 MSCOCO Image Captioning Challenge](http://arxiv.org/abs/1609.06647) - Vinyals O et al, `TPAMI 2017`. [[code]](https://github.com/tensorflow/models/tree/master/im2txt)
* [MAT: A Multimodal Attentive Translator for Image Captioning](https://arxiv.org/abs/1702.05658) - Liu C et al, `arXiv preprint  2017`.
* [Actor-Critic Sequence Training for Image Captioning](https://arxiv.org/abs/1706.09601) - Zhang L et al, `arXiv preprint 2017`.
* [What is the Role of Recurrent Neural Networks (RNNs) in an Image Caption Generator?](https://arxiv.org/abs/1708.02043) - Tanti M et al, `arXiv preprint 2017`. [[code]](https://github.com/mtanti/rnn-role)
* [Self-Guiding Multimodal LSTM - when we do not have a perfect training dataset for image captioning](https://arxiv.org/abs/1709.05038) - Xian Y et al, `arXiv preprint 2017`.
* [Phrase-based Image Captioning with Hierarchical LSTM Model](https://arxiv.org/abs/1711.05557) - Tan Y H et al, `arXiv preprint 2017`.
* [Show-and-Fool: Crafting Adversarial Examples for Neural Image Captioning](https://arxiv.org/abs/1712.02051) - Chen H et al, `arXiv preprint 2017`.

### 2018
* [Neural Baby Talk](https://arxiv.org/abs/1803.09845) - Lu J et al, `CVPR 2018`. [[code]](https://github.com/jiasenlu/NeuralBabyTalk)
* [Convolutional Image Captioning](https://arxiv.org/abs/1711.09151) - Aneja J et al, `CVPR 2018`.
* [Learning to Evaluate Image Captioning](https://arxiv.org/abs/1806.06422) - Cui Y et al, `CVPR 2018`. [[code]](https://github.com/richardaecn/cvpr18-caption-eval)
* [Discriminability Objective for Training Descriptive Captions](https://arxiv.org/abs/1803.04376) - Luo R et al, `CVPR 2018`. [[code]](https://github.com/ruotianluo/DiscCaptioning)
* [SemStyle: Learning to Generate Stylised Image Captions using Unaligned Text](https://arxiv.org/abs/1805.07030) - Mathews A et al, `CVPR 2018`.
* [Bottom-Up and Top-Down Attention for Image Captioning and Visual Question Answering](https://arxiv.org/abs/1707.07998) - Anderson P et al, `CVPR 2018`. [[code]](https://github.com/peteanderson80/bottom-up-attention)
* [GroupCap: Group-Based Image Captioning With Structured Relevance and Diversity Constraints
](http://openaccess.thecvf.com/content_cvpr_2018/papers/Chen_GroupCap_Group-Based_Image_CVPR_2018_paper.pdf) - Chen F et al, `CVPR 2018`.
* [Unpaired Image Captioning by Language Pivoting](http://openaccess.thecvf.com/content_ECCV_2018/papers/Jiuxiang_Gu_Unpaired_Image_Captioning_ECCV_2018_paper.pdf) - Gu J et al, `ECCV 2018`.
* [Recurrent Fusion Network for Image Captioning](https://arxiv.org/abs/1807.09986) - Jiang W et al, `ECCV 2018`.
* [Rethinking the Form of Latent States in Image Captioning](http://openaccess.thecvf.com/content_ECCV_2018/papers/Bo_Dai_Rethinking_the_Form_ECCV_2018_paper.pdf) - Dai B et al, `ECCV 2018`. [[code]](https://github.com/doubledaibo/2dcaption_eccv2018)
* [Learning to Guide Decoding for Image Captioning](https://arxiv.org/abs/1804.00887) - Jiang W et al, `AAAI 2018`.
* [Stack-Captioning: Coarse-to-Fine Learning for Image Captioning](https://arxiv.org/abs/1709.03376) - Gu J et al, `AAAI 2018`. [[code]](https://github.com/gujiuxiang/Stack-Captioning)
* [Temporal-difference Learning with Sampling Baseline for Image Captioning](http://eprints.lancs.ac.uk/123576/1/2018_4.pdf) - Chen H et al, `AAAI 2018`.
* [Partially-Supervised Image Captioning](https://arxiv.org/pdf/1806.06004.pdf) - Anderson P et al, `NeurIPS 2018`.
* [A Neural Compositional Paradigm for Image Captioning](https://arxiv.org/pdf/1810.09630.pdf) - Dai B et al, `NeurIPS 2018`.
* [Defoiling Foiled Image Captions](https://arxiv.org/abs/1805.06549) - Wang J et al, `NAACL 2018`.
* [Punny Captions: Witty Wordplay in Image Descriptions](https://arxiv.org/abs/1704.08224) - Chandrasekaran A et al, `NAACL 2018`. [[code]](https://github.com/purvaten/punny_captions)
* [Object Counts! Bringing Explicit Detections Back into Image Captioning](https://arxiv.org/abs/1805.00314) - Aneja J et al, `NAACL 2018`.
* [Conceptual Captions: A Cleaned, Hypernymed, Image Alt-text Dataset For Automatic Image Captioning](http://www.aclweb.org/anthology/P18-1238) - Sharma P et al, `ACL 2018`. [[code]](https://github.com/google-research-datasets/conceptual-captions)
* [Attacking visual language grounding with adversarial examples: A case study on neural image captioning](http://www.aclweb.org/anthology/P18-1241) - Chen H et al, `ACL 2018`. [[code]](https://github.com/IBM/Image-Captioning-Attack)
* [Improved Image Captioning with Adversarial Semantic Alignment](https://arxiv.org/abs/1805.00063) - Melnyk I et al, `arXiv preprint 2018`.
* [Improving Image Captioning with Conditional Generative Adversarial Nets](https://arxiv.org/abs/1805.07112) - Chen C et al, `arXiv preprint 2018`.
* [CNN+CNN: Convolutional Decoders for Image Captioning](https://arxiv.org/abs/1805.09019) - Wang Q et al, `arXiv preprint 2018`.
* [Diverse and Controllable Image Captioning with Part-of-Speech Guidance](https://arxiv.org/abs/1805.12589) - Deshpande A et al, `arXiv preprint 2018`.

### 2019
* [Unsupervised Image Captioning](https://arxiv.org/abs/1811.10787) - Yang F et al, `CVPR 2019`. [[code]](https://github.com/fengyang0317/unsupervised_captioning)
* [Show, Control and Tell: A Framework for Generating Controllable and Grounded Captions](https://arxiv.org/abs/1811.10652v2) - Cornia M et al, `CVPR 2019`. [[code]](https://github.com/aimagelab/show-control-and-tell)
* Meta Learning for Image Captioning - Li N et al, `AAAI 2019`.
* Learning Object Context for Dense Captioning - Li X et al, `AAAI 2019`.
* Hierarchical Attention Network for Image Captioning - Wang W et al, `AAAI 2019`.
* [Deliberate Residual based Attention Network for Image Captioning](https://www.aaai.org/Papers/AAAI/2019/AAAI-GaoLianli3.5390.pdf) - Gao L et al, `AAAI 2019`.
* [Improving Image Captioning with Conditional Generative Adversarial Nets](https://arxiv.org/abs/1805.07112) - Chen C et al, `AAAI 2019`.
* Connecting Language to Images: A Progressive Attention-Guided Network for Simultaneous Image Captioning and Language Grounding - Song L et al, `AAAI 2019`.


## Popular Implementations
### PyTorch
* [ruotianluo/self-critical.pytorch](https://github.com/ruotianluo/self-critical.pytorch)
* [ruotianluo/ImageCaptioning.pytorch](https://github.com/ruotianluo/ImageCaptioning.pytorch)
* [jiasenlu/NeuralBabyTalk](https://github.com/jiasenlu/NeuralBabyTalk)
### TensorFlow
* [tensorflow/models/im2txt](https://github.com/tensorflow/models/tree/master/research/im2txt)
* [DeepRNN/image_captioning](https://github.com/DeepRNN/image_captioning)
### Torch
* [jcjohnson/densecap](https://github.com/jcjohnson/densecap)
* [karpathy/neuraltalk2](https://github.com/karpathy/neuraltalk2)
* [jiasenlu/AdaptiveAttention](https://github.com/jiasenlu/AdaptiveAttention)
### Others
* [emansim/text2image](https://github.com/emansim/text2image)
* [apple2373/chainer-caption](https://github.com/apple2373/chainer-caption)
* [peteanderson80/bottom-up-attention](https://github.com/peteanderson80/bottom-up-attention)
