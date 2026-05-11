<div align="center">
  
# STITCH 🧬
### **S**patial **T**ranscriptomics **I**mputation via flow ma**TCH**ing

**A highly scalable, decoupled generative framework for multi-dimensional spatial transcriptomic virtual data reconstruction.**

[![Python 3.8+](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/downloads/release/python-380/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-ee4c2c.svg)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Paper](https://img.shields.io/badge/Paper-bioRxiv-b31b1b.svg)](#)

</div>

---

## 📖 Introduction
Spatial transcriptomics (ST) mapping is inherently hindered by discontinuous slice sampling and in-slice tissue damage. **STITCH** provides a deterministic, platform-agnostic computational foundation to bridge these multidimensional physical faults. 

Grounded in a **"Single-Sample Internal Learning"** paradigm, STITCH eliminates the need for external reference atlases. By decoupling spatial morphology restoration from gene expression generation, STITCH flexibly repairs 2D in-slice damage and bridges 3D cross-slice gaps, effectively scaling to millions of cells.

### ✨ Key Features
- **3D Cross-Slice Interpolation**: Utilizes Optimal Transport-Conditional Flow Matching (OT-CFM) to deterministically infer continuous spatial coordinates across sections.
- **2D In-Slice Inpainting**: Employs an attention-enhanced internal diffusion engine to achieve high-fidelity restoration of damaged structures.
- **$\mathcal{O}(N)$ Gene Flow Engine**: A minimalist point-wise continuous flow matching module in the latent space that effectively averts memory bottlenecks for large-scale data.
- **Platform-Agnostic**: Extensively validated across Stereo-seq, MERFISH, Xenium, and Visium platforms.

---

## ⚙️ Installation

We highly recommend using [Conda](https://docs.conda.io/en/latest/) to manage your environment. STITCH requires Python 3.8+ and PyTorch.

```bash
# 1. Clone the repository
git clone https://github.com/YourUsername/STITCH.git
cd STITCH

# 2. Create a virtual environment
conda create -n stitch_env python=3.9 -y
conda activate stitch_env

# 3. Install dependencies
pip install -r requirements.txt
```
---

## 🚀 Quick Start
STITCH is designed to be highly modular. Below is a minimal example demonstrating how to run the decoupled pipeline.

Case 1: 3D Structure Flow (e.g., MERFISH / Stereo-seq)
```bash
import stitch

# Load adjacent spatial transcriptomic slices
adata_prev = stitch.read_h5ad("data/slice_01.h5ad")
adata_next = stitch.read_h5ad("data/slice_02.h5ad")

# 1. Spatial Structure Restoration via OT-CFM
# Calculate Local FGW-OT and integrate bidirectional ODE
virtual_coords = stitch.struct_flow_3d(adata_prev, adata_next, target_depth=0.5)

# 2. Gene Feature Generation via Point-wise Flow
# Reconstruct transcriptomic profiles in O(N) complexity
virtual_genes = stitch.gene_flow(virtual_coords, adata_prev, adata_next)
```

Case 2: Lightweight 2D Inpainting (e.g., Xenium)
For 2D hole-inpainting tasks with highly targeted gene panels (e.g., 50 SVGs), STITCH can bypass the SAGA dimensionality reduction for an end-to-end generation.
```bash
import stitch

# Train the attention-enhanced internal diffusion engine
stitch.train_diffusion_2d(adata_xenium, mask_key="hole_mask", epochs=2000)

# Restore physical coordinates and gene expressions
restored_adata = stitch.inpaint_2d(adata_xenium)
```
Note: Detailed tutorials in Jupyter Notebook format are available in the tutorials/ folder.

---

## 📊 Data Availability
To reproduce the results presented in our paper, the datasets can be downloaded from the following public repositories:

- **Stereo-seq Drosophila**: [Spateo Repository](https://spateo-release.readthedocs.io/en/latest/)
- **MERFISH Mouse Brain**: [Allen Brain Cell (ABC) Atlas](https://alleninstitute.github.io/abc_atlas_access/descriptions/Zhuang-ABCA-2.html)
- **Visium BRCA & DLPFC (3D Aligned)**: [So3D Database](https://So3D.bio-database.com/download.jsp)
- **Xenium 2D Mouse Brain**: [10x Genomics Portal](https://www.10xgenomics.com/datasets/fresh-frozen-mouse-brain-for-xenium-explorer-demo-1-standard)
  
## Citation
If you find STITCH useful for your research, please consider citing our paper:
```bash
@article{YourName2024STITCH,
  title={STITCH: A decoupled generative framework for multi-dimensional spatial transcriptomic virtual data reconstruction},
  author={Your Name and Co-authors},
  journal={bioRxiv},
  year={2024},
  publisher={Cold Spring Harbor Laboratory}
}
