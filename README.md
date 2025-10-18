# KAIRI_2025_Summer
Results of summer internship at KAIST (Korea Advanced Institute of Science and Technology)

This project can be run on Google Colab.

## Project Structure

```
KAIRI_2025_Summer/
├── .gitignore                                  # Git ignore file
├── README.md                                   # Project documentation
├── 1. KAIRI_Experiment_Generate.ipynb          # Model inference & data generation
├── 2. KAIRI_Experiment_Consistent_ID_CLS.ipynb # Consistency analysis
├── 3. KAIRI_Experiment_Response_Emergence.ipynb # Response emergence analysis
├── 4. KAIRI_Experiment_AAA_Reproduce.ipynb     # Top-K analysis & reproduction
│
└── data/                                       # Data directory
    ├── CommonsenseQA_test.jsonl               # Original dataset (required)
    └── [model-name]/                          # Model-specific results (auto-generated)
        ├── data_ilt.json                      # Layer-wise inference results
        ├── consistent_ids_converted.json      # Consistent IDs list
        ├── inconsistent_ids_converted.json    # Inconsistent IDs list
        ├── normalized_*.json                  # Normalized analysis results
        └── Figure/                            # Visualization graphs
```

## Notebook Execution Order

### Step 1: Data Generation (Notebook 1)
**1. KAIRI_Experiment_Generate.ipynb**
- Load model and perform inference with 6 prompt variations
- Extract predicted tokens from hidden states at each layer
- Output: Generates `data/[model-name]/data_ilt.json`

### Step 2: Consistency Analysis (Notebook 2)
**2. KAIRI_Experiment_Consistent_ID_CLS.ipynb**
- Analyze consistency of generated answers
- Classify into Consistent vs Inconsistent groups
- Perform normalized token-based analysis
- Output: Generate ID classification JSON files

### Step 3: Response Emergence Pattern Analysis (Notebook 3)
**3. KAIRI_Experiment_Response_Emergence.ipynb**
- Analyze when answer tokens first appear at each layer
- Compare Consistent vs Inconsistent groups
- Perform Majority vs Minority analysis
- Output: Save graphs to `data/[model-name]/Figure/` folder

### Step 4: Top-K Ranking Analysis (Notebook 4)
**4. KAIRI_Experiment_AAA_Reproduce.ipynb**
- Track layer-wise trajectories of final layer's Top-K predictions
- Visualize Logit and Probability changes
- Comparative analysis by correct answer groups
- Output: Generate Top-K analysis graphs

## Dataset Preparation

Add `CommonsenseQA_test.jsonl` file to the `data/` folder.
- For large datasets, download from:
  - [Add your dataset download link here]

## Model Configuration

Configure the model in the first cell of each notebook:
```python
model_distributer = "meta-llama"
model_name = "Llama-3.1-8B"  # Specify model name to use
```

Supported models:
- Llama series (e.g., meta-llama/Llama-3.1-8B)
- Gemma series
- Other HuggingFace AutoModel compatible models

## Key Output Files

### data_ilt.json
Stores predicted tokens, logits, and indices for each question ID across 6 prompts × all layers

### ID Classification Files
- `consistent_ids_converted.json`: IDs where all 6 answers are identical
- `inconsistent_ids_converted.json`: IDs where answers differ
- `normalized_*.json`: Reclassified results after token normalization

### Figure Folder
Layer-wise analysis graphs:
- Distribution of first appearance layer for answer tokens
- Consistent vs Inconsistent group comparisons
- Layer-wise trajectory changes of Top-K predictions
