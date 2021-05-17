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
├── data  #train, and test data. 
|  └──  prediction  #storess prediction of labels after each phase
├── model
|  └──  configs.py  #storess address of current directory
|  └──  dataset.py  #handles loading dataset
|  └──  params.txt  #model hyperparameters
|  └──  gat.py  #defines a gat
|  └──  multi-phase-classification.py  # defines a gat
|  └──  semi-supervised-training-GAT.py  #Trains a gat for each phase
├── results  #detailed output of training and evaluating a model
├── saved_models_GAT  #pre-trained models and new trained models
|  └──  0 hidden, 1 attention head  # saved models with 0 hidden layer and 1 attention head
|  └──  0 hidden, 2 attention heads # saved models with 0 hidden layer and 2 attention heads
|  └──  0 hidden, 4 attention heads # saved models with 0 hidden layer and 4 attention heads
|  └──  1 hidden, 1 attention head  # saved models with 1 hidden layer and 1 attention head
|  └──  1 hidden, 2 attention heads # saved models with 1 hidden layer and 2 attention heads
|  └──  1 hidden, 4 attention heads # saved models with 1 hidden layer and 4 attention heads
|  └──  2 hidden, 1 attention head  # saved models with 2 hidden layers and 1 attention head
|  └──  2 hidden, 2 attention heads # saved models with 2 hidden layers and 2 attention heads
|  └──  2 hidden, 4 attention heads # saved models with 2 hidden layers and 4 attention heads
├── README.md
├── requirements.txt  #required Python library
├── ...
```
## Environment setup
The following instruction were tested on Python 3.7.6, 32GB RAM and macOS.
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

## Evaluating pre-trained model
Final results in the Report 6 (phase 1, 2) can be replicated with pre-trained models.
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
python multi-phase-classification.py
```
This experiment uses the default hyperparameters.
The short result will be displayed on the terminal and the detailed classification report will be saved in the `/results` folder. 
## Training a new model
Firstly, activate the virtual environment (if not activated):
```
source venv/bin/activate
```
### Train with default hyperparameters
For train a model with our default hyperparameters the following command can be used: 
```
cd $BASEPATH/model
python multi-phase-classification.py -c params.txt
```
The output of each training epoch will be displayed on the terminal and detailed results will be saved in the `/results` folder. 
Files related to models will be saved in `/saved_models_GAT/` folder.
### Train with customized hyperparameter
Create a new configuration file (for example, `new_params.txt`) in `/model/` folder. Hyperparameter details are in `/model/params.txt` and `/model/multi-phase-classification.py`.
Run:
```
cd $BASEPATH/model
python multi-phase-classification.py -c new_params.txt
```

The output of each training epoch will be displayed on the terminal and detailed results will be saved in the `/results` folder. 
Files related to models will be saved in `/saved_models_GAT/` folder.

## Evaluating a new model
Firstly, activate the virtual environment (if not activated):
```
source venv/bin/activate
```
To evaluate new models, just put them in the  `/saved_models_GAT/` folder (If they are not there already). Then, in the corresponding configuration file (for example, `new_params.txt`) in `/model/` folder, change the mode from 'train' to 'eval' and run the following command:

```
cd $BASEPATH/model
python multi-phase-classification.py -c new_params.txt
```
The short result will be displayed on the terminal and the detailed classification report will be saved in the `/results` folder. 
