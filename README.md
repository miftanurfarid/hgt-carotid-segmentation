# Hybrid Ground Truth from Multi-Algorithm Consensus for Annotation-Efficient Carotid Ultrasound Segmentation

**Mifta Nur Farid**¹,² · **Tri Arief Sardjono**¹ · **Hendra Kusuma**¹ · **Thomas Statheros**³ · **Vasile Palade**²

¹ Department of Electrical Engineering, Institut Teknologi Sepuluh Nopember, Surabaya, Indonesia  
² Centre for Computational Science and Mathematical Modelling, Coventry University, Coventry, United Kingdom  
³ Centre for Future Transport and Cities, Coventry University, Coventry, United Kingdom  

*Published in the 2026 9th International Conference on Vocational Education and Electrical Engineering (ICVEE 2026)*

## Status

Published in the [2026 9th International Conference on Vocational Education and Electrical Engineering (ICVEE 2026) proceedings](https://ieeexplore.ieee.org/document/11766385) by IEEE. The paper was presented at ICVEE 2026 (17–18 September 2026, Surabaya, Indonesia).

## Reproduction status

First stage only: `generate_targets.py` creates HGT-U and HGT-C masks from
available CUBS2 algorithm boundaries and Manual-A1 ROIs. HGT-P is optional and
requires explicitly supplied, independently verified per-method MAEs. This is
**not yet an end-to-end reproduction of the published results**: training,
fixed splits, manual/STAPLE targets, evaluation, figures, and environment
verification still need to be packaged and run. No dataset or checkpoints are
included. The original experiment code is in the dissertation repository;
this standalone generator is a clean reconstruction, independently checked
against the locally available historical masks below.

Install NumPy, SciPy, and OpenCV in a Python environment (`requirements.txt`). Obtain CUBS2 under
its applicable access terms, with `images/*.tiff` and
`LIMA-Profiles/{Computerized-*,Manual-A1}/` in `DATA_DIR`. Keep dataset and
generated outputs outside this Git repository:

```bash
python -m unittest -v test_generate_targets
python generate_targets.py --data-dir DATA_DIR --output-dir OUTPUT_DIR
```

Outputs: `MASKS_HYBRID_UNIFORM/` and `MASKS_HYBRID_UNCERTAINTY/`, each with
`<stem>_image.png`, `<stem>_mask.png`, `roi_map.json`, and
`excluded_images.txt`. Generator needs at least four valid method pairs per
image, records exclusions, and refuses to overwrite existing output directories. HGT-P can
be enabled with `--mae-json VERIFIED_MAES.json`, a JSON object keyed by the
seven exact algorithm directory names (positive MAE values in a consistent
unit). No claim about the source of those supplied values is made by the code.

The paper specifies a strict `> 0.5` conservative decision, equivalent to
five-of-seven voting when seven methods are available. This implementation
uses a strict threshold above `4/7` agreement for available methods. An older
preprocessing script used rounded `0.43` and `0.72` ramp endpoints and
`>= 0.5`; it also hard-coded performance MAEs. On the locally available CUBS2
copy, 385 images had seven valid method pairs, 113 had six, and two had five.
New HGT-U and HGT-C masks were compared pixel-for-pixel with 500 existing
masks per variant: zero changed masks; all ROI entries matched. This checks
local mask equivalence, not paper-table or training-result reproduction.
The paper's claim that all seven methods have complete files for every image
conflicts with this local copy. Verify dataset provenance before release.

Original paper experiments used an image-level hold-out, not verified
participant-level splitting. The Manual-A1 ROI remains necessary for cropping,
despite algorithm-only boundary consensus. Benchmark-derived HGT-P weights
may overlap with held-out evaluation cases; verify provenance before claiming
independent performance-weight calibration.

## Abstract

Pixel-level boundary annotation for carotid intima-media thickness (IMT) segmentation is time-consuming, requires clinical expertise, and varies between observers. This study investigates whether consensus voting over existing algorithm outputs can replace manual boundary annotation for training segmentation models. We propose a hybrid ground truth (HGT) construction method that synthesizes outputs from seven CUBS2 computerized segmentation algorithms through consensus voting, removing the need for manual boundary labels while still relying on benchmark ROI definitions for spatial alignment. Three consensus strategies are evaluated: uniform majority voting (HGT-U), performance-weighted voting (HGT-P), and conservative voting (HGT-C). Each variant trains a U-Net via 5-fold cross-validation on 350 CUBS2 images and is evaluated on a held-out test set of 150 images. Against Manual-A1 as the common clinical reference, HGT-U achieves MAE 0.257 mm with near-zero bias, closely matching three-reading manual consensus (0.254 mm, *p* = 0.42). Hybrid ground truth construction via consensus voting can provide clinically competitive boundary supervision without manual boundary labeling.
