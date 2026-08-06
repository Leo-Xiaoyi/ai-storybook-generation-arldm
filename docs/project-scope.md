# Project Scope

This repository is a cleaned public portfolio version of an undergraduate thesis
project on storybook image sequence generation with diffusion models.

## Public Repository Scope

The public repository focuses on the parts that are useful, safe, and reasonable
to review:

- thesis-oriented ARLDM adaptation code
- Oxford storybook dataset loader and preprocessing scripts
- HDF5 conversion workflow notes
- model configuration and sampling entry points
- one representative generated sequence preview
- documentation for the data and model pipeline

It intentionally excludes raw storybook PDFs, extracted datasets, HDF5 files,
model checkpoints, pretrained model caches, generated experiment archives,
server notes, and administrative thesis materials.

## Responsible Positioning

This project is best read as an applied AI, multimodal data pipeline, and
research-code adaptation project. The work focused on preparing a custom
storybook dataset, converting sequential image-text data into an efficient HDF5
format, adapting ARLDM data loading and configuration, running GPU experiments,
comparing generated outputs, and evaluating sequence coherence.

The project adapts the public ARLDM research codebase. It should not be
presented as an original model architecture, a production-ready storybook
generator, or a repository that can reproduce the full thesis workflow without
external datasets and model assets.

## Preview Sequence Notes

The included preview sequence uses the ARLDM row from the thesis evaluation and
shows five frames from the same story prompt sequence. The code also keeps the
continuation mode used during experimentation; in that setup, one saved sample
folder may contain four generated continuation frames because the first frame is
used as conditioning context.

## Resume-Friendly Summary

Adapted an ARLDM-based diffusion pipeline for storybook image generation,
building a custom Oxford Tree dataset from 234 storybooks, converting sequential
image-text pairs into HDF5 format, and running GPU training/sampling experiments
to evaluate cross-frame visual coherence.
