EM-VLM4AD — Hyperparameter Tuning Extension

This repository contains my modifications and experiments for hyperparameter tuning of the EM-VLM4AD multimodal driving-reasoning model.
The work is part of my course project, focusing on evaluating and improving decoding strategies for the model’s question-answering performance.
This repo does not contain the full original implementation.
Instead, it includes only the modified files and the notebook used to run experiments, keeping the repo clean and focused on the hyperparameter-tuning contribution.


1. Original Repository (Base Code Used)

The complete EM-VLM4AD codebase was cloned from: https://github.com/akshaygopalkr/EM-VLM4AD
All dataset preparation, model loading, and evaluation scripts originate from this repo.

2. What This Repository Contains
This repository includes the following files:

A] multi_frame_model.py
Modified version of the original Multi-Frame model.
Changes include additional decoding strategies for experimentation:
Beam Search (num_beams = 4)
Top-p Sampling (top_p = 0.9)
Temperature Sampling (temperature = 0.3)
Modified Max-Output Length (max_length = 256)

Each decoding strategy is implemented as a separate line in the generate() function.

B]Hyperparameter_Tuning.ipynb
A Colab-ready notebook that:
Loads the original model
Replaces the Multi-Frame model with the modified version
Runs evaluation on the DriveLM dataset
Saves metric outputs for comparison (BLEU, METEOR, ROUGE, CIDEr; SPICE skipped due to Java issue)

3. How to Use This Repository
Step 1 — Clone the Original Full Codebase
git clone https://github.com/akshaygopalkr/EM-VLM4AD

Step 2 — Replace the Model File
Copy the provided modified file into the cloned directory:
EM-VLM4AD/multi_frame_model.py   →   replace with this repo's multi_frame_model.py

Step 3 — Open the Notebook
Open Hyperparameter_Tuning.ipynb inside Google Colab.
Make sure to mount Google Drive if storing checkpoints there.

4. Selecting a Decoding Strategy

Inside multi_frame_model.py, in the generate() function, multiple decoding strategies are provided.

Only one decoding line should be active at a time.
To run a particular experiment:
Example — Beam Search

Uncomment:

output_ids = self.model.generate(attention_mask=attention_mask,
                                 decoder_input_ids=decoder_input_ids,
                                 inputs_embeds=merged_embedding,
                                 max_length=512,
                                 num_beams=4,
                                 early_stopping=True)

And comment out all others:
# Temperature sampling
# Top-p sampling
# Max-length modification
Repeat this for each strategy to generate separate evaluation results.

5. Dataset & Checkpoints
   
Follow the original repo instructions to download:
DriveLM dataset
Multi-frame checkpoints (T5-base or T5-large)
Modify paths inside the notebook as needed.

6. Outputs & Evaluation

Each run generates:
BLEU-1/2/3/4
METEOR
ROUGE-L
CIDEr

(SPICE is ignored due to Java incompatibility in Colab)
These metrics were used in the course project to compare baseline vs tuned results.

7. Purpose of This Repository

This repo exists solely to document:

My hyperparameter modifications
The exact model code used
The notebook that reproduces my evaluation results

It is not intended as a replacement for the full EM-VLM4AD implementation.
