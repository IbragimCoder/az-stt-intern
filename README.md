# Azerbaijani ASR Pipeline (R.I.S.K. CJSC Intern Task)

Automatic Speech Recognition (ASR) system for the Azerbaijani language built on the `OpenAI Whisper-tiny` model. Evaluated and fine-tuned using the `google/fleurs` dataset.

---

## 📊 Results

### Part A — Base Model (Whisper-tiny, Zero-Shot)
| Metric | Score   |
|--------|---------|
| **WER**| 119.94% |
| **CER**| 78.55%  |

> 🔍 **Note on WER > 100%:** 
> A WER above 100% is mathematically correct and occurs when the model produces significantly more words (insertions) or substitutions than the reference text. For `whisper-tiny` on zero-shot Azerbaijani, this reflects the model's struggle with phonetic alignment without language-specific tuning.

### Part B3 — Base vs Fine-Tuned Comparison (Test Set)
| Model                    | WER (%) | CER (%) | WER Δ    | CER Δ    |
|--------------------------|---------|---------|----------|----------|
| Whisper-tiny (Base)      | 119.94  | 78.55   | -        | -        |
| Whisper-tiny (Fine-Tuned)| 117.09  | 74.01   | -2.85%   | -4.54%   |

### 🏆 Best & Worst Samples (Base Model)
Full results are available in `results/part_a_results.csv`.
* **Best Sample:** WER 0.50 | CER 0.26
* **Worst Sample:** WER 21.00 | CER 15.00+ 

---

## ⚙️ Model & Training Parameters
* **Base model:** `openai/whisper-tiny` (39M)
* **Dataset:** `google/fleurs` (az_az)
* **Learning rate:** 1e-5 | **Batch size:** 8 | **Max steps:** 50

> 💡 **Dataset Selection Rationale:**
> Although the task prompt suggested the Mozilla Common Voice dataset, this pipeline utilizes `google/fleurs` (az_az). The Common Voice dataset currently requires an explicit Hugging Face authentication token (`HF_TOKEN`) and manual user consent agreement. To ensure that this repository is fully reproducible out-of-the-box for the reviewer without requiring them to set up API keys or accounts, `google/fleurs` was chosen as a high-quality, open-access alternative.

---


## 🚀 Setup & Run Instructions

1. Clone the repository and install dependencies:
```bash
git clone <https://github.com/IbragimCoder/az-stt-intern>
cd az-stt-intern
pip install -r requirements.txt
```
2. Part A — Base model evaluation:
```bash
Navigate to the part_a directory and execute the notebook:
cd part_a
jupyter nbconvert --to notebook --execute part_a.ipynb
```

3. Part B — Fine-tuning pipeline:
Navigate to the part_b directory to run the training process:
```bash
cd part_b
jupyter nbconvert --to notebook --execute part_b.ipynb
```
