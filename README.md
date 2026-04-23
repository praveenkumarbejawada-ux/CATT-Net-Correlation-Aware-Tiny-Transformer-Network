# CATT-Net-Correlation-Aware-Tiny-Transformer-Network
CATT-Net is a lightweight deep learning model for air quality prediction using incomplete real-world data. It combines CorrGAN-based data imputation with a tiny transformer to capture temporal patterns and pollutant correlations. Designed for multi-pollutant forecasting, it is optimized for deployment on resource-constrained edge devices.
CATT-Net: Correlation-Aware Tiny Transformer Network

Air quality prediction is a challenging problem, especially when working with real-world data that is often incomplete, noisy, and highly dynamic. This project presents CATT-Net, a lightweight and efficient deep learning framework designed for multivariate air quality forecasting on resource-constrained devices.

The core idea behind this work is to address two practical issues simultaneously:

Handling missing sensor data
Building an accurate yet lightweight prediction model

To deal with missing values, the project uses a CorrGAN-based imputation approach, which reconstructs incomplete data while preserving correlations between pollutants. Instead of relying on simple interpolation, this method helps maintain realistic relationships in the dataset.

For forecasting, the proposed CATT-Net architecture combines:

A convolutional frontend to capture short-term temporal patterns
A tiny transformer encoder to learn long-range dependencies
A hybrid pooling mechanism for better feature aggregation

This design keeps the model compact while still delivering strong performance.

The system is trained to predict multiple pollutants simultaneously (PM2.5, NO2, O₃, SO₂) using hourly air quality data. It is evaluated across multiple datasets and compared with baseline models such as CNN, LSTM, and GRU.

To make the solution practical for deployment, the trained model is also converted into an INT8 TensorFlow Lite format, making it suitable for edge devices with limited computational resources.
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
<img width="633" height="384" alt="image" src="https://github.com/user-attachments/assets/577b4834-9f61-4276-a8c3-3828d300a992" />
<img width="626" height="386" alt="image" src="https://github.com/user-attachments/assets/3f250c18-f3c1-465b-b505-cedc4071714d" />
<img width="634" height="397" alt="image" src="https://github.com/user-attachments/assets/246a1013-197e-4eda-a935-90c6e3255546" />
