# mazeABCD

This includes the introduction to ABCD task preprocessing step by step, during and after you've done the experiment. 

THINGS THAT COULD BE USEFUL THROUGHOUT 
----------------------------------

**Setting up VSCode and SSH to Ceph** 
all of the files are stored on Ceph, within the folder `/ceph/behrens/<yourname>`, with a more detailed folder structure below (you'll see it if you scroll to folder structure). 





DURING EXPERIMENT 
----------------------------------

During experiment, you might need to calculate the transition rate of each day / session before deciding whether to switch on to the next task for the animal. If transition rate is** >0.70** (i.e. animal taking shortest path between two goals for more than 70% of the times), you should switch it on to the next task. 

STEP1: running sleap  
    - please see the repo by Peter for a detailed instruction of SLEAP


STEP2: maze registration and transition rate analysis
    - please see the repo mazeABCD_registration 




AFTER EXPERIMENT 
-----------------------------------

**STEP1: Organise your ceph folder accordingly, with the following folder structure:**


## Folder Structure 
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

### raw_data
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

### preprocessed_data
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

### processed_data
```
├── processed_data/
    │   ├── neuron_raw/
    │   ├── behaviour_raw/
    │   ├── trialtimes_raw/
    │   ├── task_raw/
    │   ├── LED_raw/  ## if optogenetics
    │   └── poketime_raw/
```

**STEP2. double check metadata and upload to the `/raw_data/metadata/` folder** 
- make sure to mark the sessions to include as 1 in the include column.
- sessions to exclude: e.g. animal dropping out of maze; abnormal behaviour; etc.
- mark the sessions to manually correct, which would include
      - sessions that are restarted (pycontrol and ephys restarted) without restarting the camera recording (i.e. one tracking id with two behaivour ids), which requires manual splitting of the .h5 file and .csv file for ROIs after sleap processing 
      - sessions where pycontrol task was started before ephys/camera (which require manual alignment of sync pulses

**STEP3: running sleap**  
    - please see the repo by Peter for a detailed instruction of SLEAP

**STEP4: maze registration and transition rate analysis**
    - please see the repo mazeABCD_registration 

**STEP5: run the behavioural preprocessing pipeline** 
    - please see the mazeABCD_preprocessing repo

(OPTIONAL, only if doing ephys recording)
**STEP6: run the ephys preprocessing pipeline** 
    - please see the mazeABCD_spikesorting repo 




