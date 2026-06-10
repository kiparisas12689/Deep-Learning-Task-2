# Lithuanian Informal-to-Formal Dataset Project

## Overview

This project contains an original Lithuanian informal-to-formal text rewriting dataset and fine-tuning workflows for experimenting with different language models.

The task is:

- input: informal Lithuanian comment
- output: formal, grammatically corrected Lithuanian rewrite

This fits the assignment because Lithuanian is a lower-resource language and the dataset was manually assembled for this project.

## Main Files

- [lt_formal_dataset_464.json]
- [main_workflow_cpu.ipynb]
- [main_gemma3.ipynb]
- [ASSESSMENT_NOTES.md]
- [requirements.txt]

## Dataset

### Size

- Total examples: 464
- Train examples: 358
- Test examples: 106

### Structure

Each row contains:

- `id`
- `informal_text`
- `formal_text`
- `split`

### Data Creation

The dataset was built from two manually prepared sources:

1. Lithuanian Facebook comment pairs.
2. Lithuanian Reddit comment pairs.

The final dataset is original in the sense that the input-output rewriting pairs were manually assembled and rewritten for this coursework project rather than copied from an existing benchmark.

### Annotation Rules

When creating `formal_text`, the main rules were:

1. fix spelling and punctuation,
2. restore Lithuanian diacritics where needed,
3. remove or soften slang, profanity, or highly informal wording,
4. preserve the original meaning as closely as possible,
5. rewrite the result in a more formal style.

## Fine-Tuning Setup

The project includes experiments with two model configurations.

### 1. mT5-Small + LoRA (`main_workflow_cpu.ipynb`)

- base model: `google/mt5-small`
- fine-tuning method: `LoRA`
- task type: sequence-to-sequence rewriting
- notebook mode: lightweight defaults for weak hardware

This workflow was designed for CPU-friendly experimentation and serves as the primary training pipeline.

### 2. Gemma 3 1B (`main_gemma3.ipynb`)

Additional experiments were conducted using the `Gemma 3-1B` model to evaluate the performance of a larger language model on the informal-to-formal rewriting task.

Evaluation was performed on the held-out test set containing **106 examples**. The following metrics were obtained:

- BLEU: **3.716**
- ROUGE-L: **0.22**
- Perplexity: **46.8**

These experiments provide a comparison against the smaller mT5-based setup while remaining feasible on limited hardware.

The initial setup attempted to use larger models, which had difficulty running because of higher computational requirements, so the final project focuses on configurations that remain accessible on modest hardware.

## How To Run

### CPU-Friendly LoRA Workflow

Open:

- [main_workflow_cpu.ipynb]

Run the notebook from top to bottom.

The notebook contains:

1. dependency installation,
2. dataset inspection,
3. CPU-friendly LoRA training,
4. prediction generation,
5. evaluation,
6. single-example demo inference.

### Gemma 3 Workflow

Open:

- [main_gemma3.ipynb]

Run the notebook from top to bottom to reproduce the Gemma 3 experiments and evaluation metrics.

## Outputs

The notebooks save artifacts in:

- [outputs]

Important output files include:

- saved model/adapters,
- test predictions,
- evaluation reports,
- generated metrics.

## Notes

This project was simplified toward the end to focus on reproducible notebook-based workflows. Earlier heavier model experiments are no longer required for the final setup.

If you use a stronger hardware setup, you can increase:

- epochs,
- number of training samples,
- model size,
- or hyperparameter search complexity.
