# Formula 1 Race Predictions

The FIA which governs Formula 1 racing has tasked me with creating a model that will make lap by lap predictions that might help sponsors decide which drivers to invest in, fans to have a better experience watching the race, and constructors to see how the competition is doing to make adjustments to their racing strategy in real-time. The data was taken from [Ergast Developer API](http://ergast.com/mrd/) and split into various JSON or CSV files from race results, to pit-stop times, to circuit information. Our modelling was done using LSTM + PyTorch and the evaluation metric used to see how well our model performed was RMSPE (root mean squared percentage error).

![formula1](https://github.com/gregoryhhan/formula1_capstone/blob/main/images/f1_banner.jpg)

## Business Understanding

Since the first Formula 1 race in the 1950s, there has been a constant development to develop the fastest cars and pair them with the most capable of drivers. Only the 20 best drivers can sit behind the wheel of a Formula 1 car and race in a number of races across the world to claim a championship. And, with many advancements in technology, Formula 1 has become a data-driven sport. There are countless sensors on the cars, data points generated from every race, and the usage of deep learning models to find the best strategies, forecasts, and decisions to win a race. There are about 750 million data points that are received during a 2-hour race which must be analyzed for something seemingly simple such as deciding which lap to change the tires when it starts to rain. Although, there are some unpredictable events that may occur such as engine failure, those events are rare and as such deep learning models are very efficient to make race predictions [Formula 1 and Machine Learning](https://becominghuman.ai/formula-1-and-machine-learning-62d1f7166c41).

## Data Understanding

There are many factors that can determine what happens during a race and who will eventually become the winner which are included in the dataset I used for my modelling. However, I selected a few that I thought had the biggest influence: laptimes during qualification, pit-stop times, statuses of the cars, and position on the grid when starting the race.

### Pit Stop Times

Pit stop times were available from 2012 onward. There is a disparity between 2012 to 2014 which might be due to the changes in pit stop regulations reducing the pit entry speed limit from 70mph to 40mph.

![pitstop](https://github.com/gregoryhhan/formula1_capstone/blob/main/images/pitstop_times.png)

### Fastest Lap Times

The fastest lap times remained largely unchanged but with the introduction of the faster V6 turbo hybrid engine in 2014, the seconds for a fastest lap time begin to decrease.

![fastestlap](https://github.com/gregoryhhan/formula1_capstone/blob/main/images/fastest_laptimes.png)

### Grid Position to Win

Usually the drivers who started in the top 5 positions at the start of the race ended up winning the race, but there were races in which the last place driver took first place; those races were attributed to changes of statuses amongst the cars and unpredictable events like weather.

![gridposition](https://github.com/gregoryhhan/formula1_capstone/blob/main/images/grid_positions.png)

### Statuses of Cars

The majority of cars finished the races with no problems but a significant number of cars ended up with statuses such as accident or car issues that would dictate whether they finished the race and what place they would come in.

![status](https://github.com/gregoryhhan/formula1_capstone/blob/main/images/statuses.png)

## Modelling and Evaluation

I used Google Colab for my modelling to utilize the GPU to run my model. The link to the notebooks can be found below. One thing to take note is that the data was mounted from my Google Drive which cannot be accessed by another user so, you can copy the necessary csv files from the data folder of this repository, add it to a new folder into your Google Drive, and replace my drive with yours when mounting it in the notebook.

For my modelling, I used LSTM (long short term memory) which is a recurrent neural network to use for times series data. It takes information from prior inputs to influence the current inputs and outputs. Similar to a human brain, LSTM would decide which memories would be siginificant to use to make current and future decisions. There are 3 states to LSTM : forget, input, and output. Forget state is when the model decides what parts of the timestamp data to forget or carry over, input state is when new information is added to the model, and the output state which passes the current information to the next timestamp data. Along with LSTM, I used PyTorch which is a frameowrk developed by Facebook as a library for processing tensors in deep learning. One advantage PyTorch has is that it uses a dynamic computational graph (creates scheme for modelling on the fly)  vs. static (creates entire scheme before data can be added).

The baseline model was made using the data from the last 20 years of Formula 1 (2001-2020). The evaluation metric used was RMSPE which is the percentage of error between the predicted values and actual values. The model did not perform well and overfit with an RMSPE of 447%. It might've been because the model did not know what to do for driver ids that numbered over 800+ vs. positions that were numbered from 1-20. 

I used some feature engineering to scale the data so that my model would be able to more accurately make predictions. I used one hot encoding for driver ids, scaled the lap times into integers based on seconds, and grouped statuses of the cars into 6 groups to make it easier to discern what status a car would be. My model performed pretty well as it returned an RMSPE of 25%. 

Here is a comparison of how my model performed predicting the race results of the 2020 Abu Dhabi races against the actual results. 
![raceresult](https://github.com/gregoryhhan/formula1_capstone/blob/main/images/abudhabi.png)

There are other considerations to make my model perform better such as track conditions, tire quality, and weather statuses in the future.

### App Creation

I also created a webapp through Streamlit which would visualize how my model did when making lap-by-lap predictions. The user would select model parameters such as season year, which number of the grand prix, and how many laps have gone by to see what positions the drivers were currently in.

You can view the app through: [Formula 1 Race Predictions](https://gregoryhhan.wixsite.com/my-site-1)

### Conclusion

My model can be expanded on using cloud computing to access and analyze the 1.1 million data points transmitted per second from cars/pits to make better predictions during a race. And, it can be used by constructors to develop faster cars, make better racing strategies, and for fans to have a better viewing experience during the race.

### Repository Structure

```
├── data                    <- datasets
  ├── races_npy             <- race data turned into numpy
├── images 
├── filesplit
├── races
├── .gitignore                                   
├── Main Notebook + EDA    
├── Baseline_Model
├── Final_Model
├── README.md
└── streamlit 
```
### Links to Google Colab Notebooks
[Final Notebook](https://colab.research.google.com/drive/12gNChHZ3J0Kv1srlolbN9bzCqiYnrOSU?usp=sharing)

[FileSplit](https://colab.research.google.com/drive/12nRRpCB650WTeWnnVagb8xd72jTJW3d0?usp=sharing) files split so that it can uploaded to Github
