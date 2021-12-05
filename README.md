# Bremen-Big-data-2019
This repository contains the code and dataset for the Bremen Big data challenge 2019.  
Link to the competition: https://bbdc.csl.uni-bremen.de/index.php/2019 

## Problem description

The Bremen Big Data Challenge 2019 is about classifying various everyday and sporting movements. For this purpose, sensor data recorded on one leg above and below the 
knee are available. The training dataset contains the data of 15 subjects, four more are used to evaluate your solutions.  
In the data there are the following 22 movements:

* Race (run).  
* Walking (walk).  
* Standing (stand).  
* Sitting (sit).  
* Get up and sit down (sit-to-stand, stand-to-sit).  
* Climbing and descending stairs (stair-up, stair-down).  
* Jumping on one or both legs (jump-one-leg, jump-two-leg).  
* Run left or right curve (curve-left-step, curve-right-step).  
* On the spot turn left or right, left or right foot first (curve-left-spin-Lfirst, curve-left-spin-Rfirst, curve-right-spin-Lfirst, curve-right-spin-Rfirst).  
* Sideways steps to the left or right (lateral-shuffle-left, lateral-shuffle-right).  
* Change of direction when running to the right or left, left or right foot first (v-cut-left-Lfirst, v-cut-left-Rfirst, v-cut-right-Lfirst, v-cut-right-Rfirst)  
  
In addition, there are other, possibly incorrectly labeled movements in the data. For the task of the BBDC 2019, only the 22 listed movements are relevant.   
All data is available as CSV files (comma separated values). The first three lines of training data (train.csv) look like this:  
![image](https://user-images.githubusercontent.com/68081679/144753590-8f1da8ef-1bda-4964-97e5-01bdde02f380.png)  
Each line corresponds to a recording of a movement. The columns have the following meanings:

* Subject: The Id of the subject  
* Datafile: Path of the file containing the sensor data for this recording. For each test person, there is a folder in which the sensor
data for individual motion recordings are lying in individual files.  
* Label: The Movement That Has Been Recorded  


The test data (challenge.csv) has the following format:  
![image](https://user-images.githubusercontent.com/68081679/144753706-2c4f081a-998c-41d6-8506-8e0201d0d109.png)  
The columns have the same meaning as in train.csv. The Label column constantly contains the letter Xto indicate that this value is not present.
If you submit solutions, then your submission should correspond exactly to the test data, with each X replaced by a label.
This label corresponds to your classification result for this movement. It is important that the spelling (including upper/lower case) of the 
textual labels exactly matches the spelling of the labels in the training data.  
For example, the data files.B look like this (example: Subject02_Aufnahme000.csv)
![image](https://user-images.githubusercontent.com/68081679/144753816-9b804d89-7551-4028-a6f9-71cc8a8020f5.png)  
Each line represents the sensor values measured at a time (sampled at 1000Hz). The columns represent the individual sensors whose position is illustrated by the graphic:  
![image](https://user-images.githubusercontent.com/68081679/144753853-0b6c5a08-babe-45cf-8466-aa7b2ee2f02e.png)  



