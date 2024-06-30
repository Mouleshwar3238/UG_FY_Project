# UG_FY_Project
Designed Vanilla RNN, LSTM and GRU models to predict the state of charge of a lithium-ion battery used in an EV

## Dataset Description
The dataset contains data for driving trips that have been made using a BMW i3 electric vehicle, and has been originally sourced from IEEE Dataport.
* Title: BATTERY AND HEATING DATA IN REAL DRIVING CYCLES
* URL: https://www.kaggle.com/datasets/atechnohazard/battery-and-heating-data-in-real-driving-cycles
* Dataset description:
  | Number of trips | 70  |
  | :---------------: | :---: |
  | Number of categories | 2 |
  | Number of trips in category A (summer) | 32 |
  | Number of trips in category B (winter) | 38 |
  | Total number of samples | 10,94,793 |
  | Number of samples in category A | 4,67,701 |
  | Number of samples in category B | 6,27,092 |

### Training and Test Datasets
The training dataset has combined data from both categories, sorted in decreasing order of battery SoC.
  | Number of trips | 35  |
  | :---------------: | :---: |
  | Number of trips in category A (summer) | 16 |
  | Number of trips in category B (winter) | 19 |
  | Total number of samples | 5,38,214 |
  | Number of samples in training subset | 4,30,572 (80%) |
  | Number of samples in validation subset | 1,07,642 (20%) |
  | Input features | 3 (Battery Voltage, Battery Current,<br>Battery Temperature) |
  | Target variable | Battery SoC |

On the other hand, the test dataset contains data for 12 unseen trips, 6 each from category A and B. <br>
To normalize the training, validation and test datasets, min-max normalization has been used.

## Vanilla RNN
The SimpleRNN and Dense layers of the Sequential module of the Keras library in Python were used to implement the Vanilla RNN.
* The activation functions used are as follows:
  * **Tanh or hyperbolic tangent** function for the **hidden layer(s)**
  * **Linear function** for the **output layer**
* **Mean squared error (MSE)** was used as the loss function as well as a performance metric
* Along with MSE, **R-squared (R2)** score was used as a performance metric
* **Stochastic gradient descent (SGD)** with **0.025** as the learning rate, was used as the optimizer

The optimal configuration for the Vanilla RNN model was determined using a trial and error approach, in which different configurations were trained for 100 epochs with 512 samples per batch, and their performance metrics were analysed. The configuration with the least possible MSE as well as highest possible R2 score was chosen as the optimal one.

## LSTM
The LSTM and Dense layers of the Sequential module of the Keras library in Python were used to implement the long short-term memory network. The activation functions, loss function, optimizer, learning rate and the performance metrics used are similar to the Vanilla RNN implementation, with the optimal configuration for the LSTM model also being determined in a similar fashion.

## GRU
The GRU and Dense layers of the Sequential module of the Keras library in Python were used to implement the gated recurrent unit network. The activation functions, loss function, optimizer, learning rate and the performance metrics used are similar to the Vanilla RNN implementation, with the optimal configuration for the LSTM model also being determined in a similar fashion.


