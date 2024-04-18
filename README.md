## UASRM

Date: 3/15/2024
Contact: tcgoldfarb@gmail.com

The UASRM (Unet Audio Spectrogram Repair Model) is a personal research exercise in utilizing inpainting machine learning
methods for audio repair by Todd Goldfarb.

The idea revolves around the concept of treating an audio as an image (spectrogram format), and then using inpainting techniques
commonly used on standard imaging on the spectrogram.

NOTE: The .ipnyb currently fails, as it is up to the user to input a dataset for use. Once a dataset.wav file is provided, the code will run.

![image](https://github.com/Todd-C-Goldfarb/UASRM/assets/132838573/ff60a346-6170-488b-a6d5-de2a5bc18345)

As a summary, the .ipnyb file contains:

# Data Pipeline
The preprocessing step takes a selection of wave (.wav) files, and creates a dataset (artificially damaging/removing audio and pairing with clean audio).
The preprocessing steps are:
- .wav (wave) -> 2D Raw Audio Array

- Raw 2D Array -> Spectro. (STFT), with artificial damaging.

- Spectrogram Values -> Tensors (for use with PyTorch)

This whole process is reversed to output to audio.

# Modified U-Net
- Modified U-Net Architecture model that creates a feature map up to 4096 channels, using Skip Connections (64, 128, 256, 512, 1024, 2048).
- The forward output is spliced at the damaged points of the audio and returned to the original spectrogram (only “filling in” data at specified damage intervals).
- The model is trained over the damaged and clean audio dataset, and then uses MSELoss for backpropagation.

# Quantative Results
![image](https://github.com/Todd-C-Goldfarb/UASRM/assets/132838573/404e49dc-2e58-4a43-bc87-7edbf7049110)

This algorithm is used to calculate accuracy.
It is a "harsher" algorithm that only calculates for exact and "close-to-exact" values.

## How to Use
- Fill in audio .wav files, either large chunks or many files. Either way, the audio will be split up into values specified by the .ipnyb.
- The ideal "damage" length should be around ~0.5s with upwards of 5+ seconds of context.

## Example Results (Un-Ideal Conditions, w/ Student Resources)
![image](https://github.com/Todd-C-Goldfarb/UASRM/assets/132838573/2de56532-f192-4520-97c2-de685b5a8cef)
![image](https://github.com/Todd-C-Goldfarb/UASRM/assets/132838573/7ac4babf-cfbb-478b-b034-b5167f606108)
![image](https://github.com/Todd-C-Goldfarb/UASRM/assets/132838573/378a52b2-185d-4bb8-b6a3-ce4cd786d246)

  
