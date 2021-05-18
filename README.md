# Graph attention-based solution

## Outline
- Structure of the repository
- Environment setup
- Evaluating pre-trained model
- Training a model 
- Evaluating a model

## Structure of the repository
At the root folder of the project, you will see:

```text
├── data  #training, and testing data. 
|  └──  prediction  #stores prediction of labels after each phase
├── model
|  └──  configs.py  #stores address of current directory
|  └──  dataset.py  #handles loading dataset
|  └──  params.txt  #model hyperparameters
|  └──  customized-params.txt  #customized model hyperparameters
|  └──  gat.py  #defines a gat
|  └──  multi_phase_classification.py  #handles different phases of training
|  └──  train-GAT.py  #trains a gat for each phase
├── results  #classification report
├── saved_models_GAT  #saved models and new trained models
|  └──  0 hidden layer - 1 attention head  # saved models with 0 hidden layer and 1 attention head
|  └──  0 hidden layer - 2 attention heads # saved models with 0 hidden layer and 2 attention heads
|  └──  0 hidden layer - 4 attention heads # saved models with 0 hidden layer and 4 attention heads
|  └──  1 hidden layer - 1 attention head  # saved models with 1 hidden layer and 1 attention head
|  └──  1 hidden layer - 2 attention heads - multi-phase # saved models with 1 hidden layer and 2 attention heads for both of the two phases
|  └──  1 hidden layer - 4 attention heads # saved models with 1 hidden layer and 4 attention heads
|  └──  2 hidden layers - 1 attention head  # saved models with 2 hidden layers and 1 attention head
|  └──  2 hidden layers - 2 attention heads # saved models with 2 hidden layers and 2 attention heads
|  └──  2 hidden layers - 4 attention heads # saved models with 2 hidden layers and 4 attention heads
├── README.md
├── requirements.txt  #required Python library
├── ...
```
## Environment setup
The following instruction were tested on Python 3.7.6, 32GB RAM, processor of 2.3 GHz Intel Core i7 and macOS.
We recommend using a python virtual environment:
```
mkdir venv
virtualenv --python=python3 venv

#fill in $BASEPATH with the repository address
export BASEPATH=[path to the repo]
source venv/bin/activate
```
After activating the virtual environment, install required library packages:
```
cd $BASEPATH
pip3 install -r requirements.txt
```
Environment setup is done. Next time just simply run the following code to activate the virtural environment:
```
source venv/bin/activate
```

## Evaluating the pre-trained models
Final results in the Report 6 (Table 2,5) can be replicated with the pre-trained models.
Firstly, activate the virtual environment (if not activated):
```
source venv/bin/activate
```
Fill in and set paths:
```
export BASEPATH=[path to the repo]
```
Run evaluation experiment:
```
cd $BASEPATH/model
python multi_phase_classification.py
```
This experiment uses the default hyperparameters. The important hyperparameters are mentioned in section "3.5.2 Model implementation" of the report 6. A detailed explanation of them are available at `/model/multi_phase_classification.py` and `/model/params.txt`
The f-scores will be displayed on the terminal and the detailed classification report will be saved in the `/results` folder. 
It takes less than 15 minutes on the reported system to get results of each phase.
## Training a new model
Firstly, activate the virtual environment (if not activated):
```
source venv/bin/activate
```
### Train with the default hyperparameters
For train a model with our default hyperparameters the following command can be used: 
```
cd $BASEPATH/model
python multi_phase_classification.py -c params.txt
```
The f-score of each training epoch will be displayed on the terminal and final classifcation report will be saved in the `/results` folder. 
Models will be saved in `/saved_models_GAT/` folder.
It takes about 10 hours on the reported system to train each phase.
### Train with customized hyperparameters
Change the default hyperparameters of the `/model/new_params.txt` according to your wish. 
Run:
```
cd $BASEPATH/model
python multi_phase_classification.py -c new_params.txt
```

The f-score of each training epoch will be displayed on the terminal and final classification report will be saved in the `/results` folder. 
Models will be saved in `/saved_models_GAT/` folder.
The running time depends on the utilizing the hyperparameters.
## Evaluating a new model
Firstly, activate the virtual environment (if not activated):
```
source venv/bin/activate
```
To evaluate new models, just put them in the  `/saved_models_GAT/` folder (If they are not there already). Then, in the corresponding configuration file (`new_params.txt`) in `/model/` folder, change the mode from 'train' to 'eval' and run the following command:

```
cd $BASEPATH/model
python multi_phase_classification.py -c new_params.txt
```
The f-scores will be displayed on the terminal and the detailed classification report will be saved in the `/results` folder. 
It takes less than 20 minutes on the reported system to get results of each phase.
