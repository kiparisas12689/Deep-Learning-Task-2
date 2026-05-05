# Lithuanian Informal-to-Formal Dataset Project

## Overview

This project contains an original Lithuanian informal-to-formal text rewriting dataset and a CPU-friendly LoRA fine-tuning notebook.

The task is:

- input: informal Lithuanian comment
- output: formal, grammatically corrected Lithuanian rewrite

This fits the assignment because Lithuanian is a lower-resource language and the dataset was manually assembled for this project.

## Main Files

- [lt_formal_dataset_303.json]
- [main_workflow_cpu.ipynb]
- [ASSESSMENT_NOTES.md]
- [requirements.txt]

## Dataset

### Size

- Total examples: 303
- Train examples: 242
- Test examples: 61

### Structure

Each row contains:

- `id`
- `informal_text`
- `formal_text`
- `split`

### Data Creation

The dataset was built from two manually prepared sources:

1. 203 Lithuanian Facebook comment pairs.
2. 100 Lithuanian Reddit comment pairs.

The final dataset is original in the sense that the input-output rewriting pairs were manually assembled and rewritten for this coursework project rather than copied from an existing benchmark.

### Annotation Rules

When creating `formal_text`, the main rules were:

1. fix spelling and punctuation,
2. restore Lithuanian diacritics where needed,
3. remove or soften slang, profanity, or highly informal wording,
4. preserve the original meaning as closely as possible,
5. rewrite the result in a more formal style.

## Fine-Tuning Setup

The final notebook version is designed for CPU-friendly experimentation:

- base model: `google/mt5-small`
- fine-tuning method: `LoRA`
- task type: sequence-to-sequence rewriting
- notebook mode: lightweight defaults for weak hardware

The initial setup attempted to use large-models, which had trouble running because of high computational expenses, so we switched to smaller scale models.

## How To Run

Open:

- [main_workflow_cpu.ipynb]

Run the notebook from top to bottom.

The notebook already contains:

1. dependency installation,
2. dataset inspection,
3. CPU-friendly LoRA training,
4. prediction generation,
5. evaluation,
6. single-example demo inference.

## Outputs

The notebook saves artifacts in:

- [outputs]

Important output files:

- saved LoRA adapter model
- test predictions
- evaluation report

## Notes

This project was simplified toward the end to focus on a single notebook workflow. Earlier heavier model experiments are no longer required for the final setup.

If you use a stronger setup you can increase:

- epochs,
- number of training samples,
- or model size.
