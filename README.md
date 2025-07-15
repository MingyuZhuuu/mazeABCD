# mazeABCD

This includes the introduction to ABCD task preprocessing step by step, during and after you've done the experiment. 

THINGS THAT COULD BE USEFUL THROUGHOUT 
----------------------------------

**Setting up VSCode and SSH to Ceph** 

all of the files are stored on Ceph, within the folder `/ceph/behrens/<yourname>`, with a more detailed folder structure below (you'll see it if you scroll to folder structure). 


**setting up a conda environment on ceph** 

For the preprocessing of different data, you might need different packages, it'd be nice to have different conda environments, the repo for different preprocessing pipelines would guide you through this, but generally they follow: 
```
conda create --name <env_name> python==3.12.7
conda activate <env_name>
```

and then direct to your `/ceph/behrens/<yourname>/project/code` folder in terminal and run the following line to set up the environment. 

```
pip install -r <your_subfolder>/requirements.txt
```

**requesting a gpu/cpu node** 

```bash
    srun --nodes=1 --ntasks-per-node=1 --cpus-per-task=8 -p gpu --gres=gpu:1 --time=12:00:00 --mem=64G --pty bash -i
    # wait for resource to be allocated -- can take a while 
```

kernel for jupyter notebook 

after you've got a node, direct to your `/ceph/behrens/<yourname>/project/code` folder 
run: 

```bash
    source /etc/profile.d/modules.sh
    ## if using gpu:
    # module load cuda
    module load miniconda
    conda activate <conda_env_of_choice>     #sometimes requires  'source activate <conda_env_of_choice>'
    jupyter-notebook --no-browser --ip=0.0.0.0 --port 8888
```

then 



DURING EXPERIMENT 
----------------------------------

During experiment, you might need to calculate the transition rate of each day / session before deciding whether to switch on to the next task for the animal. If transition rate is** >0.70** (i.e. animal taking shortest path between two goals for more than 70% of the times), you should switch it on to the next task. 

STEP1: running sleap  
    - please see the repo by Peter for a detailed instruction of SLEAP


STEP2: maze registration and transition rate analysis
    - please see the repo mazeABCD_registration 




AFTER EXPERIMENT 
-----------------------------------

## STEP1: Organise your ceph folder accordingly, with the following folder structure:**


### Folder Structure** 
```
├── code/                                  # contains all the repos that'll be useful, and your own codes 
│   ├── ABCD_preprocessing/    
│   ├── ABCD_preprocessing_ephys/
│   ├── mazeSLEAP/
│   └── your_own_code/
├── data/ 
│   ├──raw_data/
│   ├──preprocessed_data/
│   ├──processed_data/
│   ├──analysis_data/

```

**raw_data**
```
├── data/ 
│    ├── raw_data/
│          ├── ephys/
│                ├── subject1
│                       ├── date_session
│                       ├── ...
│                ├── subject2
│                ├── ....                                      
│          ├── behaviour/
│                ├── subjectID-date-session.txt (pycontrol files)
│                ├── subjectID-date_session.mp4 (video files)
│                ├── subjectID_pinstate_date-session.csv (pinstate files) 
│          ├── metadata/
│                ├── subjectID_MetaData.csv
│                ├── ....
```

**preprocessed_data**
```
├── preprocessed_data/
│    ├── SLEAP/
│    ├── SLEAP_ROIs/
│    ├── maze_params/
│    ├── concat_ephys/
│          ├── subjectID
│                 ├── date
│                 ├── ...
│    ├── spikesorting_concat/
│          ├── subjectID
│                 ├── date
│                 ├── ... 
│    └── spikesorting_concat_done/
│          ├── subjectID
│                 ├── date
│                 ├── ... 
```

**processed_data**
```
├── processed_data/
    │   ├── neuron_raw/
    │   ├── behaviour_raw/
    │   ├── trialtimes_raw/
    │   ├── task_raw/
    │   ├── LED_raw/  ## if optogenetics
    │   └── poketime_raw/
```



## STEP2. double check metadata and upload to the `/raw_data/metadata/` folder
- make sure to mark the sessions to include as 1 in the include column.
- sessions to exclude: e.g. animal dropping out of maze; abnormal behaviour; etc.
- mark the sessions to manually correct, which would include
      - sessions that are restarted (pycontrol and ephys restarted) without restarting the camera recording (i.e. one tracking id with two behaivour ids), which requires manual splitting of the .h5 file and .csv file for ROIs after sleap processing 
      - sessions where pycontrol task was started before ephys/camera (which require manual alignment of sync pulses



## STEP3: running sleap**  
    - please see the repo by Peter for a detailed instruction of SLEAP




## STEP4: maze registration and transition rate analysis**
    - please see the repo mazeABCD_registration 




## STEP5: run the behavioural preprocessing pipeline** 
    - please see the mazeABCD_preprocessing repo




**(OPTIONAL, only if doing ephys recording)**
## STEP6: run the ephys preprocessing pipeline** 
    - please see the mazeABCD_spikesorting repo 




