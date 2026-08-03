# Notice

This repository is a cleaned portfolio version of my undergraduate thesis project,
*Story Generation Based on Diffusion Models*.

The implementation is adapted from the public ARLDM project:

- Upstream project: https://github.com/xichenpan/ARLDM
- Paper: *Synthesizing Coherent Story with Auto-Regressive Latent Diffusion Models*

The repository also includes override modules derived from third-party research
libraries such as BLIP and Diffusers. Their original headers and notices are
preserved where present.

My thesis work focused on adapting and extending the ARLDM workflow for a new
Oxford Tree storybook dataset, including data preparation, HDF5 conversion,
Oxford-specific dataset loading, training/debugging, sampling, and evaluation.

Large assets are intentionally not included:

- Raw storybook PDFs and extracted dataset files
- HDF5 training data
- model checkpoints and pretrained weights
- LLaMA2 model files
- Stable Diffusion model cache
- server logs and experiment archives

This repository is intended as a portfolio and documentation artifact, not as a
fully reproducible release of the original thesis environment.
