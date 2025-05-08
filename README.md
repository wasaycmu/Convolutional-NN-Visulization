# Convolutional-NN-Visulization
## Overview

This lab focuses on visualizing and interpreting the internal behavior of a Convolutional Neural Network (CNN), specifically the VGG16 model pre-trained on ImageNet. Our goals include:

- Loading and using a pre-trained model
- Sending various input images through it
- Analyzing intermediate layer activations
- Interpreting the role of specific convolutional filters

## Why VGG16?

We chose VGG16 due to its:

- **Simplicity**: Uniform architecture using 3×3 convolutional filters
- **Pedagogical value**: Discussed extensively in class and easier to analyze
- **Depth**: With 16 weight layers and 138 million parameters, it offers ample opportunities for filter-level analysis
- **Computational efficiency**: Smaller filters make it feasible to visualize features without excessive compute

VGG16 was developed by Karen Simonyan and Andrew Zisserman in 2014 and placed highly in the ImageNet Challenge. It uses only 3×3 convolutional filters with stride 1 and max-pooling with 2×2 filters, making the network deep yet manageable.

## Setup

### Load and Freeze Pre-Trained Model

We used the VGG16 model from Keras and froze all layers to preserve the pre-trained weights. The model was saved locally to avoid reloading or retraining.

## Image Classification

We used locally stored images that were not part of ImageNet to test how well the model generalizes. Despite being trained on ImageNet, VGG16 performed well, showing robust feature extraction.

### Sample Predictions

| Image File      | Top Prediction | Confidence |
|-----------------|----------------|------------|
| borzoi.jpg      | Borzoi         | 99.99%     |
| fat_halpert.jpg | Bow tie        | 100%       |
| let_it_be.jpg   | Book jacket    | 99.99%     |
| mug.jpeg        | Water jug      | 99.97%     |
| shrek.jpg       | Mask           | 100%       |
| wayne.jpeg      | Crutch         | 91.10%     |
| temoc.jpeg      | Ski            | 99.75%     |
| tanuki.jpeg     | Weasel         | 99.98%     |

Some predictions were spot-on (e.g., "borzoi"), while others were reasonable guesses based on visual similarity. Notably, tanuki is not an ImageNet class, so the model approximated it as a "weasel."

## Filter Analysis

### Objective

We selected a mid-level convolutional layer (`block3_conv2`) for deeper analysis. This allowed us to explore filters that represent abstract shapes or object parts rather than just simple edges or textures.

### Steps Taken

1. **Visualized Filter Activations**: We used gradient ascent to generate images that maximally activate selected filters.
2. **Identified Top Activating Classes**: We fed diverse ImageNet images through the network to find those that highly activate a given filter.
3. **Formulated Hypothesis**: Based on both the maximally activating inputs and generated visualizations, we hypothesized the semantic function of each filter.

### Insights

The selected filter in `block3_conv2` appears to be most responsive to:

- Diagonal edges
- Curved structures
- Patterns commonly found in animal faces and certain objects

These observations suggest that the filter is likely involved in detecting mid-level features that contribute to object part detection.

## Tools and Resources

- [OpenAI Microscope](https://microscope.openai.com/models) — for exploring visualizations of neurons in various models
- [Lecture 4 Notebook on Visualizing CNNs](https://github.com/8000net/LectureNotesMaster/blob/master/04%20LectureVisualizingConvnets.ipynb)

## Model Architecture Summary

The VGG16 architecture includes:

- 13 convolutional layers
- 5 max-pooling layers
- 3 fully connected (dense) layers
- Over 138 million total parameters

The use of uniform 3×3 filters and consistent design choices makes VGG16 particularly suitable for introspection and layer-by-layer visualization.

## Conclusion

VGG16 remains a strong and interpretable architecture for analyzing CNN behavior. Through this lab, we successfully visualized filter activations, interpreted their functions, and confirmed that pre-trained models can generalize surprisingly well even to out-of-distribution images.

