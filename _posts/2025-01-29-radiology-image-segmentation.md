---
layout: post
title: What Deep Learning can do for Image Segmentation in Radiology
author: Taro Langner
---

<p class="message">
    In this post: From Fully Convolutional Networks to TotalSegmentator <br>
    <I>(10 min read)</I><br>
    
</p>

Amidst the ongoing hype around the growing capabilities of large language models, it can be curious to note how earlier predictions about machine learning have stood the test of time. 

Autonomous driving and radiology in particular were considered obvious candidates for automation, starting with the deep learning boom for image recognition around 2012. Geoffrey Hinton famously suggested in 2016 that training of radiologists should be discontinued altogether, arguing that they [would be obsolete within five years](https://www.youtube.com/watch?v=2HMPRXstSvQ). 


<details>
<summary>And yet, things turned out quite different... (click to expand)</summary> 
<img src="/assets/radiologists_in_regular_cars.jpeg" alt="Radiologist Jobs in 2025">

<I>
<a href="https://x.com/olexandr/status/1809670998746161426">(Source)</a>.
And once at work, a US radiologist in 2025  <a href="https://www.glassdoor.com/Salaries/physician-radiologist-salary-SRCH_KO0,21.html">may earn $265-495k per year</a> or pick from a number of job openings that actually <a href="https://x.com/erikbryn/status/1662564885589561344/photo/1">appears to be increasing</a>.
</I>
<br>

</details>
<br>


This is a sobering reminder that many real-world problems turned out to be much harder to crack than expected at first. Although the AI hype has since mostly turned elsewhere, a closer look at what happened in these fields can be rather interesting.

This blog post examines one of their most active, and arguably most successful research areas and reviews one decade worth of progress around deep learning methods for semantic segmentation of medical images in radiology.



## Semantic Segmentation for Radiology

From magnetic resonance imaging (MRI) to computed tomography (CT), medical imaging offers various modalities for visualising the human body. Just like the anatomy itself, these images are often three-dimensional and thus composed of volumetric pixels, or voxels, similar to the block worlds of Minecraft. 

Early on, measurements and findings were often reported from two-dimensional X-ray images. With increasingly affordable imaging technology, the data has since grown both in quantity and resolution, leaving [mere seconds on average](https://www.sciencedirect.com/science/article/pii/S1076633215002457?casa_token=Pud-r9Fq_0wAAAAA:2Vb-4PygjIL9U4FDzfmQ_I9g1cqrvSo-UP1KK9tanNCZalCEN_OUtMCwKdFXgCliL0bXCb9TErwI) for a radiologist to inspect images that can each consist of millions of voxels.

_Semantic segmentation_ is one type of image analysis that is commonly performed in research and industry on these images. It aims to assign a class label to every pixel or voxel, typically to mark all parts of the image that contain a certain tissue or structure. Once complete, a segmentation mask can be used to measure volumes, render surface models or plan radiation treatments.

<p class="message">

<b>Video Example:</b> <br>

<a href="https://www.youtube.com/watch?v=ZRYMItzwg8g&t=220s">- Manual CT Image Segmentation in 3D Slicer (YouTube)</a> [7:43 minutes] <br>
</p>


When done by hand, a given volumetric image is typically segmented by drawing on it as a stack of dozens or hundreds of two-dimensional slices. This can take from minutes to hours or [even days](https://www.cell.com/neuron/fulltext/S0896-6273(02)00569-X?cc=y%3Fcc%3Dy). Results may vary not only between different operators but also when the same image is analysed repeatedly by the same person. This becomes a challenge in studies where hundreds or even thousands of scans are to be analysed in this way.

Despite its many issues, manual segmentation remains the method of choice for many real-world projects that operate in risk-averse settings under restrictive regulatory constraints. On the flip side, these same regulations and concerns have helped to reduce the number of scenarios where malfunctioning software would [burn patients with radiation](https://en.wikipedia.org/wiki/Therac-25) or [confuse surgeons with misleading 3d navigation views](https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfRes/res.cfm?id=171315).

Risk-averse skeptics were furthermore proven right on several occasions before when they doubted claims about technology being superior to medical experts. In the late 90s, computer-aided detection (CAD) systems were funded with millions of dollars per year but later reported to provide no benefit or [perhaps even cause harm](https://jamanetwork.com/journals/jamainternalmedicine/fullarticle/2443369). The deep learning boom later caused an entire flood of such claims, like in the 2017 [CheXNet paper](https://arxiv.org/abs/1711.05225) co-authored by Andrew Ng, the issues of which are discussed with many insights in the [blog of Lauren Oakden-Rayner](https://laurenoakdenrayner.com/2018/01/24/chexnet-an-in-depth-review/).

Despite this history of overpromising, the work done by a multitude of researchers and engineers over the years has nonetheless achieved some impressive progress. Especially deep learning systems for semantic segmentation of medical images have a lot to offer and are worth a closer look.


## Deep Learning for Semantic Image Segmentation

In the ImageNet challenge of 2012, [AlexNet](https://tensorlabbet.com/#AexNet) famously set a new benchmark result for image recognition by assigning one of 1,000 possible class labels to a given input image with unprecedented accuracy. 

_Sliding window segmentation_ used such image classifiers for semantic segmentation, applying them to each position of an image to receive as input a patch around the current position and predict a class label for the central pixel. This approach suffered from inefficiencies, however, with redundant processing wherever a given image area appeared in multiple, adjacent patches.

[[Fully Convolutional Networks, 2015]](https://openaccess.thecvf.com/content_cvpr_2015/html/Long_Fully_Convolutional_Networks_2015_CVPR_paper.html) were proposed as a neural network architecture for dense prediction of pixel-wise labels. This approach removes any fully-connected layers from established architectures for image classification. The remaining convolutional and pooling layers act as an encoder, producing feature maps that retain spatial image information at different resolutions. From these, a 1x1 convolution produces one feature map for each class, to be upsampled by transposed convolution layers to restore the original image dimensions. 


<p class="message">

<b>Transposed Convolution (Animations)</b> <br>

<a href="https://github.com/vdumoulin/conv_arithmetic/blob/master/README.md">- Convolution arithmetic (GitHub)</a> by Vincent Dumoulin,  Francesco Visin <br>
<br>

Note: Transposed convolutions differ from dilated (or à trous) convolutions <a href="https://tensorlabbet.com/#DilatedConv">that featured in a previous blog post</a>.

</p>


With skip connections, these upsampled feature maps are obtained not only from the final, most low-resolution output, but also from earlier steps and fused together by summation to incorporate more high-resolution features.

[[U-Net, 2015]](http://miai.ha.edu.cn/Essays/8Medical%20image%20segmentation/U-Net.pdf) built on this approach by proposing a symmetric encoder-decoder architecture with even more skip connections. The encoder part forms the left half of its U-shape, with successive network layers producing feature maps of decreasing resolution. The decoder path then gradually restores the original resolution with transposed convolution layers. Long skip connections provide shortcuts that concatenate feature maps of the encoder to their counterparts in the decoder.
This enables U-Nets to consider both coarse, low-resolution features as well as detailed, high-resolution features.

[[3D U-Net, 2016]](https://lmb.informatik.uni-freiburg.de/Publications/2016/CABR16/cicek16miccai.pdf) later extended these concepts to volumetric, voxel-based input data by using 3D variants of both pooling and convolution layers.

U-Net architectures enjoyed enormous success and remain competitive options for medical image segmentation to this day. They tend to be robust and reliable, with 2D variants training within minutes on modern GPUs and being lightweight enough for inference even on laptop CPUs.
They can also perform well even with just a few dozen training images, as each pixel or voxel effectively forms one training sample. Hundreds of U-Net variants were subsequently proposed in the literature, including [SegResNet](https://arxiv.org/abs/1810.11654) with short skip connections and [2.5D approaches](https://arxiv.org/abs/1801.05746) that stack adjacent slices to form RGB colour images suitable for encoders pre-trained on ImageNet.

[[nnU-Net, 2018]](https://arxiv.org/abs/1809.10486) (‘no-new-Net’) was ultimately proposed as a self-adapting framework for training effective U-Net architectures. It enables the training of both 2D and 3D U-Nets, as well as cascades with subsequent segmentation steps. Instead of focusing on modifications of the model architecture, it adjusts the preprocessing, training, inference and post-processing with many domain-specific heuristics and also enables cross-validations for evaluation.

For example, as imaging devices of different vendors can vary in contrast, the preprocessing first standardizes or at least scales the image intensities. Some segmentation tasks suffer from extreme class imbalances (for example when small cancerous lesions are to be segmented) and the sampling strategy therefore tries to balance the foreground and background samples for each minibatch in training. Variations in patient anatomy and position are simulated by augmentation with rotation, scaling and mirroring during training. Test-time augmentation furthermore presents each sample with its mirrored copy and averages the predictions for increased robustness. Contemporary GPUs were often limited to 11GB, and so the inference processes larger images by blending patch-wise predictions. 

Its authors at the German Cancer Research Center (DKFZ) published an open-source implementation. Its [research code](https://github.com/MIC-DKFZ/nnUNet) (which purportedly [left Godzilla dead](https://github.com/MIC-DKFZ/batchgenerators/blob/1185d57bbc002f4b88c03fdea885dc28537ad8e7/batchgenerators/augmentations/noise_augmentations.py#L55), whereas I was merely scarred) enabled many to reproduce these techniques. So successful was this framework both in benchmark challenges and various research papers that even in summer 2024 it [still lays claim](https://arxiv.org/pdf/2404.09556) to dominance in this domain.

[[TotalSegmentator, 2023]](https://pmc.ncbi.nlm.nih.gov/articles/PMC10546353/) was later released as a freely available, already trained nnU-Net model for segmentation of 104 different structures in CT images, such as organs, bones, muscle and blood vessels. Up to this point, it was common that segmentation models trained on one dataset would not perform as well on data from other sources due to distribution shifts from different imaging devices, protocols or patient demographics. By training on a varied dataset of over one thousand real-world CT images with different age groups, sites, and protocols, TotalSegmentator made a substantial leap in generalization across arbitrary CT data. Notably, the model was made highly accessible with a Python package, integration into 3D Slicer and even a [free web interface](https://totalsegmentator.com/). In 2024, [an extended version](https://arxiv.org/pdf/2405.194929) was released for segmentation of 59 structures in even more variable images from MRI.


## Concluding Thoughts

From early Fully Convolutional Networks of 2014 to TotalSegmentator in 2024 for MRI, these papers trace the evolution of deep learning for semantic segmentation of radiology images over an entire decade. As an open research question it motivated thousands of papers with varied methodologies. Their insights were gradually distilled into the later publications and methods. Today, no programming or deep learning knowledge is required for anyone to simply drag and drop an image into [TotalSegmentator](https://totalsegmentator.com/) with impressive results. \
That is progress! 

Medical image segmentation still remains an active field of research, with various benchmark challenges (beyond the scope of TotalSegmentator) in conferences like [MICCAI](https://miccai.org/index.php/) and [Kaggle challenges with monetary prizes](https://www.kaggle.com/competitions/rsna-2024-lumbar-spine-degenerative-classification).

The convolutional neural network architectures reviewed so far in this post also remain a competitive option especially for limited training data, as is common for medical images. Methods that utilise Transformers have emerged too, such as [SwinUNETR](https://arxiv.org/abs/2201.01266) (also see the open-source [MONAI](https://github.com/Project-MONAI/tutorials/blob/main/auto3dseg/README.md) framework) and [MedSAM](https://www.nature.com/articles/s41467-024-44824-z) as a medical version of the [Segment Anything Model](https://openaccess.thecvf.com/content/ICCV2023/html/Kirillov_Segment_Anything_ICCV_2023_paper.html). More recently, even multimodal [large language models are being considered for radiology tasks](https://pubs.rsna.org/doi/pdf/10.1148/radiol.232756) which may warrant an entire blog post of their own.

So with all these innovations, then, why has radiology not been automated yet? While there is a growing number of success stories of FDA-approved and CE marked supporting tools entering the market, these systems have to overcome numerous obstacles. Next to regulatory hurdles, workflow integration and acceptance issues, the technical challenge is just one of them.

However, even the technical challenges in this space have not been truly automated yet. I received a taste of this myself when working on [kidney segmentations in MRI of UK Biobank](https://www.nature.com/articles/s41598-020-77981-4). Before my results for 40,000 participants could be uploaded to the [official data catalogue](https://biobank.ndph.ox.ac.uk/showcase/label.cgi?id=159), I skimmed through thousands of these images to identify and understand outlier cases where my U-Net had failed to accurately segment both kidneys.

This taught me about [horseshoe kidneys](https://en.wikipedia.org/wiki/Horseshoe_kidney), or renal fusion, in which both kidneys are connected from birth. In this large dataset over a dozen such cases occurred, and without any training examples for this rare condition, the model had not learned how to handle them well at first. Mel Gibson is often given as a famous case of renal fusion, and if he had participated in UK Biobank, my system would have likely failed him. But who knows, perhaps today TotalSegmentator would have succeeded even for him?



