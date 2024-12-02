# Interspeech 2025 - Speech Emotion Recognition in Naturalistic Conditions Challenge
# Baselines Training and Evaluation

The Speech Emotion Recognition (SER) in Naturalistic Conditions Challenge at Interspeech 2025 aims to advance the field of emotion recognition from spontaneous speech, emphasizing real-world applicability over controlled, acted scenarios. Utilizing the MSP-Podcast corpus — a rich dataset of over 324 hours of naturalistic conversational speech — the challenge provides a platform for researchers to develop and benchmark SER technologies that perform effectively in complex, real-world environments. Participants have access to speaker-independent training and development sets, as well as an exclusive test set, all annotated for two distinct tasks: categorical emotion recognition and emotional attributes prediction.

This repository contains scripts to train and evaluate baseline models on various tasks including categorical emotion recognition and multi-task emotional attributes prediction.

#### Refer to the links below to sign up for the challenge and to find information about the rules, submission deadlines, file formatting instructions, and more:

Link to the challenge: [Interspeech 2025 - Speech Emotion Recognition in Naturalistic Conditions Challenge](https://lab-msp.com/MSP-Podcast_Competition/IS2025/)


Link to previous challenge paper (Odyssey 2024 - SER Challenge): [PDF](https://ecs.utdallas.edu/research/researchlabs/msp-lab/publications/Goncalves_2024.pdf)

The paper contains baseline implementation details. See citation bellow:

```
@inproceedings{Goncalves_2024,
  title     = {Odyssey 2024 - Speech Emotion Recognition Challenge: Dataset, Baseline Framework, and Results},
  author    = {Lucas Goncalves and Ali N. Salman and Abinay Reddy Naini and Laureano Moro-Velázquez and Thomas Thebaud and Paola Garcia and Najim Dehak and Berrak Sisman and Carlos Busso},
  year      = {2024},
  booktitle = {The Speaker and Language Recognition Workshop (Odyssey 2024)},
  pages     = {247--254},
  doi       = {10.21437/odyssey.2024-35},
}
```


## Environment Setup

Python version = 3.9.7

To replicate the environment necessary to run the code, you have two options:

### Using Conda

1. Ensure that you have [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/) installed.
2. Create a conda environment using the `spec-file.txt` by running:
    conda create --name baseline_env --file spec-file.txt
3. Activate the environment:
    conda activate baseline_env
4. Make sure to install the transformers library as it is essential for the code to run:
    pip install transformers


### Using pip

1. Alternatively, you can use `requirements.txt` to install the necessary packages in a virtual environment:
    python -m venv myenv
    source myenv/bin/activate
    pip install -r requirements.txt
2. Make sure to install the transformers library as it is essential for the code to run:
    pip install transformers


## Configuration

Before running the training or evaluation scripts, check instructions below and update the `./configs/config_dim.json` and `./configs/config_cat.json` files with the paths to your local audio folder and label CSV file.

### Categorical Emotion Recognition Model

Before running training or evaluation of the categorical emotion recognition model, please execute the script `process_labels_for_categorical.py` to properly format the provided `labels_consensus.csv` file for categorical emotion recognition. Place the path to the processed .csv file in the `./configs/config_cat.json` file to run this configuration.

### Attributes Emotion Recognition Model

The original `labels_consensus.csv` file provided with the dataset can be used as is for attributes emotion recognition. Please place the path to the `labels_consensus.csv` file in the `./configs/config_dim.json` file to run this configuration.

## Inferencing

### HuggingFace

If you are only interested in using the pretrained models for prediction or feature extraction, we have made the models available on HuggingFace.

 #### Models on HuggingFace (Interspeech 2025)
  - [ ] Categorical model (TBA)
  - [ ] Multi-task attribute model (TBA)

  #### Previous Models on HuggingFace (Odyssey 2024)
  - [x] [Categorical model](https://huggingface.co/3loi/SER-Odyssey-Baseline-WavLM-Categorical)
  - [x] [Multi-task attribute model](https://huggingface.co/3loi/SER-Odyssey-Baseline-WavLM-Multi-Attributes)   -  [Emotional Attributes Prediction App/Demo](https://huggingface.co/spaces/3loi/WavLM-SER-Multi-Baseline-Odyssey2024)


## Training and Evaluation

To train or evaluate the models, use the provided shell scripts. Here's how to use each script:

- `bash run_cat.sh`: Trains or evaluates the categorical emotion recognition baseline.
- `bash run_dim.sh`: Trains or evaluates the multi-task emotional attributes prediction baseline.


### Models

The models are to be saved in the `model` folder. If you are evaluating the pretrained models, please download the models using the script provided in the `model` folder at `./model/download_models.sh`. 
  ```
  $ bash download_models.sh <categorical|attributes|all>
  ```
- Example 1: `bash download_models.sh all` to download all the models.
- Example 2: `bash download_models.sh categorical` to download categorical model only.

If you wish to manually download a pre-trained model, please visit this [website](https://lab-msp.com/MSP-Podcast_Competition/IS2025/models/) and download the desired model and place them in the `model` folder. 

Pre-trained models file descriptions:
- "cat_ser.zip" --> Categorical emotion recognition baseline.
- "dim_ser.zip" --> Multi-task emotional attributes baseline.



### Evaluation Only

If you are only evaluating a model and do not wish to train it, comment out the lines related to `python train_eval_files/train_****_.py` in the respective run `.sh` file.

### Evaluation and saving results for emotional attributes prediction

A custom executable sample file for evaluation and results saving has been provided `./train_eval_files/eval_dim_ser.py`. To execute, just download or train the multi-task emotional attributes baseline. The script `bash run_dim.sh` already has execution code to run this set up (Note: If you will not be training the entire model again, please comment out the training lines in `run_dim.sh` before evaluation). The results will be saved in the correct `.csv` format and it will be located in a `results` folder created inside your model path location.

## Issues

If you encounter any issues while setting up, training, or evaluating the models, please open an issue on this repository with a detailed description of the problem.

---------------------------
To cite this repository in your works, use the following BibTeX entry:

```
@inproceedings{Goncalves_2024,
  title     = {Odyssey 2024 - Speech Emotion Recognition Challenge: Dataset, Baseline Framework, and Results},
  author    = {Lucas Goncalves and Ali N. Salman and Abinay Reddy Naini and Laureano Moro-Velázquez and Thomas Thebaud and Paola Garcia and Najim Dehak and Berrak Sisman and Carlos Busso},
  year      = {2024},
  booktitle = {The Speaker and Language Recognition Workshop (Odyssey 2024)},
  pages     = {247--254},
  doi       = {10.21437/odyssey.2024-35},
}
```

