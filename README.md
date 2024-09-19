# Code Cortex - Machine Learning Pipeline for Product Measurements Extraction

## Project Overview

This project aims to develop a machine learning pipeline that processes product images to extract entity-related measurements, such as **width, height, depth, weight, and volume**, using **Optical Character Recognition (OCR)**. The pipeline extracts numerical values and measurement units from product images, mapping them to relevant entities like product dimensions or weight.

## Table of Contents
- [Introduction](#introduction)
- [Models and Techniques](#models-and-techniques)
- [Pipeline Workflow](#pipeline-workflow)
  - [1. Data Preprocessing](#1-data-preprocessing)
  - [2. Unit and Value Extraction](#3-unit-and-value-extraction)
  - [3. Value and Unit Selection](#4-value-and-unit-selection)
  - [4. Predictions](#5-predictions)
- [Experiments](#experiments)
  - [Experiments-1: Hybrid Model Architecture](#experiments-1-hybrid-model-architecture)
  - [Experiments-2: Data Preprocessing & Prediction](#experiments-2-data-preprocessing--prediction)
- [Conclusion](#conclusion)

---

## Introduction

This project focuses on extracting specific measurements from images using **OCR** and machine learning techniques. We aim to automate the process of identifying entities like product dimensions and weights, extracting their corresponding numerical values and units from the image content.

## Models and Techniques

- **EasyOCR**: Optical character recognition for extracting text from images.
- **Pattern Matching & Regular Expressions (Regex)**: Extracting numeric values and units from the text.
- **ResNet-50**: A CNN-based architecture for image feature extraction.
- **BERT**: NLP model used to process the text extracted from images.

## Pipeline Workflow

### 1. Data Preprocessing

The dataset includes image URLs, entity names, and corresponding values. The preprocessing steps include:

- **OCR**: Using **Tesseract** to extract text from product images.
- **Text Post-processing**: Cleaning the extracted text by removing unwanted characters and standardizing measurement units (e.g., replacing " with inch).

### 2. Unit and Value Extraction

After extracting the text from an image, we:

- **Entity-Unit Mapping**: A dictionary is created to map entities (e.g., "width," "height") to allowed measurement units (e.g., centimetre, inch, kilogram).
- **Pattern Matching**: Regular expressions (regex) are applied to detect numerical values and units like "15 cm" or "3.5 kg."

### 3. Value and Unit Selection

A relevance filtering process ensures only units relevant to the entity are selected. If multiple values are detected, the most appropriate value is chosen based on the entity type.

### 4. Predictions

Extracted values are saved in a **CSV file**, associating each image with its corresponding entity and values.

## Experiments

### Experiments-1: Hybrid Model Architecture

1. **ResNet-50**: A pre-trained ResNet-50 is used to extract high-level features from images. Its final layer is replaced with a smaller fully connected layer (128 units) to suit the task.
2. **BERT**: A pre-trained BERT model processes text extracted by OCR. The [CLS] token embedding is used for text representation.
3. **Loss Functions**:
   - **Value Prediction**: Mean squared error (MSE) loss is used for predicting numerical values.
   - **Unit Prediction**: Cross-entropy loss is used for predicting the correct units.
4. **Hyperparameter Tuning**: We used **Optuna** for optimizing hyperparameters like learning rate and batch size.

### Experiments-2: Data Preprocessing & Prediction

1. **Data Preprocessing**: Regex patterns are applied to extract numeric values and units.
2. **OCR with Tesseract**: Text is extracted using Tesseract OCR.
3. **Unit and Value Extraction**: Regex identifies and extracts the relevant numbers and units.
4. **Value and Unit Selection**: Appropriate values are selected from the extracted text.
5. **Predictions**: The extracted data is saved as a **CSV** file.

The pipeline code is available in the `app.ipynb` file.

## Conclusion

This OCR-based pipeline successfully extracts entity-specific values from product images, automating the data processing. The combination of **EasyOCR** and entity-specific unit filtering is scalable for large datasets. However, with an **F1 score of 0.44**, there is significant room for improvement. Enhancing text post-processing and error handling, especially for low-quality images and complex layouts, would boost the model's robustness. Further refining OCR and regex methods could improve accuracy and performance.

---
