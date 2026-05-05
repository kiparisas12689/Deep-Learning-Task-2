# Assessment Notes

## Short Description

I created an original Lithuanian informal-to-formal rewriting dataset with 303 examples. Each example contains an informal Lithuanian comment and a manually prepared formal rewrite.

## Why This Fits the Assignment

1. The dataset is original and task-specific.
2. It targets Lithuanian, which is a lower-resource language.
3. It supports fine-tuning for a clear transformation task.
4. The model can be demonstrated on unseen Lithuanian inputs during checkout.

## Dataset Creation

The dataset was created from two manually assembled sources:

1. 203 Lithuanian Facebook comment pairs.
2. 100 Lithuanian Reddit comment pairs.

The comments were rewritten into formal Lithuanian and stored in JSON format with:

- `id`
- `informal_text`
- `formal_text`
- `split`

## Annotation Logic

For each formal rewrite, I:

1. fixed grammar, spelling, and punctuation,
2. restored Lithuanian diacritics,
3. reduced slang and profanity,
4. preserved the original meaning as closely as possible,
5. rewrote the output in a more formal register.

## Fine-Tuning Choice

I used LoRA because:

1. it is a recognized advanced technique,
2. it is more efficient than full fine-tuning,
3. it is more realistic for limited hardware,
4. it still demonstrates real model adaptation on the dataset.

For the final CPU-friendly notebook, I used `google/mt5-small` with LoRA to make local training more feasible.

## Evaluation

I evaluate the model using:

1. exact match,
2. normalized exact match,
3. character similarity,
4. manual inspection of meaning preservation and formality.

##  Limitations

1. The dataset is relatively small.
2. Some rewrites are softened rather than literally preserving profanity.
3. CPU-only training required a lighter model and lighter training settings.

## What Could Be Improved

1. train on the full dataset for longer,
2. use stronger hardware,
3. add a validation split,
4. collect more examples,
5. compare multiple base models.
