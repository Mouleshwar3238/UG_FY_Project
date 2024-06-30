# UG_FY_Project
Designed Vanilla RNN, LSTM and GRU models to predict the state of charge of a lithium-ion battery used in an EV

## Dataset Description
The dataset contains data for driving trips that have been made using a BMW i3 electric vehicle, and has been originally sourced from IEEE Dataport.
* Title: BATTERY AND HEATING DATA IN REAL DRIVING CYCLES
* URL: https://www.kaggle.com/datasets/atechnohazard/battery-and-heating-data-in-real-driving-cycles
* Dataset description:
  | Number of trips | 70  |
  | --------------- | --- |
  | Number of categories | 2 |
  | Number of trips in category A (summer) | 32 |
  | Number of trips in category B (winter) | 38 |
  | Total number of samples                |  10,94,793 |
  | Number of samples in category A        |  4,67,701  |
  | Number of samples in category B        |  6,27,092  |

The performance metrics used to analyse the performance of the models were Mean Squared Error (MSE) and R-squared (R2) score.



The activation functions used are as follows:
* Tanh or hyperbolic tangent function for the hidden layer(s)
* Linear function for the output layer
