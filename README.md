# mazeABCD

This includes the introduction to ABCD task preprocessing step by step, during and after you've done the experiment. 

DURING EXPERIMENT 
----------------------------------

During experiment, you might need to calculate the transition rate of each day / session before deciding whether to switch on to the next task for the animal. If transition rate is** >0.70** (i.e. animal taking shortest path between two goals for more than 70% of the times), you should switch it on to the next task. 

I. running sleap  
please see the repo by Peter for a detailed instruction of SLEAP


II. transition rate analysis







AFTER EXPERIMENT 
-----------------------------------
I. organise your data on ceph in the right place. 


II. double check metadata
- make sure to mark the sessions to include as 1 in the include column.
- sessions to exclude: e.g. animal dropping out of maze; abnormal behaviour; etc.
- mark the sessions to manually correct, which would include
      - sessions that are restarted (pycontrol and ephys restarted) without restarting the camera recording (i.e. one tracking id with two behaivour ids), which requires manual splitting of the .h5 file and .csv file for ROIs after sleap processing 
      - sessions where pycontrol task was started before ephys/camera (which require manual alignment of sync pulses
  

III.
