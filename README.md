# Formula 1 Race Predictions

The FIA which governs Formula 1 racing has tasked me with creating a model that will make lap by lap predictions that might help sponsors decide which drivers to invest in, fans to have a better experience watching the race, and constructors to see how the competition is doing to make adjustments to their racing strategy in real-time. The data was taken from [Ergast Developer API](http://ergast.com/mrd/) and split into various JSON or CSV files from race results, to pit-stop times, to circuit information. Our modelling was done using LSTM + PyTorch and the evaluation metric used to see how well our model performed was RMSPE (root mean squared percentage error).

![formula1](https://github.com/gregoryhhan/formula1_capstone/blob/main/images/f1_banner.jpg)

## Business Understanding

Since the first Formula 1 race in the 1950s, there has been a constant development to develop the fastest cars and pair them with the most capable of drivers. Only the 20 best drivers can sit behind the wheel of a Formula 1 car and race in a number of races across the world to claim a championship. And, with many advancements in technology, Formula 1 has become a data-driven sport. There are countless sensors on the cars, data points generated from every race, and the usage of deep learning models to find the best strategies, forecasts, and decisions to win a race. There are about 750 million data points that are received during a 2-hour race which must be analyzed for something seemingly simple such as deciding which lap to change the tires when it starts to rain. Although, there are some unpredictable events that may occur such as engine failure, those events are rare and as such deep learning models are very efficient to make race predictions [Formula 1 and Machine Learning](https://becominghuman.ai/formula-1-and-machine-learning-62d1f7166c41).

### Data Understanding

There are many factors that can determine what happens during a race and who will eventually become the winner which are included in the dataset I used for my modelling. However, I selected a few that I thought had the biggest influence: laptimes during qualification, pit-stop times, statuses of the cars, and position on the grid when starting the race.

### Modelling and Evaluation

Based on our analysis of the data, we would recommend honing in on these 4 factors:
<ul>
  <li>Doctor recommendation of vaccines</li>
  <li>Opinion of vaccine effectiveness</li>
  <li>Opinion of flu risk</li>
  <li>Health insurance</li>
</ul>


### App Creation

### Conclusion

We used these 4 quesitons below as a guide to completing this analysis:
<ul>
  <li>Which model is the most effective in predicting whether a person received a seasonal flu shot?</li>
  <li>Which model is the most effective in predicting whether a person received a H1N1 flu shot?</li>
  <li>Which features are the most important in predicting whether a person received a seasonal flu shot?</li>
  <li>Which features are the most important in predicting whether a person received a H1N1 flu shot?</li>
</ul>

### Repository Structure

```
├── data          <- Both sourced externally and generated from code 
├── images 
├── races
├── races_npy 
├── .gitignore                    <- gitignore 
├── README.md                  <- Narrative documentation of analysis in Jupyter notebook
├── Main Notebook + EDA
├── Baseline_Model
├── Feature_Engineered_Model
├── Final_Model
├── README.md<- The top-level README for reviewers of this project
└── streamlit           <- PDF version of project presentation
