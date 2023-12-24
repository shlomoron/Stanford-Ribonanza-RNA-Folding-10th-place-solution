# Stanford-Ribonanza-RNA-Folding-10th-place-solution
This repository contains my solution (10th place, gold medal) for the Kaggle competition of [Stanford Ribonanza RNA Folding
](https://www.kaggle.com/competitions/stanford-ribonanza-rna-folding) (ASLFR).   

## The steps to reproduce my solution
### 1. Turning the prone-to-OOM errors CSV into friendly NP arrays
This is [done here](https://www.kaggle.com/code/shlomoron/srrf-solution-1-csv-to-np).
### 2. Turning the data into TFRecords
This is [done here](https://www.kaggle.com/code/shlomoron/srrf-solution-2-tfrecords). The data include the competition's training data, given bpps, and CapR values for the sequences. I calculated the CapR values using [ratthachat's notebook](https://www.kaggle.com/code/ratthachat/preprocessing-deep-learning-input-from-rna-string). You can find the CapR values dataset [here](https://www.kaggle.com/datasets/shlomoron/srrf-train-set-capr).
### 3. Training the models
This is [done here](https://www.kaggle.com/shlomoron/srrf-soltion-3-model-training). I trained two kinds of models. The first one (model_1) was trained only on the sequences data. The second one (model_2) included bpp sum&max features and CapR values for each nucleotide. In the notebook, I trained a +bpp&CapR model. To train a sequence-only model, look for 'class one_hot_and_mask_layer' and change it according to the instructions there.
### 4. Ensembling, inferencing, and submitting
This is less interesting. I will just give some details about ensembling: I ensembled 30 model_1 and 16 model_2, each trained with randomized hyperparameters (see the training notebook in #2 for more information). The model_1 ensemble achieved 0.14133/0.14304 public/private LB scores. The model_2 ensemble achieved 0.14094/0.14299 public/private LB scores. An ensemble of both ensembles with 2.5:5.5 weights in favor of model_2 achieved 0.1402/0.14199 public/private LB scores. This score is significantly higher than my final score since I was too suspicious of bpp/CapR and submitted the model_1 ensemble and ensemble of both model_1 and model_2 ensembles with very conservative weights of 5:3 in favor of model_1, which achieved the score of 0.14133/0.14304 public/private LB scores. For more details and discussion about my solution, check my write-up on the Kaggle forums.

