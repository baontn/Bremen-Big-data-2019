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

## Approach
### Overall approach
I will make 3 predictions using 3 models, and then take the prediction results and vote to determine the best prediction.   

## Detail plan 
### Load the data  
The data will be loaded from this github repository:  
![image](https://user-images.githubusercontent.com/68081679/144754967-ef741b53-20c6-4816-8e17-572d603a2a78.png)  
After that, I will create an array of zeros, and then append the value of the subject's sensor data to that array. Finally, the array will be added to a list for later transformation. The size of the array was 4000 for file GRU_1 and GRU_2, and that of file GRU_3 was 3000. The reason for this size will be discussed in the next part.  
![image](https://user-images.githubusercontent.com/68081679/144755261-60747880-9271-4767-b512-30be011f7c03.png)  
This function will return the train dataset and the scaler. The scaler will be used later for the test dataset. The following function will return the train dataset and the scaler:  
![image](https://user-images.githubusercontent.com/68081679/144755520-d1fb1d40-b0ed-41a7-a107-65740ddab189.png)  
Data from subjects '02','03','04','05','06','07','08','09',11,12,13,16 were used to create the training data. Data from subject 17,18,19 were used to make the testing data.  
The function used to create testing dataset is similar to the one used to create training data.  
![image](https://user-images.githubusercontent.com/68081679/144755870-31bc0e2c-5592-4089-adc2-3f76786f7fc0.png)  
The process to create the predict dataset was also similar.  
Since there were some 'fake' labels that the organizer added into the dataset, we have to exclude it from our consideration. I replaced the values of the sensor reading by ones:  
![image](https://user-images.githubusercontent.com/68081679/144756076-bd163b74-88e1-4882-a22b-4afed4e31c9b.png)  

from the file train.csv, I obtained the y values and then one-hot encoded them. Below is the distribute of y values in the train dataset:  
![image](https://user-images.githubusercontent.com/68081679/144758227-3cedf971-ec79-4a30-9527-d9fea9f9ee0d.png)

### Data Exploration: 

First, it can be observed from the folder that the size for each file is not constain. I tried to see the distribution of the file size.  
The function below created a list of file size from all test subjects.  
![image](https://user-images.githubusercontent.com/68081679/144754879-d20f5382-1d44-465e-9ca0-210d9216cec7.png)
Result:  
![image](https://user-images.githubusercontent.com/68081679/144757627-4805cd92-47ce-4c80-93b3-ed0ef126d289.png)  
It can be seen that most of the data has the size under 4000. SO I chose 4000 as the default size for the data. If the actual data was shorter than 4000, the empty values would be filled with 0.   
After that, I tried to see the distribution of the value of the sensors (in this case value from subject number 14):  
![image](https://user-images.githubusercontent.com/68081679/144757869-ffd007a6-9ff7-4568-9969-23c58e3085d2.png)  
It is safe to conclude that the values of the sensor reading were normally distributed. For that reason, I used the StandardScaler from Sklearn to scale the data. 









