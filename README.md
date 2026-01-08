# Multimodal Phishing Detection

A hybrid deep learning system combining visual (MobileNetV2) and textual (XLM-RoBERTa) analysis for phishing website detection with Grad-CAM explainability.

## Performance

- **Accuracy:** 85.0% (95% CI: 80.05%-89.95%)
- **ROC-AUC:** 0.9636
- **F1-Score:** 84.98%
- **Model Size:** 1,085 MB

## Dataset

**Phishpedia Dataset** (60,145 samples total)

Download the datasets:
- [Phishing Samples (30K)](https://drive.google.com/file/d/12ypEMPRQ43zGRqHGut0Esq2z5en0DH4g/view) - 7.3GB
- [Benign Samples (30K)](https://drive.google.com/file/d/1yORUeSrF5vGcgxYrsCoqXcpOUHt-iHq_/view) - 56GB

**Original Dataset:** [Phishpedia Official](https://sites.google.com/view/phishpedia-site/home)

## Quick Start

### Prerequisites
```bash
Python 3.9+
CUDA-capable GPU (recommended: 15GB+ VRAM)
```

### Installation

1. **Clone repository**
```bash
git clone https://github.com/Masoodsaid/UFCE4B-60-M.git
cd UFCE4B-60-M
```

2. **Install dependencies**
```bash
pip install torch torchvision transformers scikit-learn matplotlib seaborn tqdm opencv-python pillow
```

3. **Download datasets**
   - Download both ZIP files from the links above
   - Extract to `data/` directory:
```
data/
├── phish_sample_30k/
└── benign_sample_30k/
```

### Run Training

**Google Colab (Recommended):**
```python
# Upload notebook to Colab
# Mount Google Drive with datasets
# Run all cells
```

## Project Structure

```
├── Multimodal_Phishing_Detection.ipynb  # Main notebook
└── README.md
```

## Configuration

Key parameters in the notebook:
- `NUM_SAMPLES = 2000` - Subset size (increase if you have more VRAM)
- `BATCH_SIZE = 16` - Adjust based on GPU memory
- `NUM_EPOCHS = 10` - Training epochs (early stopping enabled)
- `LEARNING_RATE = 1e-4`

## Model Architecture

```
Visual Branch: MobileNetV2 (pretrained) → 512D features
Text Branch: XLM-RoBERTa-base → 512D features
Fusion: Multi-head Attention (8 heads)
Classifier: 512→256→128→2 (Phishing/Benign)
```

## Results

| Metric | Value |
|--------|-------|
| Accuracy | 85.0% |
| Precision (Phishing) | 96.4% |
| Recall (Phishing) | 75.0% |
| False Positive Rate | 3.3% |
| ROC-AUC | 0.9636 |

## Limitations

- **Sample Size:** Trained on 2,000 samples (3.3% of dataset) due to computational constraints
- **Adversarial Vulnerability:** Accuracy drops to 56% under FGSM attacks (ε=0.1)
- **Model Size:** 1,085 MB - unsuitable for mobile/edge deployment
- **Not production-ready** without adversarial defenses

## Use Cases

- Research and academic purposes  
- Proof-of-concept demonstrations  
- Server-side deployment (with GPU)  

## Acknowledgments

- **Dataset:** [Phishpedia](https://sites.google.com/view/phishpedia-site/home)
- **Models:** PyTorch, Hugging Face Transformers
- **Hardware:** Google Colab (Tesla T4)

---
