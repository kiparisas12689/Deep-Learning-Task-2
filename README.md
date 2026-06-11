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

## Training Dynamics and Model Comparison

### Gemma 3 1B

The training and validation loss curves for the Gemma 3-1B model show rapid learning during the first few epochs. Training loss decreases steadily throughout training, while validation loss reaches its lowest value around **epoch 5**.

After epoch 5, validation loss begins to increase even though training loss continues to decrease. This suggests that the model starts to overfit the training data beyond this point. Consequently, the checkpoint from approximately epoch 5 provides the best generalization performance on the validation set.

This behavior indicates that Gemma 3-1B is able to learn the rewriting task relatively quickly and extract useful patterns from the dataset within a small number of epochs.

### mT5-Small + LoRA

The mT5-Small model exhibits a different training pattern. Both training and validation loss decrease gradually over a much larger number of epochs, showing a slower but more stable convergence process.

Unlike Gemma 3-1B, the validation loss does not show a strong increase after the early stages of training. Instead, it continues to improve incrementally as training progresses, suggesting a lower tendency toward early overfitting.

### Overall Comparison

The two models demonstrate different learning characteristics:

- **Gemma 3-1B** learns quickly and reaches its best validation performance after only a few epochs.
- **mT5-Small + LoRA** converges more slowly and steadily over time.
- The Gemma model achieves stronger overall performance on the Lithuanian informal-to-formal rewriting task, as reflected by the evaluation metrics obtained on the held-out test set.

These observations suggest that the larger Gemma 3-1B model is better able to capture the linguistic transformations required for the task, although careful checkpoint selection or early stopping is important to avoid overfitting.

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
