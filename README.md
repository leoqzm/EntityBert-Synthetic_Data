# EntityBert-Synthetic_Data
Follow the instruction in the [SyntheticDataGeneration.ipynb](SyntheticDataGeneration.ipynb) notebook to run the synthetic data generation steps
## First need to download and build anaconda environment
Need to change the path
```
/content/drive/MyDrive/transformer-models-trained-on-mimic-iii-to-generate-synthetic-patient-notes-1.0.0/environment.yml
``` 
To the environment.yml in your directory

## Need to run the bash code and change the input output file path in the code block
```
%%bash
source activate mimic-discharge-summaries

#!/bin/bash

cd /content/drive/MyDrive/transformer-models-trained-on-mimic-iii-to-generate-synthetic-patient-notes-1.0.0/transformer

TEST_FILE=#NEED to change to input file path
PROBLEM=mimic_discharge_summaries
MODEL=transformer
HPARAMS=transformer_base
DATA_DIR=./data
TRAIN_DIR=./output
USR_DIR=.

BEAM_SIZE=4
ALPHA=0.6
DBS=4
EXTRA_LEN=50
HPARAMS_OVERRIDE="max_length=10000,max_target_seq_length=512,max_input_seq_length=512"

t2t-decoder \
    --t2t_usr_dir=$USR_DIR \
    --data_dir=$DATA_DIR \
    --problem=$PROBLEM \
    --model=$MODEL \
    --hparams_set=$HPARAMS \
    --hparams=$HPARAMS_OVERRIDE \
    --output_dir=$TRAIN_DIR \
    --decode_hparams="beam_size=$BEAM_SIZE,alpha=$ALPHA,batch_size=$DBS,extra_length=$EXTRA_LEN" \
    --decode_from_file=$TEST_FILE \
    --decode_to_file=#NEED to change to output file
```
