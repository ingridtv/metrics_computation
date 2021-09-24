# Stand-alone project for segmentation validation and metrics computation
Designed for brain tumor segmentation purposes.

# 1. Folder and data structures and naming conventions
Assuming in the following example that the data are stored based on their origin, but
anything should work. The folders named _index0_ and _index1_ could be renamed to
_Amsterdam_ and _StOlavs_ for instance.

## 1.1 Original data folder structure
The main data directory containing the original MRI images and corresponding
manual annotations is expected to resemble:
  > * /Path/to/data/root/  
  > --- index0/  
  > ------ AMS0/  
  > --------- volumes/  
  > ------------ AMS0_T1.nii.gz  
  > --------- segmentations/  
  > ------------ AMS0_T1_label_tumor.nii.gz  
  > ------ AMS25/  
  > ------ AMS50/  
  > --- index1/  
  > ------ STO25/  
  > ------ STO50/

## 1.2 Inference results folder structure
The inference results should be grouped inside what will become the validation folder,
resembling the following structure (here for Study1). The outer-most sub-folder
naming convention inside _predictions_ are the fold numbers.
  > * /Path/to/validation/Study1/  
  > --- predictions/  
  > ------ 0/  
  > --------- index0_AMS0/  
  > ------------ AMS0_T1-predictions.nii.gz  
  > --------- index1_STO25/  
  > ------------ STO25_T1-predictions.nii.gz  
  > ------ 1/  
  > --------- index0_AMS50/  
  > ------------ AMS50_T1-predictions.nii.gz  
  > --------- index1_STO50/  
  > ------------ STO50_T1-predictions.nii.gz

## 1.3 Folds file
The file with patients' distribution within each fold used for training should list
the content of the validation and test sets iteratively.  
The file should be called __cross\_validation\_folds.txt__ and placed in the validation
study folder side-by-side with the _predictions_ sub-folder.  
An example of its content is given below:
  > index0_AMS1000_T1_sample index1_STO250_T1_sample\n    
  > index0_AMS0_T1_sample index1_STO25_T1_sample\n  
  > index0_AMS0_T1_sample index1_STO25_T1_sample\n    
  > index0_AMS25_T1_sample index1_STO50_T1_sample\n  

# 2. Installation
After installing all Python dependencies as listed in the requirements.txt file,
do the following in a terminal.
  > cd /path/to/validation_metrics_computation  
  > cp blank_main_config.ini main_config.ini 

You can now edit your __main\_config.ini__ file for running the different processes.  
An additional explanation of all parameters specified in the configuration file can be
found in _/Utils/resources.py_. 

# 3. Process
To run, you need to supply the configuration file as parameter.
  > python main.py -c main_config.ini

After filling in the configuration file, you should run first the 
__validation__ task and then the __study__ task.  
N.B. If no study fits your need, you can create a new study file in _/Studies/_.