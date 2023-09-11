# A lightweight SelfONN model for general ECG classification with
pretraining

This repository is accompanying our upcoming article [A lightweight SelfONN model for general ECG classification with
pretraining](https://doi.org/xxxx), which builds on three datasets,
(1) [Icentia11K](https://academictorrents.com/details/af04abfe9a3c96b30e5dd029eb185e19a7055272), 
Related paper, Icentia11K: An Unsupervised Representation Learning Dataset for Arrhythmia Subtype Discovery.

(2) [PTB-XL dataset](https://physionet.org/content/ptb-xl/1.0.3/),
Related paper, PTB-XL, a large publicly available electrocardiography dataset.

(3) [ICBEB 2018](http://2018.icbeb.org/Challenge.html), 
Related paper, An Open Access Database for Evaluating the Algorithms of Electrocardiogram Rhythm and Morphology Abnormality Detection

The code will be made available upon the manuscript is accepted.

If you use our code or referenced our paper, please acknowledge our work by citing the corresponding articles.


## Setup

### Environment
Install the dependencies (wfdb, pytorch, torchvision, cudatoolkit, fastai, fastprogress) by creating a conda environment:

Pytorch 1.11, Python 3.8


### Project overview
1. get_datasets.sh, the script for preparing dataset.

2. the 'code' directory contains all the experimental code files.
Change to 'code' directory, then,
configs/, contains configuration files for model;
experiments/, contains a file named scp_experiment.py, 
models/, contains model definitions,
utils/, contains tool functions,

3. data/, the root directory of all data,

4. output/, the root directory of all experimental outputs. 


### Get data
Download and prepare the datasets (PTB-XL and ICBEB) via the follwing bash-script:

    ./get_datasets.sh

This script first downloads [PTB-XL](https://physionet.org/content/ptb-xl/) and stores it in `data/ptbxl/`. 
Afterwards all training data from the [ICBEB 2018](http://2018.icbeb.org/Challenge.html) is downloaded and temporally stored in `tmp_data/`. 
After downloading and unzipping, `code/utils/convert_ICBEB.py` is called which stores the data in appropriate format in `data/ICBEB/`. 

For preparing the Icentia11K dataset, since this dataset has a storage of over 250 GB, we suggest you download the dataset firstly, and place the dataset outside the project, and access this dataset through soft link.
After downloading and unzipping, `code/utils/convert_Icentia11k.py` is called which stores the data in appropriate format in `data/icentia11k/`. 


## Reproduce results from the paper

Change to the root directory, and then call

    python -m code.reproduce_my_experiments


This will perform all experiments for all models used in the paper. 
Depending on the executing environment, this will take up to several hours. 
Once finished, all trained models, predictions and results are stored in `output/`, 
where for each experiment a sub-folder is created each with `data/`, `models/` and `results/` sub-sub-folders. 

### Download models and results

The models can be accessed on reasonable requests, we will also consider releasing our model later. 


## For customized experiments
For creating customized models for experiments, you can try as follows:

1. create your model `code/models/your_model.py` which implements a standard classifier interface with `fit(X_train, y_train, X_val, y_val)` and `predict(X)`
2. create a config file `code/configs/your_configs.py` with name, type and parameters (if needed)
3. add your modeltype and model import to the cases in `perform`-function of `code/experiments/scp_experiment.py` (already added for demonstration purpose!)
4. add your model-config to `models` and perform your experiment as below (adjusted code of `code/reproduce_results.py`):


# References
Please acknowledge our work by citing our journal paper

    @article{QinECGClassification2023,
    doi = {xx/xxx},
    url = {https://doi.org/xxx},
    year = {2023},
    volume={xx},
    number={x},
    pages={xx-xx},
    publisher = {xxxx},
    author = {Keke Qin, Wu Huang, Tao Zhanga, Hengyuan Zhanga, and Xiangrong Cheng},
    title = {A lightweight SelfONN model for general ECG classification with pretraining},
    journal = {xxxx}
    }
	
For the PTB-XL dataset, please cite

    @article{Wagner:2020PTBXL,
    doi = {10.1038/s41597-020-0495-6},
    url = {https://doi.org/10.1038/s41597-020-0495-6},
    year = {2020},
    publisher = {Springer Science and Business Media {LLC}},
    volume = {7},
    number = {1},
    pages = {154},
    author = {Patrick Wagner and Nils Strodthoff and Ralf-Dieter Bousseljot and Dieter Kreiseler and Fatima I. Lunze and Wojciech Samek and Tobias Schaeffter},
    title = {{PTB}-{XL},  a large publicly available electrocardiography dataset},
    journal = {Scientific Data}
    }

    
If you use the [ICBEB challenge 2018 dataset](http://2018.icbeb.org/Challenge.html) please acknowledge

    @article{liu2018:icbeb,
    doi = {10.1166/jmihi.2018.2442},
    year = {2018},
    month = sep,
    publisher = {American Scientific Publishers},
    volume = {8},
    number = {7},
    pages = {1368--1373},
    author = {Feifei Liu and Chengyu Liu and Lina Zhao and Xiangyu Zhang and Xiaoling Wu and Xiaoyan Xu and Yulin Liu and Caiyun Ma and Shoushui Wei and Zhiqiang He and Jianqing Li and Eddie Ng Yin Kwee},
    title = {{An Open Access Database for Evaluating the Algorithms of Electrocardiogram Rhythm and Morphology Abnormality Detection}},
    journal = {Journal of Medical Imaging and Health Informatics}
    }
