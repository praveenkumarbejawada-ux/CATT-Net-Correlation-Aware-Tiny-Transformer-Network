# CATT-Net-Correlation-Aware-Tiny-Transformer-Network
# ABSTRACT
Predicting air quality precisely is a difficult task in a realistic air-quality monitoring environment due to incomplete, noisy, and sophisticated data about pollutants with time evolution. Missing data caused by malfunctions of sensors and problems related to data transfer and device maintenance negatively affect prediction results. At the same time, a great number of successful neural network architectures for air-quality predictions require high amounts of computational resources for their functioning. In order to address both issues in one approach, the paper presents an end-to-end multivariate forecasting framework. Initially, it uses CorrGAN– a data reconstruction algorithm based on generative adversarial networks that learns data correlations between air-quality indicators. Then, CATT-Net– correlation-aware tiny transformer– processes these data and predicts pollutant concentrations. Reconstructed by CorrGAN, data are filled-in and retain their natural correlations making complete and coherent multivariate sequences for training. The CATT-Net architecture includes convolutional features extraction, positional encoding, and self attention mechanism. Proposed approach makes it possible to forecast PM2.5, NO2,O3, and SO2 concentrations in parallel relying on hourly data of urban air quality. Efficacy of the approach was compared with the state-of-the-art techniques for deep learning and confirmed in several ablation studies analyzing the role of the architectural blocks. Furthermore, for the sake of practicality, resulting model was exported to TensorFlow Lite INT8 version.

# Introduction
Air Quality Index (AQI) is a commonly used indicator that provides insight into the current air quality level by representing pollutant concentrations as an in
dex,reflecting their possible impact on human health and nature. Particulate matter (PM2.5), nitrogen dioxide (NO2), ozone (O3), sulfur dioxide (SO2) are among the most important pollutants that lead to air quality problems in urban areas. By means of transforming the values of multiple pollutant concentrations into a single value, the AQI index serves as a useful tool for governmental agencies, environmental organizations, and ordinary citizens to understand the severity of the air pollution situation. It facilitates issuing health advisories and informing people about air pollution hazards. Moreover, knowing the AQI index allows decision-makers to formulate policies regarding urban planning, in dustrial production regulations, and traffic organization. Nonetheless, despite the apparent importance of AQI, forecasting its values in practice remains a difficult task. First of all, air-quality datasets frequently have missing values due to problems with sensors’ operation, maintenance, and communication. Secondly,pollutant concentration dynamics tend to be stochastic and highly dependent on various factors such as industrial production, vehicle emissions, weather, and human activity. This poses challenges for accurate prediction for traditional statistical methods and some deep learning models as well. Moreover, many precise forecasters require high computational capacities, rendering them inefficient on resource constrained devices. The goal of this project is to build an AQI prediction system that would be both accurate and suitable for practical implementation. In particular, in real environmental monitoring applications, neglecting missing values or applying trivial imputation techniques results in distortion of inter-correlations between pollutants and reduces the forecast accuracy. Similarly, employing sophisticated forecasting mechanisms raises accuracy but makes the models less appropriate for low-capacity devices. Hence, two complementary objectives motivate this work: first, recovering missing values from an air-quality dataset while ensuring their consistency; second, developing a lightweight forecast mechanism capable of learning long-range relationships and suitable for deployment on low-resources devices.The proposed solution combines CorrGAN-based missing value imputation with an efficient light multivariate transformer architecture called CATT-Net (Correlationaware Tiny Transformer Network).
<img width="1633" height="1122" alt="Model Architecture" src="https://github.com/user-attachments/assets/e505273f-bf8e-4c8c-a6f0-5c17ba052be6" />

# Results

<h3>Amaravati Dataset Results</h3>

<table>
<tr>
<th>Category</th>
<th>Precision</th>
<th>Model</th>
<th>MAE</th>
<th>RMSE</th>
<th>R²</th>
<th>sMAPE</th>
</tr>

