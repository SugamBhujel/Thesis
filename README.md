# Popularity Bias in Recommender Systems

## Overview
This repository contains the implementation for my MSc thesis on popularity bias in recommender systems using the MovieLens 32M dataset.

## Contents
- Thesis_on_Popularity_Bias.ipynb — main experiment pipeline

## Dataset

- **Source:** MovieLens 32M Dataset  
- **Provider:** GroupLens Research  
- **Link:** https://grouplens.org/datasets/movielens/  

### Preprocessing
- Users with ≥ 20 ratings  
- Items with ≥ 5 ratings  
- 80/20 train-test split (per user)  
- Popularity computed using training data only  

> Note: Due to size constraints, the dataset is not included in this repository. Please download it from the official source and place it in the appropriate directory before running the notebook.

## How to Run

1. Install dependencies:
pip install numpy pandas scikit-learn matplotlib seaborn shap

2. Open the notebook:
jupyter notebook Thesis_on_Popularity_Bias.ipynb

3. Run all cells

## Requirements
- Python 3.x
- Jupyter Notebook or Google Colab

