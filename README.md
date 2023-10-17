# STGATE
This repo is dedicated to the STGATE: Spatial-Temporal Graph Attention network with a Transformer Encoder for EEG-based emotion recognition
[link to the original paper](https://www.frontiersin.org/articles/10.3389/fnhum.2023.1169949/full)

## Structure of the repo

- `lib`: The directory with current DL models, scripts for running some preprocessing and so on

- `experiments`: Several runs in jupyter notebooks to evaluate models from lib

- `data`: The folder to put the EEG data from [DREAMER](https://zenodo.org/record/546113), [SEED](https://bcmi.sjtu.edu.cn/home/seed/downloads.html) dataset (and write in code relative path to it)

- `literature`:  The sources for our research

## TODO list
- [ ] Create preprocessing script (in lib/) for EEG data to pass data into the model (Mike/Marco), until 18.10
- [ ] Understand the input shape and format of data for the GNN model (Georgiy), until 18.10
- [ ] ~~Almost copy-paste~~ Implement the GNN model from https://github.com/xyk0058/STGAT (Georgiy), until 19.10
- [ ] (OPTIONAL) Create the presentation for the Friday (20.10) pre-defence (but Maria has said that we can simply send the code and show some plots) 
- [ ] (OPTIONAL) Maybe add some architecture from https://github.com/hulianyuyy/STGAT/tree/main