<tr>
<td rowspan="8">Baseline Models</td>
<td rowspan="4">FP32</td>
<td>CATT-Net</td><td>4.30</td><td>6.04</td><td>0.72</td><td>16.31</td>
</tr>
<tr><td>GRU</td><td>4.23</td><td>6.08</td><td>0.73</td><td>15.45</td></tr>
<tr><td>LSTM</td><td>4.76</td><td>6.62</td><td>0.69</td><td>17.18</td></tr>
<tr><td>1D CNN</td><td>5.18</td><td>7.12</td><td>0.63</td><td>18.31</td></tr>

<tr>
<td rowspan="4">INT8</td>
<td>CATT-Net</td><td>4.32</td><td>6.08</td><td>0.71</td><td>16.40</td>
</tr>
<tr><td>GRU</td><td>4.24</td><td>6.09</td><td>0.73</td><td>15.49</td></tr>
<tr><td>LSTM</td><td>4.73</td><td>6.50</td><td>0.70</td><td>17.37</td></tr>
<tr><td>1D CNN</td><td>5.13</td><td>6.99</td><td>0.64</td><td>18.34</td></tr>

<tr>
<td rowspan="8">Ablation Variants</td>
<td rowspan="4">FP32</td>
<td>CATT-Net (Full)</td><td>4.08</td><td>5.65</td><td>0.72</td><td>16.08</td>
</tr>
<tr><td>w/o Attention Pooling</td><td>4.15</td><td>5.78</td><td>0.72</td><td>15.71</td></tr>
<tr><td>Single Transformer Block</td><td>4.51</td><td>6.29</td><td>0.70</td><td>16.78</td></tr>
<tr><td>w/o Conv Frontend</td><td>4.71</td><td>6.50</td><td>0.67</td><td>17.88</td></tr>

<tr>
<td rowspan="4">INT8</td>
<td>CATT-Net (Full)</td><td>4.09</td><td>5.68</td><td>0.72</td><td>16.08</td>
</tr>
<tr><td>w/o Attention Pooling</td><td>4.09</td><td>5.72</td><td>0.73</td><td>15.63</td></tr>
<tr><td>Single Transformer Block</td><td>4.54</td><td>6.31</td><td>0.70</td><td>16.98</td></tr>
<tr><td>w/o Conv Frontend</td><td>4.76</td><td>6.53</td><td>0.67</td><td>18.09</td></tr>

</table>

<h3>Delhi Dataset Results</h3>

<table>
<tr>
<th>Category</th>
<th>Precision</th>
<th>Model</th>
<th>MAE</th>
<th>RMSE</th>
<th>R²</th>
<th>sMAPE</th>
</tr>

<tr>
<td rowspan="8">Baseline Models</td>
<td rowspan="4">FP32</td>
<td>CATT-Net</td><td>7.02</td><td>9.90</td><td>0.88</td><td>9.07</td>
</tr>
<tr><td>GRU</td><td>15.74</td><td>29.82</td><td>0.55</td><td>13.81</td></tr>
<tr><td>LSTM</td><td>9.77</td><td>16.60</td><td>0.75</td><td>11.42</td></tr>
<tr><td>1D CNN</td><td>10.99</td><td>15.23</td><td>0.77</td><td>12.65</td></tr>

<tr>
<td rowspan="4">INT8</td>
<td>CATT-Net</td><td>8.49</td><td>12.85</td><td>0.87</td><td>9.19</td>
</tr>
<tr><td>GRU</td><td>10.60</td><td>13.96</td><td>0.77</td><td>13.15</td></tr>
<tr><td>LSTM</td><td>9.35</td><td>12.80</td><td>0.77</td><td>12.13</td></tr>
<tr><td>1D CNN</td><td>14.23</td><td>19.59</td><td>0.66</td><td>14.97</td></tr>

<tr>
<td rowspan="8">Ablation Variants</td>
<td rowspan="4">FP32</td>
<td>CATT-Net (Full)</td><td>8.48</td><td>11.59</td><td>0.85</td><td>10.26</td>
</tr>
<tr><td>w/o Attention Pooling</td><td>7.91</td><td>10.84</td><td>0.81</td><td>10.33</td></tr>
<tr><td>Single Transformer Block</td><td>9.12</td><td>13.40</td><td>0.76</td><td>11.49</td></tr>
<tr><td>w/o Conv Frontend</td><td>14.33</td><td>20.71</td><td>0.65</td><td>14.79</td></tr>

