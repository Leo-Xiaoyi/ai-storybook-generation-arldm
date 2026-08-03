# Portfolio Notes

This project is best presented as an applied AI and data pipeline project.

## Strong Interview Positioning

I adapted a research codebase around ARLDM for a custom storybook-generation
task. My work focused on preparing a new multimodal dataset, converting it into
an efficient HDF5 training format, adapting dataset loading and configuration,
running GPU experiments, comparing generated outputs, and evaluating coherence.

The included preview sequence uses the ARLDM row from the thesis evaluation and
shows five frames from the same story prompt sequence. The code also keeps the
continuation mode used during experimentation; in that setup, one saved sample
folder may contain four generated continuation frames because the first frame is
used as conditioning context. Do not mix frames from different sample items just
to make a preview look longer.

## Avoid Overstating

- Do not claim that I invented ARLDM.
- Do not claim that this is a production-ready storybook generator.
- Do not claim that the full dataset or model can be reproduced directly from
  this public repository.
- Do not position this as my target career direction if the role is mainly AI
  application development.
- Do not imply that all original thesis files were published. The public repo is
  a cleaned portfolio release containing the relevant final code and evidence.

## Resume-Friendly Summary

Adapted an ARLDM-based diffusion pipeline for storybook image generation,
building a custom Oxford Tree dataset from 234 storybooks, converting sequential
image-text pairs into HDF5 format, and running GPU training/sampling experiments
to evaluate cross-frame visual coherence.
