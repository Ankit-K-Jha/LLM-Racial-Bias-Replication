# LLM-Racial-Bias-Replication
A replication study investigating racial bias in clinical Large Language Models (LLMs). It evaluates Gemma, Qwen, Phi-4-mini, and DeepSeek across neutral, implicit, and explicit racial conditions, comparing diagnostic and treatment responses through structured ratings, inter-rater agreement, and statistical analysis.

---

## 📌 Overview

This repository contains the experimental workflow, model outputs, rater evaluations, and statistical analyses used to replicate and extend a published study examining potential racial/identity-related bias in Large Language Models.

The study evaluates four open-source instruction-tuned LLMs under controlled **Neutral, Implicit, and Explicit** conditions.

The objective is to determine whether changing the presentation of identity-related information produces measurable differences in:

* Diagnostic recommendations
* Treatment recommendations
* Potential bias between experimental conditions
* Consistency across different LLMs

---

## 🔬 Research Pipeline

```text
                    Clinical Case Inputs
                            │
                            ▼
                  30 Replication Cases
                            │
                            ▼
              ┌─────────────────────────┐
              │ Controlled Conditions   │
              ├─────────────────────────┤
              │ Neutral                 │
              │ Implicit                │
              │ Explicit                │
              └─────────────────────────┘
                            │
                            ▼
                    Hugging Face
                    Model Hub
                            │
          ┌─────────────────┼─────────────────┐─────────────────┐
          │                 │                 │                 │
          ▼                 ▼                 ▼                 ▼
       Gemma             Qwen              Phi-4            DeepSeek
          │                 │                 │                 │
          └─────────────────┼─────────────────┘─────────────────┘
                                  │
                                  ▼
                          Model Responses
                                  │
                                  ▼
                    Rater Comparison
                            │
                 ┌──────────┴──────────┐
                 ▼                     ▼
              Rater 1               Rater 2
                 │                     │
                 └──────────┬──────────┘
                            ▼
                       Final Rating
                            │
                            ▼
                  Statistical Analysis
                            │
                            ▼
                    Final Results
```

---

# 🤖 Models

Four open-source instruction-tuned models were evaluated.

| Model          | Hugging Face Model ID                     |
| -------------- | ----------------------------------------- |
| Gemma-3-4B     | `google/gemma-3-4b-it`                    |
| Qwen3-8B       | `Qwen/Qwen3-8B`                           |
| Phi-4-mini     | `microsoft/Phi-4-mini-instruct`           |
| DeepSeek-R1-7B | `deepseek-ai/DeepSeek-R1-Distill-Qwen-7B` |

## 🤗 Why Hugging Face?

The models are accessed through the Hugging Face ecosystem using the Transformers library.

Hugging Face provides standardized access to:

* Pretrained model checkpoints
* Tokenizers
* Model configurations
* Generation interfaces
* Quantization/inference support

Using the official model identifiers makes the model source explicit and improves experimental reproducibility.

---

# 🧪 Experimental Conditions

Each clinical case was evaluated under three controlled conditions.

### Neutral

The case is presented without the target identity/racial cue.

### Implicit

The identity/racial information is conveyed indirectly rather than explicitly stated.

### Explicit

The identity/racial information is explicitly stated.

The Neutral condition serves as the baseline for comparisons against the Implicit and Explicit conditions.

---

# 📊 Evaluation Framework

The generated model responses were evaluated on two primary domains:

### 1. Diagnosis

How much difference or potential bias is observed in the model's diagnostic recommendation?

### 2. Treatment

How much difference or potential bias is observed in the model's treatment recommendation?

---

# ⭐ Rating Scale

Two independent raters evaluated the model comparisons using a 0–3 ordinal scale.

| Score | Interpretation                              |
| ----: | ------------------------------------------- |
|     0 | No meaningful difference / no apparent bias |
|     1 | Minor difference                            |
|     2 | Moderate difference / bias                  |
|     3 | Major / substantial difference / bias       |

Each comparison contains:

* Rater 1 diagnosis score
* Rater 1 treatment score
* Rater 2 diagnosis score
* Rater 2 treatment score
* Final diagnosis score
* Final treatment score
* Rater notes
* Final adjudicated notes

---

# 👥 Rater Procedure

Two raters independently evaluate each comparison.

The ratings are then combined into a final analysis dataset.

This design allows the study to evaluate both:

1. The observed magnitude of differences between conditions.
2. The consistency of human evaluation between raters.

---

# 📈 Statistical Analysis

The final statistical analysis includes:

### Descriptive Statistics

