# STGATE
This repo is dedicated to the STGATE: Spatial-Temporal Graph Attention network with a Transformer Encoder for EEG-based emotion recognition
[link to the original paper](https://www.frontiersin.org/articles/10.3389/fnhum.2023.1169949/full)

## Structure of the repo

- `lib`: The directory with current DL models, scripts for running some preprocessing and so on

- `experiments`: Several runs in jupyter notebooks to evaluate models from lib

- `data`: The folder to put the EEG data from [DREAMER](https://zenodo.org/record/546113), [SEED](https://bcmi.sjtu.edu.cn/home/seed/downloads.html) and SEED IV datasets (and write in code relative path to it)

- `literature`:  The sources for our research

##  Goals of the research
- [ ] Receive the *Accuracy score* from the [article](https://www.frontiersin.org/articles/10.3389/fnhum.2023.1169949/full):
  - [ ] 90.37% in SEED
  - [ ] 76.43% in SEED-IV
  - [x] 77.44% and 75.26% in the valence and arousal dimensions of the DREAMER (Done for GCNN model)
- [ ] 

## TODO list
- [ ] Create preprocessing script (in lib/) for EEG data to pass data into the model (now it is in )
- [x] ~~Understand the input shape and format of data for the GNN model (Georgiy), until 18.10~~
- [x] ~~Almost copy-paste~~ ~~Implement the GNN model from https://github.com/xyk0058/STGAT (Georgiy), until 19.10~~
- [x] (OPTIONAL) Maybe add some architecture from https://github.com/hulianyuyy/STGAT/tree/main

## Experiments
All experiments with architectures and data preprocessing are described as .ipynb and other logs/reports in [experiments/](https://github.com/mrph2898/STGATE/tree/main/experiments) folder.
- [STGAT_METR_LA_colab_run.ipynb](https://github.com/mrph2898/STGATE/blob/main/experiments/STGAT_METR_LA_colab_run.ipynb)
  
  First attempt with STGAT architecture was on METR-LA dataset. The code (train.py, utils.py, lib/generate_training_data.py, lib/data_preparation.py, lib/metrics.py, lib/utils.py) was taken simply from [STGAT repo](https://github.com/xyk0058/STGAT).
  
  There was regression problem of traffic forecasting with GNN.
  The *main disadvantage* - we should somehow estimate the original adjacency matrix.
  
  But this model simply was used to check the architecture - the logs is located in Weights&Biases [here](https://wandb.ai/mrph2898/STGAT?workspace=user-gkormakov) and generated as the report in this repo [STGAT_reproducibility report](https://github.com/mrph2898/STGATE/blob/main/experiments/STGAT_reproducibility_WB_report_few_steps.pdf)
  
- [experiments/EEG_DatasetsCreation.ipynb](https://github.com/mrph2898/STGATE/blob/main/experiments/EEG_DatasetsCreation.ipynb)

  This notebook was created after several attempts of data preprocessing. We've found the [torcheeg](https://torcheeg.readthedocs.io/en/latest/torcheeg.datasets.html) library with great datasets preparation for Dataloders  for CNN's architectures as well as for GNNs.

  The methods in this notebooks will create tmp directory with the specific observations of time series. As the example, we've used DREAMER dataset. The preprocessing for it was only adding the [adjacency matrix](https://github.com/torcheeg/torcheeg/blob/main/torcheeg/datasets/constants/emotion_recognition/dreamer.py) (from the electrode placement, which is stored also in constants in torcheeg).

  For SEED and SEED IV we also generated the preprocessed data, but it takes 40 Gb of the space, so we reproduce (up to the 2023.10.28) only the DREAMER results of classification.

- [STGATE_run_DREAMER](https://github.com/mrph2898/STGATE/blob/main/experiments/STGATE_run_DREAMER.ipynb)

  The main notebook for the classification model on the DREAMER. Instead of using the attention layers on 2d (as for traffic and skeleton-based STGAT), we should take 1d Convs on our channels.
  But then, in the attention layer we had the shape mismatch problem (up to the 2023.10.28). So, this notebook is about the unsuccess

- [DGCNN_RUN](https://github.com/mrph2898/STGATE/blob/main/experiments/DGCNN_RUN.ipynb)

  If simply take the CNN instead of attention layers, we will receive the DGCNN network. The run of this model is described in this notebook.

  The logs of two runs (for arousal and valence classes of DREAMER) are located [here, WB](https://wandb.ai/mrph2898/lightning_logs?workspace=user-gkormakov) and, as the pdf-report, in this repo [DGCNN_DREAMER report](https://github.com/mrph2898/STGATE/blob/main/experiments/DGCNN_DREAMER%20lightning_logsWB_report.pdf)

## Models
All architectures, somehow related to the STGATE, are located in [models/](https://github.com/mrph2898/STGATE/tree/main/models) directory.

The main architectures are models/stgat.py and models/stgate.py. But they are not working properly for the classification (up to the 2023.10.28)  
  
