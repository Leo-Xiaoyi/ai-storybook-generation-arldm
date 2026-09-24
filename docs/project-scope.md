# Project Scope

This repository presents the ARLDM image-generation work from my undergraduate
thesis on storybook generation. The thesis workflow also used LLaMA2-7B to
generate story text for the adapted ARLDM pipeline.

## Public Repository Scope

The published materials include:

- thesis-oriented ARLDM adaptation code
- Oxford storybook dataset loader and preprocessing scripts
- HDF5 conversion workflow notes
- model configuration and sampling entry points
- one representative generated sequence preview
- documentation for the data and model pipeline

Raw storybook material, HDF5 datasets, model weights, and experiment archives
remain external to the repository; see [release safety](release-safety.md).

## Technical Contributions

I prepared a custom Oxford Reading Tree dataset, converted sequential image-text
data to HDF5, adapted ARLDM data loading and configuration, ran GPU experiments,
and compared generated story sequences with SDXL V1.0. A CLI-based LLaMA2-7B
stage supplied story captions for the end-to-end thesis workflow.

The image-generation model builds on the public ARLDM research codebase, credited
in [NOTICE.md](../NOTICE.md).

## Preview Sequence Notes

The included preview sequence uses the ARLDM row from the thesis evaluation and
shows five frames from the same story prompt sequence. The code also keeps the
continuation mode used during experimentation; in that setup, one saved sample
folder may contain four generated continuation frames because the first frame is
used as conditioning context.

## Resume-Friendly Summary

Built a thesis storybook-generation workflow combining LLaMA2-7B story text with
an adapted ARLDM image pipeline; prepared 234 Oxford Reading Tree books across 9
reading levels as five-frame HDF5 data, ran GPU training and sampling, and
evaluated image coherence against SDXL V1.0.