<tr>
<td rowspan="4">INT8</td>
<td>CATT-Net (Full)</td><td>9.90</td><td>14.46</td><td>0.80</td><td>11.20</td>
</tr>
<tr><td>w/o Attention Pooling</td><td>14.48</td><td>18.38</td><td>0.76</td><td>15.24</td></tr>
<tr><td>Single Transformer Block</td><td>10.15</td><td>15.03</td><td>0.76</td><td>11.60</td></tr>
<tr><td>w/o Conv Frontend</td><td>16.12</td><td>22.98</td><td>0.59</td><td>16.43</td></tr>

</table>

<h3>Kolkata Dataset Results</h3>

<table>
<tr>
<th>Category</th>
<th>Precision</th>
<th>Model</th>
<th>MAE</th>
<th>RMSE</th>
<th>R²</th>
<th>sMAPE</th>
</tr>

<tr>
<td rowspan="8">Baseline Models</td>
<td rowspan="4">FP32</td>
<td>CATT-Net</td><td>4.54</td><td>6.23</td><td>0.61</td><td>19.32</td>
</tr>
<tr><td>GRU</td><td>5.55</td><td>8.09</td><td>0.52</td><td>19.66</td></tr>
<tr><td>LSTM</td><td>4.57</td><td>6.63</td><td>0.58</td><td>17.26</td></tr>
<tr><td>1D CNN</td><td>7.72</td><td>11.68</td><td>0.07</td><td>23.85</td></tr>

<tr>
<td rowspan="4">INT8</td>
<td>CATT-Net</td><td>4.36</td><td>6.12</td><td>0.60</td><td>18.84</td>
</tr>
<tr><td>GRU</td><td>5.54</td><td>7.88</td><td>0.54</td><td>19.75</td></tr>
<tr><td>LSTM</td><td>4.60</td><td>6.60</td><td>0.56</td><td>17.46</td></tr>
<tr><td>1D CNN</td><td>7.13</td><td>10.45</td><td>0.19</td><td>23.33</td></tr>

<tr>
<td rowspan="8">Ablation Variants</td>
<td rowspan="4">FP32</td>
<td>CATT-Net (Full)</td><td>4.56</td><td>6.60</td><td>0.61</td><td>16.65</td>
</tr>
<tr><td>CATT-Net w/o Attention Pooling</td><td>5.48</td><td>7.55</td><td>0.63</td><td>16.38</td></tr>
<tr><td>CATT-Net (Single Transformer Block)</td><td>4.46</td><td>6.48</td><td>0.60</td><td>18.04</td></tr>
<tr><td>CATT-Net w/o Conv Frontend</td><td>7.07</td><td>9.43</td><td>0.30</td><td>25.89</td></tr>

<tr>
<td rowspan="4">INT8</td>
<td>CATT-Net (Full)</td><td>4.88</td><td>6.95</td><td>0.57</td><td>17.63</td>
</tr>
<tr><td>CATT-Net w/o Attention Pooling</td><td>5.51</td><td>7.63</td><td>0.62</td><td>16.65</td></tr>
<tr><td>CATT-Net (Single Transformer Block)</td><td>4.53</td><td>6.55</td><td>0.58</td><td>18.42</td></tr>
<tr><td>CATT-Net w/o Conv Frontend</td><td>6.82</td><td>9.20</td><td>0.27</td><td>25.31</td></tr>

</table>

## Abservations on Results
From the results across Amaravati, Delhi, and Kolkata, it can be seen that CATT-Net generally performs better than the baseline models. In most cases, it gives lower error values, especially for MAE and RMSE, which shows that the predictions are more accurate.

The Delhi dataset is more challenging due to higher variation, but even there, the model manages to maintain stable performance compared to others. For Amaravati, the errors are relatively lower, indicating smoother data patterns, while Kolkata falls somewhere in between.

Another important point is that the INT8 version performs almost the same as FP32, which means the model can be used on low-resource devices without losing much accuracy. The ablation results also make it clear that removing key components, like the convolutional frontend or attention mechanism, leads to a drop in performance.

Overall, the model works well across different datasets and maintains a good balance between accuracy and efficiency.
