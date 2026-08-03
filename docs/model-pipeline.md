# Model Pipeline

The thesis framework used ARLDM as the core image-generation model.

ARLDM differs from independent text-to-image generation because it conditions
each generated frame on earlier story frames. This is useful for storybook
generation, where character appearance, scene style, and visual continuity matter
across multiple images.

## ARLDM Adaptation

The original ARLDM implementation was adapted for the Oxford storybook dataset:

- added an Oxford-specific `StoryDataset`
- converted page-level story data into 5-frame sequential samples
- adjusted max token length for longer captions
- supported optional new character-name tokens
- resized CLIP and BLIP token embeddings when extra tokens were used
- kept ARLDM's history-aware conditioning path for sequential generation

## Training And Sampling

The cleaned code keeps the original high-level flow:

```text
Oxford HDF5 dataset
    -> PyTorch Lightning DataModule
    -> CLIP text encoding
    -> BLIP multimodal history encoding
    -> latent diffusion U-Net
    -> VAE decoding
    -> generated story frames
    -> FID / qualitative evaluation
```

The original thesis experiments were run on a GPU server. The public version
keeps configuration and code structure, but excludes checkpoints and model
weights.

## Evaluation

The thesis compared the Oxford-adapted ARLDM workflow with SDXL V1.0 on the
same generated story prompts. The focus was not only single-image quality, but
also whether the same characters and scenes remained coherent across a sequence.
