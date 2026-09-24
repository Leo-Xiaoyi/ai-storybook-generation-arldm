# AI Storybook Generation with ARLDM

For my undergraduate thesis, **Story Generation Based on Diffusion Models**, I
built a storybook-generation workflow from story text to coherent image
sequences. A CLI-based LLaMA2-7B stage generated story captions, and I adapted
an open-source Auto-Regressive Latent Diffusion Model (ARLDM) to an Oxford
Reading Tree dataset for image generation, training, and evaluation.

![Generated five-frame ARLDM sequence](examples/generated_sequence/sequence_preview.png)

_Five-frame ARLDM story sequence from the thesis evaluation, generated from
one story prompt sequence._

Each dataset item contains five consecutive frames. In continuation sampling,
the first frame can serve as context while the model generates the next four.

## What I Built

- Built a custom Oxford Reading Tree storybook dataset from 234 books across 9
  reading levels.
- Extracted and cleaned paired image-text data with OCR, then grouped pages into
  five-frame story items and converted them to HDF5 for model training.
- Adapted the ARLDM codebase for the Oxford dataset with a custom dataset loader,
  preprocessing scripts, and training/sampling configuration.
- Adjusted token length and CLIP/BLIP embedding settings for longer captions
  and recurring character names.
- Built a CLI interface for LLaMA2-7B story-text generation and used its
  captions as input to the adapted ARLDM workflow.
- Ran GPU training and sampling experiments; compared the resulting sequences
  with SDXL V1.0 and evaluated text-image consistency and cross-frame
  coherence with 32 survey participants.

## Project Scope

The public repository contains the ARLDM adaptation, Oxford dataset pipeline,
training and sampling configuration, technical documentation, and a generated
sequence preview. The thesis also used a LLaMA2-7B text-generation stage; the
published code concentrates on the image-generation pipeline. Source books,
datasets, and model weights remain outside the repository.

## Pipeline

```text
Data        Oxford Reading Tree books -> OCR -> five-frame HDF5 dataset
Training    HDF5 dataset -> adapted ARLDM on GPU
Generation  Story request -> LLaMA2-7B -> captions -> ARLDM -> story frames
Evaluation  ARLDM/SDXL samples -> comparison and 32-participant survey
```

## Repository Structure

```text
.
├── configs/
│   └── oxford_arldm.yaml
├── docs/
│   ├── data-preparation.md
│   ├── model-pipeline.md
│   ├── project-scope.md
│   └── release-safety.md
├── examples/
│   └── generated_sequence/
├── src/
│   ├── data_script/
│   ├── datasets/
│   ├── models/
│   ├── fid_utils.py
│   └── main.py
├── NOTICE.md
├── README.md
└── requirements.txt
```

## Tech Stack

- Python
- PyTorch and PyTorch Lightning
- Hugging Face Diffusers
- CLIP, BLIP, and LLaMA2-7B
- Hydra configuration
- EasyOCR, OpenCV, PIL, and HDF5
- GPU training with SLURM; SDXL V1.0 for comparison

## Reproducing the Published Image Pipeline

Prepare the external data and model assets locally:

- an Oxford-style HDF5 story dataset at `data/oxford.hdf5`
- Stable Diffusion v1.5 model files
- BLIP pretrained weights
- an ARLDM checkpoint for sampling, or GPU resources for training

Install dependencies:

```bash
pip install -r requirements.txt
```

Set model paths:

```bash
export STABLE_DIFFUSION_V1_5_PATH=/path/to/stable-diffusion-v1-5
export BLIP_PRETRAINED_PATH=/path/to/model_large.pth
export BERT_BASE_UNCASED_PATH=/path/to/bert-base-uncased
```

Run from the repository root:

```bash
python src/main.py
```

Edit `configs/oxford_arldm.yaml` to switch between `train` and `sample` mode.

## Results Summary

In the thesis evaluation, the Oxford-adapted ARLDM workflow produced more
visually coherent story sequences than SDXL V1.0 for the tested storybook-style
prompts. A small user survey with 32 participants rated the ARLDM outputs higher
than SDXL V1.0 for both text-image consistency and cross-frame coherence.

The project connects multimodal data preparation, model adaptation, GPU
training, story-sequence generation, and qualitative/user evaluation.

See [release scope](docs/project-scope.md) and [asset notes](docs/release-safety.md)
for the public repository contents and external assets.

## Attribution

This work adapts the public ARLDM implementation by Pan et al. for an
undergraduate thesis project. See [NOTICE.md](NOTICE.md) for details.
