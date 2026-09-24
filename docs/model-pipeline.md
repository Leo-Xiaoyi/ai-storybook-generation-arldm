# Model Pipeline

The thesis workflow used a CLI-based LLaMA2-7B stage to generate story captions
from user requests, then passed those captions to an adapted ARLDM pipeline for
sequential image generation. The published code focuses on the ARLDM stage.

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
Training: Oxford HDF5 data -> PyTorch Lightning DataModule -> adapted ARLDM
Generation: story request -> LLaMA2-7B -> story captions -> adapted ARLDM
            -> CLIP text encoding + BLIP multimodal history encoding
            -> latent diffusion U-Net -> VAE decoding -> story frames
Evaluation: generated frames -> FID / qualitative comparison / user survey
```

The original thesis experiments were run on a GPU server. The public version
keeps configuration and code structure, but excludes checkpoints and model
weights.

Each data item contains five consecutive story frames. In the thesis evaluation,
representative ARLDM outputs were presented as five-frame story sequences. In
the code's `continuation` sampling setup, the first frame can be used as
conditioning context, so saved sample folders may contain four generated
continuation frames for one item.

## Evaluation

The thesis compared the Oxford-adapted ARLDM workflow with SDXL V1.0 on the
same generated story prompts. The focus was not only single-image quality, but
also whether the same characters and scenes remained coherent across a sequence.