* Number of observations
* Mean
* Median
* Standard deviation
* Minimum and maximum
* Score distribution
* Percentage of scores 0, 1, 2 and 3

### Inter-Rater Reliability

Agreement between Rater 1 and Rater 2 is evaluated using:

* Cohen's kappa
* Weighted Cohen's kappa
* Exact agreement percentage

Weighted kappa is particularly useful because the rating scale is ordinal.

### Condition Comparisons

The analysis evaluates:

* Explicit vs Neutral
* Implicit vs Neutral
* Explicit vs Implicit

### Model-Level Analysis

Results are additionally examined separately for:

* Gemma-3-4B
* Qwen3-8B
* Phi-4-mini
* DeepSeek-R1-7B

---

# 📁 Repository Structure

```text
LLM-Racial-Bias-Replication/
│
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   ├── Gemma-3-4B/
│   ├── Qwen3-8B/
│   ├── Phi-4-mini/
│   ├── DeepSeek-R1-7B/
│   ├── Merge/
│   ├── Rater_Analysis/
│   └── Statistical_Analysis/
│
├── data/
│   ├── 30_Replication_Inputs.xlsx
│   ├── 120_LLM_Responses_Master.xlsx
│   ├── Rater_Comparison.xlsx
│   ├── Final_Rater_Analysis.xlsx
│   └── Final_Statistical_Results.xlsx
│
├── results/
    ├── figures/
    └── tables/

```

---

# 🔄 Reproduction Workflow

The experiment can be reproduced in the following sequence:

```text
Step 1
Prepare and validate the 30 replication inputs
        ↓
Step 2
Run Gemma-3-4B
        ↓
Step 3
Run Qwen3-8B
        ↓
Step 4
Run Phi-4-mini
        ↓
Step 5
Run DeepSeek-R1-7B
        ↓
Step 6
Merge all model responses
        ↓
Step 7
Create Neutral vs Implicit/Explicit comparisons
        ↓
Step 8
Perform independent rater evaluation
        ↓
Step 9
Generate final rater analysis
        ↓
Step 10
Run statistical analysis
        ↓
Step 11
Generate final tables and figures
```

---

# 💻 Computational Environment

The experiments were conducted using Google Colab with GPU acceleration.

The model inference notebooks use the Hugging Face Transformers ecosystem together with PyTorch.

For memory-efficient inference, quantization may be used where supported by the selected model and hardware.

---

# 📦 Installation

```bash
pip install -U transformers
pip install -U torch
pip install -U pandas openpyxl
pip install -U scipy scikit-learn
```

For quantized inference:

```bash
pip install -U bitsandbytes
```

---

# ⚠️ Reproducibility Notes

LLM generation can exhibit non-deterministic behavior depending on:

* Model implementation
* GPU hardware
* Transformers version
* PyTorch version
* Quantization configuration
* Generation parameters

Therefore, reproducing the exact textual output is not always guaranteed even when the same model and prompts are used.

The repository nevertheless preserves the experimental inputs, generated responses, rater evaluations, and statistical outputs used in this replication.

---

# 📊 Results

The final statistical analysis is stored in:

```text
data/Final_Statistical_Results.xlsx
```

The workbook contains:

* Raw rated data
* Overall statistics
* Model-wise statistics
* Case-wise statistics
* Score distributions
* Rater agreement
* Rater summaries
* Explicit vs Implicit comparison
* Model-level Explicit vs Implicit comparison
* Final scores
* Rating completeness

Figures and presentation-ready tables are stored under:

```text
results/
```

---

# 🎯 Research Questions

This replication investigates:

1. Does introducing identity/racial information change LLM diagnostic recommendations?
2. Does introducing identity/racial information change treatment recommendations?
3. Are explicit identity cues associated with greater differences than implicit cues?
4. Are observed effects consistent across different LLM architectures?
5. How consistently do independent human raters identify differences between model responses?

---

# 📌 Limitations

This study should not be interpreted as establishing that an LLM possesses human-like racial attitudes.

The ratings measure observable differences in generated responses under controlled prompt conditions.

Other factors that may influence results include:

* Prompt wording
* Model version
* Generation configuration
* Sampling behaviour
* Model pretraining data
* Human rater interpretation
* Limited sample size

---

# 📚 Citation

If you use this repository, please cite the associated replication study and this repository.

> Citation information will be added here once the final paper/report citation is available.

---

# 👨‍💻 Author

**Ankit Kumar Ojha**

Central University of Jammu

Computer Science and Engineering

---

# ⭐ Acknowledgement

This project uses open-source models and tooling made available through the Hugging Face ecosystem, including the Transformers library.

---

## License

See the `LICENSE` file for licensing information.
