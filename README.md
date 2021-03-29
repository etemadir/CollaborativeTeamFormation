# Finding Collaborative Experts in Community Question Answering

This repository provides a standard training and testing framework for Finding Collaborative Experts in Community Question Answering.

## Usage

#### Installation

- Clone this repo. or download and unzip the code
- Enter OpenAttHetRL directory, and run the following code
    ```
    pip install .
    or
    pip install CollaborativeTF
    ```


#### Examples
##### e.g. 1 data preprocessing
 ```python
# import the class
from  CollaborativeTF.preprocessing import  datapreprocessing 
# run preprocessing by passing the location and dataset
datapreprocessing.createdata("./data/","android") 
 ```
The datasets are publicly available at https://archive.org/details/stackexchange. For each dataset, three files as  Posts.xml, Tags.xml, and Users.xml are required for the data preprocessing phase. 

 ##### e.g. 2 generate train and test data 
```python 
#import CollaborativeTF class to run the framework
from  CollaborativeTF.framework import  CollaborativeTF
#generate train and test data  
CollaborativeTF.prepare_train_test("data/android")
```
 ##### e.g. 3 model training
 ```python
# import CollaborativeTF class to run the framework
from  CollaborativeTF.framework import  CollaborativeTF
#perform  function run_train to train the model 
#   parameters: 
#  "data/android": dataset name and location,
#  dim_node=32,dim_word=300  node and word embedding dimentions ,
#  epochs=10,batch_size=16   the number of epochs and batch size
#  returns: trainded model is stored in ./data/android/parsed/model/
model=CollaborativeTF.run_train("data/android",dim_node=32,dim_word=32
                         ,epochs=1,batch_size=16)
# save node and word embedding vectors
model.saveembedings()
#save the model
CollaborativeTF.saveModel("data/android/parsed/model/","model",model)
#load the model
loadedModle=CollaborativeTF.loadModel("data/android/parsed/model/","model")
 ```
 
 ##### e.g. 4 perform expert finding 
 ```python
# import CollaborativeTF class to run the framework
from  CollaborativeTF.framework import  CollaborativeTF
#load the model
loadedModle=CollaborativeTF.loadModel("data/android/parsed/model/","model")
#find topk related experts for a given question
q={"title":"How Can I fix GPS in my Samsung Galaxy S?","tags":["gps","samsung-galaxy-s"],"askerID":1089}
top10=CollaborativeTF.findTopKexperts(question=q,model=loadedModle,topk=10)
print(top10)
print("done!")
 ```

