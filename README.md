# Hybrid Ground Truth from Multi-Algorithm Consensus for Annotation-Efficient Carotid Ultrasound Segmentation

**Mifta Nur Farid**¹,² · **Tri Arief Sardjono**¹ · **Hendra Kusuma**¹ · **Thomas Statheros**³ · **Vasile Palade**²

¹ Department of Electrical Engineering, Institut Teknologi Sepuluh Nopember, Surabaya, Indonesia  
² Centre for Computational Science and Mathematical Modelling, Coventry University, Coventry, United Kingdom  
³ Centre for Future Transport and Cities, Coventry University, Coventry, United Kingdom  

*Presented at the 2026 9th International Conference on Vocational Education and Electrical Engineering (ICVEE 2026)*

## Status

The paper was presented at [ICVEE 2026](https://icvee.conference.unesa.ac.id/) (17–18 September 2026, Surabaya, Indonesia). Official proceedings publication in IEEE Xplore is currently pending.

The source code will be made available here upon publication of the proceedings.

## Abstract

Pixel-level boundary annotation for carotid intima-media thickness (IMT) segmentation is time-consuming, requires clinical expertise, and varies between observers. This study investigates whether consensus voting over existing algorithm outputs can replace manual boundary annotation for training segmentation models. We propose a hybrid ground truth (HGT) construction method that synthesizes outputs from seven CUBS2 computerized segmentation algorithms through consensus voting, removing the need for manual boundary labels while still relying on benchmark ROI definitions for spatial alignment. Three consensus strategies are evaluated: uniform majority voting (HGT-U), performance-weighted voting (HGT-P), and conservative voting (HGT-C). Each variant trains a U-Net via 5-fold cross-validation on 350 CUBS2 images and is evaluated on a held-out test set of 150 images. Against Manual-A1 as the common clinical reference, HGT-U achieves MAE 0.257 mm with near-zero bias, closely matching three-reading manual consensus (0.254 mm, *p* = 0.42). Hybrid ground truth construction via consensus voting can provide clinically competitive boundary supervision without manual boundary labeling.
