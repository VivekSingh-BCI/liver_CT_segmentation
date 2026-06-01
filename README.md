# Liver CT Dataset

Download Liver CT Processed dataset through this link: https://qmulprod-my.sharepoint.com/:u:/g/personal/hfy432_qmul_ac_uk/IQAID5WHQqQ0RIiP82xjQgVcAeL4K5O6W8GBif4vQbJmcEg?e=KJ39oD

# Liver CT Segmentation with U-Net

This repository contains a student-friendly Jupyter notebook for liver and tumor segmentation from contrast-enhanced CT slices using a 2D U-Net in PyTorch.

The notebook is designed for MSc students who may be new to programming, artificial intelligence, and medical image segmentation. It includes detailed explanations, inline code comments, model architecture notes, training/evaluation steps, and Grad-CAM visualizations.

## Dataset

This practical uses the HCC subset of a public primary liver cancer contrast-enhanced CT dataset.

- HCC means hepatocellular carcinoma.
- The notebook focuses on arterial phase HCC data from 94 patients.
- Source article: "Comprehensive multi-phase 3D contrast-enhanced CT imaging for primary liver cancer"
- Link: https://www.nature.com/articles/s41597-025-05125-2

The original dataset contains 3D contrast-enhanced CT imaging. For this teaching notebook, the data are expected to be prepared as 2D PNG slices with matching segmentation masks.

Expected local folder structure:

```text
Segmentation/
  train/
    images/
    masks/
  val/
    images/
    masks/
  test/
    images/
    masks/
```

The dataset files are not included in this repository.

## Segmentation Classes

Each pixel belongs to one of three classes:

- `0`: background, shown as black
- `1`: liver, shown as green
- `2`: tumor, shown as red

## Notebook

Main notebook:

- `liver_tumor_unet_pytorch_teaching_student_friendly.ipynb`

The notebook covers:

1. Dataset checking
2. Mask color conversion
3. PyTorch `Dataset` and `DataLoader`
4. 2D U-Net model definition
5. Training and validation
6. Dice and IoU evaluation
7. Prediction visualization
8. Saving predicted masks
9. Grad-CAM explanation maps

## Model Architecture

The U-Net in the notebook uses:

- 4 encoder stages: 32, 64, 128, and 256 feature channels
- 1 bottleneck stage: 512 feature channels
- 4 decoder stages: 256, 128, 64, and 32 feature channels
- 4 skip connections
- Final `1 x 1` convolution to produce 3 class-score channels

The encoder has 8 convolution layers, the bottleneck has 2 convolution layers, and the decoder has 8 convolution layers plus 4 upsampling layers.

## Jupyter Runtime Note

The notebook uses:

```python
NUM_WORKERS = 0
PIN_MEMORY = False
```

These settings avoid PyTorch `DataLoader` multiprocessing cleanup errors that can occur in Jupyter notebooks.

## Requirements

Install the required Python packages:

```bash
pip install torch torchvision pillow matplotlib numpy pandas tqdm scikit-learn
```

Use a CUDA-capable GPU if available. The notebook can also run on CPU, but training will be slower.

## Outputs

Generated outputs are intentionally ignored by Git, including:

- model checkpoints such as `*.pth`
- prediction folders
- local train/validation/test image data
- Jupyter checkpoints

## Medical Disclaimer

This notebook is for education and research practice only. It is not a clinical tool and must not be used for medical diagnosis or treatment decisions.
