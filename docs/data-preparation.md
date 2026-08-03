# Data Preparation

The original thesis used a custom Oxford Tree storybook dataset built from 234
storybook PDFs across 9 reading levels.

The public repository does not include the raw PDFs, extracted images, captions,
or HDF5 files. Those assets are large and may have distribution restrictions.

## Original Workflow

1. Extract text from each storybook page using OCR.
2. Remove text regions from page images to avoid leaking text into the training
   image data.
3. Crop page illustrations and save them as PNG files.
4. Pair each image with its corresponding caption.
5. Group every 5 consecutive story frames into one sequential training item.
6. Split data into train, validation, and test subsets.
7. Store images and captions in HDF5 format for faster training I/O.

In continuation mode, the model uses the five-frame story item as context and
target structure, but saves four generated continuation frames for each sampled
item.

## Included Scripts

- `src/data_script/move.py` prepares cleaned captions and image folders.
- `src/data_script/oxford_hdf5.py` converts the processed Oxford story folders
  into HDF5 groups for train, validation, and test data.
- `src/datasets/oxford.py` loads sequential story items for ARLDM training and
  sampling.

## Expected Local Layout

The original scripts expect a local dataset layout similar to:

```text
dataset/
├── split/
│   ├── story-folder-1/
│   ├── story-folder-2/
│   └── test/
└── newcaps/

data/
└── oxford.hdf5
```

For a public portfolio repo, the data is intentionally excluded. The important
part is the preprocessing and dataset adaptation approach, not shipping the
original storybook assets.
