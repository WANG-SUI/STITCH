<div align="center">

# STITCH
### **S**patial **T**ranscriptomics **I**mputation via flow ma**TCH**ing

**A scalable, decoupled generative framework for multidimensional virtual spatial transcriptomics reconstruction.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Paper](https://img.shields.io/badge/Paper-bioRxiv-b31b1b.svg)](https://www.biorxiv.org/content/early/2026/06/06/2026.06.03.729557)
[![GitHub stars](https://img.shields.io/github/stars/WANG-SUI/STITCH?style=social)](https://github.com/WANG-SUI/STITCH/stargazers)

</div>

---

## Introduction

Spatial transcriptomics technologies can resolve tissue architecture at increasingly high resolution, but complete spatial coverage remains difficult. Physical sectioning, sparse slice sampling, sequencing cost, and in-slice tissue damage often leave substantial spatial gaps, producing fragmented 3D tissue reconstructions and incomplete 2D slices.

STITCH addresses this problem as a multidimensional virtual spatial transcriptomics reconstruction task. Instead of relying on external reference atlases or matched histological image priors, STITCH learns intrinsic spatial-transcriptomic patterns directly from the observed tissue sample. The framework is motivated by internal learning: local spatial continuity, coherent microenvironmental composition, and region-specific expression structure provide sample-specific information that can support reconstruction of missing regions.

STITCH uses a decoupled architecture that separates spatial morphology restoration from transcriptomic generation. First, a spatial-aware graph autoencoder compresses high-dimensional gene expression into a topology-preserving latent representation. Second, a Structure Flow module reconstructs missing spatial coordinates: optimal transport-conditioned flow matching is used for 3D cross-slice gaps, while an internal learning strategy is used for 2D in-slice damage repair. Third, a Gene Flow module generates the corresponding transcriptomic profiles through point-wise conditional flow matching in latent space.

This design gives STITCH linear computational complexity for transcriptomic generation and enables scalable reconstruction of large spatial atlases. In the manuscript, STITCH is evaluated across single-cell and spot-level spatial transcriptomics platforms, including Stereo-seq, MERFISH, Xenium, and Visium. In a large-scale MERFISH mouse brain experiment, STITCH expands 54 observed slices into a continuous atlas of 571 slices and more than 11 million cells within approximately 5 hours on a single commodity GPU.

## Key Features

- **3D cross-slice interpolation:** reconstructs virtual spatial sections across physical slice gaps using optimal transport-conditioned flow matching.
- **2D in-slice repair:** restores damaged tissue regions using an internal learning strategy adapted for spatial transcriptomics.
- **Spatial-aware latent modeling:** compresses gene expression through a graph autoencoder while preserving local spatial topology.
- **Point-wise Gene Flow:** generates transcriptomic profiles with linear computational complexity for large-scale atlas reconstruction.
- **Platform compatibility:** supports both single-cell and spot-level spatial transcriptomics datasets.

---

## Data Availability

To reproduce the results presented in our paper, the datasets can be downloaded from the following public repositories:

- **Stereo-seq Drosophila:** [Spateo Repository](https://spateo-release.readthedocs.io/en/latest/) and [direct data link](https://www.dropbox.com/s/bvstb3en5kc6wui/E7-9h_cellbin_tdr_v2.h5ad?dl=1)
- **MERFISH Mouse Brain:** [Allen Brain Cell Atlas](https://alleninstitute.github.io/abc_atlas_access/descriptions/Zhuang-ABCA-2.html)
- **Visium BRCA and DLPFC:** [So3D Database](https://So3D.bio-database.com/download.jsp)
- **Xenium 2D Mouse Brain:** [10x Genomics Portal](https://www.10xgenomics.com/datasets/fresh-frozen-mouse-brain-for-xenium-explorer-demo-1-standard)

---

## Citation

If you find STITCH useful for your research, please cite:

```bibtex
@article{Wang2026STITCH,
  title = {STITCH: Spatial Transcriptomics Imputation via Flow Matching with Internal Learning},
  author = {Wang, Sui and Wang, Xinyu and Peng, Qiangwei and Li, Tiejun},
  journal = {bioRxiv},
  year = {2026},
  doi = {10.64898/2026.06.03.729557},
  url = {https://www.biorxiv.org/content/early/2026/06/06/2026.06.03.729557}
}
```
