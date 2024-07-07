# Lithium-Ion Battery SoC Prediction Using Deep Learning
Designed Vanilla RNN, LSTM and GRU models to predict the state of charge of a lithium-ion battery used in an EV.

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
The GRU and Dense layers of the Sequential module of the Keras library in Python were used to implement the gated recurrent unit network. The activation functions, loss function, optimizer, learning rate and the performance metrics used are similar to the Vanilla RNN implementation, with the optimal configuration for the GRU model also being determined in a similar fashion.

## Model Testing/Validation
The performance of the three optimal models was compared using the test datasets, as well as the remaining datasets that were not used for either training, validation or testing.
* Results for the Test Datasets
<table>
<thead>
  <tr>
    <th align="center">Model</th>
    <th align="center">Number of Parameters</th>
    <th align="center">Overall Average MSE (in %)</th>
    <th align="center">Overall Average R2 Score (in %)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td align="center">Vanilla RNN</td>
    <td align="center">67,075</td>
    <td align="center">0.0587</td>
    <td align="center">99.9971</td>
  </tr>
  <tr>
    <td align="center">LSTM</td>
    <td align="center">2,67,523</td>
    <td align="center">0.0524</td>
    <td align="center">99.9958</td>
  </tr>
  <tr>
    <td align="center">GRU</td>
    <td align="center">2,01,475</td>
    <td align="center">0.0136</td>
    <td align="center">99.9992</td>
  </tr>
</tbody>
</table>

* Results for the Miscellaneous Test Datasets
<table>
<thead>
  <tr>
    <th align="center">Model</th>
    <th align="center">Number of Parameters</th>
    <th align="center">Overall Average MSE (in %)</th>
    <th align="center">Overall Average R2 Score (in %)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td align="center">Vanilla RNN</td>
    <td align="center">67,075</td>
    <td align="center">0.1622</td>
    <td align="center">99.9966</td>
  </tr>
  <tr>
    <td align="center">LSTM</td>
    <td align="center">2,67,523</td>
    <td align="center">0.1707</td>
    <td align="center">99.9961</td>
  </tr>
  <tr>
    <td align="center">GRU</td>
    <td align="center">2,01,475</td>
    <td align="center">0.0418</td>
    <td align="center">99.9991</td>
  </tr>
</tbody>
</table>

## Supplementary Results
In addition to the above RNN models, SoC prediction was carried out using some popular ML algorithms.
<table>
<thead>
  <tr>
    <th align="center">Algorithm</th>
    <th align="center">Training R2 Score <br> (in %)</th>
    <th align="center">Validation R2 Score  <br> (in %)</th>
    <th align="center">Test R2 Score <br> (in %)</th>
    <th align="center">Miscellaneous Test R2 Score <br> (in %)</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td align="center">Linear Regression</td>
    <td align="center">82.9611</td>
    <td align="center">82.8506</td>
    <td align="center">93.5213</td>
    <td align="center">81.5465</td>
  </tr>
  <tr>
    <td align="center">Lasso Regression</td>
    <td align="center">82.9510</td>
    <td align="center">82.8430</td>
    <td align="center">93.3572</td>
    <td align="center">81.3621</td>
  </tr>
  <tr>
    <td align="center">Ridge Regression</td>
    <td align="center">82.9575</td>
    <td align="center">82.8485</td>
    <td align="center">93.4173</td>
    <td align="center">81.4368</td>
  </tr>
  <tr>
    <td align="center">Linear SVR</td>
    <td align="center">81.9056</td>
    <td align="center">81.8045</td>
    <td align="center">94.5503</td>
    <td align="center">81.9790</td>
  </tr>
  <tr>
    <td align="center">Decision Tree Regressor</td>
    <td align="center">99.9899</td>
    <td align="center">96.5195</td>
    <td align="center">85.4748</td>
    <td align="center">71.3823</td>
  </tr>
  <tr>
    <td align="center">AdaBoost Regressor</td>
    <td align="center">74.1895</td>
    <td align="center">74.2081</td>
    <td align="center">77.1237</td>
    <td align="center">62.9671</td>
  </tr>
  <tr>
    <td align="center">MLP Regressor</td>
    <td align="center">92.8503</td>
    <td align="center">92.8617</td>
    <td align="center">94.7645</td>
    <td align="center">81.1827</td>
  </tr>
  <tr>
    <td align="center">KNN Regressor</td>
    <td align="center">98.7171</td>
    <td align="center">98.0798</td>
    <td align="center">84.5740</td>
    <td align="center">72.0371</td>
  </tr>
  <tr>
    <td align="center">XGBoost Regressor</td>
    <td align="center">96.8006</td>
    <td align="center">96.7200</td>
    <td align="center">90.1492</td>
    <td align="center">77.4607</td>
  </tr>
  <tr>
    <td align="center">Random Forest Regressor</td>
    <td align="center">99.7114</td>
    <td align="center">97.9454</td>
    <td align="center">89.2077</td>
    <td align="center">75.8618</td>
  </tr>
  <tr>
    <td align="center">Gradient Boosting Regressor</td>
    <td align="center">93.5534</td>
    <td align="center">93.4392</td>
    <td align="center">93.2566</td>
    <td align="center">79.7241</td>
  </tr>
</tbody>
</table>

For the KNN Regressor, the best value of K was found by plotting the elbow curve for R2 scores versus different values of K.

## Conclusion 
The GRU model achieved the least MSE and highest R2 score than that of the other models and hence, it proved to be quite capable of accurately estimating the SoC of a battery operating under different conditions.

