# UG_FY_Project - Lithium-Ion Battery SoC Prediction Using Deep Learning
Designed Vanilla RNN, LSTM and GRU models to predict the state of charge of a lithium-ion battery used in an EV

## Dataset Description
The dataset contains data for driving trips that have been made using a BMW i3 EV. It has been originally sourced from IEEE Dataport, but published in Kaggle.
* Title: BATTERY AND HEATING DATA IN REAL DRIVING CYCLES
* URL: https://www.kaggle.com/datasets/atechnohazard/battery-and-heating-data-in-real-driving-cycles
<table>
<thead>
  <tr>
    <th align="center" colspan="2">Generic Description of Dataset</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td align="center">Number of trips</td>
    <td align="center">70</td>
  </tr>
  <tr>
    <td align="center">Number of categories</td>
    <td align="center">2</td>
  </tr>
  <tr>
    <td align="center">Number of trips in category A (summer)</td>
    <td align="center">32</td>
  </tr>
  <tr>
    <td align="center">Number of trips in category B (winter)</td>
    <td align="center">38</td>
  </tr>
  <tr>
    <td align="center">Total number of samples</td>
    <td align="center">10,94,793</td>
  </tr>
  <tr>
    <td align="center">Number of samples in category A</td>
    <td align="center">4,67,701</td>
  </tr>
  <tr>
    <td align="center">Number of samples in category B</td>
    <td align="center">6,27,092</td>
  </tr>
</tbody>
</table>

### Training and Test Datasets
The training dataset has combined data from both categories, sorted in decreasing order of battery SoC.
<table>
  <thead>
    <tr>
      <th align="center" colspan="2">Generic Description of Training Dataset</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">Number of trips</td>
      <td align="center">35</td>
    </tr>
    <tr>
      <td align="center">Number of trips in category A (summer)</td>
      <td align="center">16</td>
    </tr>
    <tr>
      <td align="center">Number of trips in category B (winter)</td>
      <td align="center">19</td>
    </tr>
    <tr>
      <td align="center">Total number of samples</td>
      <td align="center">5,38,214</td>
    </tr>
    <tr>
      <td align="center">Number of samples in training subset</td>
      <td align="center">4,30,572 (80%)</td>
    </tr>
    <tr>
      <td align="center">Number of samples in validation subset</td>
      <td align="center">1,07,642 (20%)</td>
    </tr>
    <tr>
      <td align="center">Input features</td>
      <td align="center">3 (Battery Voltage, Battery Current,<br>Battery Temperature)</td>
    </tr>
    <tr>
      <td align="center">Target variable</td>
      <td align="center">Battery SoC</td>
    </tr>
  </tbody>
</table>

On the other hand, the test dataset contains data for 12 unseen trips, 6 each from category A and B. To normalize the training, validation and test datasets, min-max normalization has been used, with a scaling range of [-1,1].

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


