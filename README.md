# plane_delay_project
Abstract 

This research analyzes the effect of the geographical dispersion of U.S. airports on flight delay patterns using statistical and machine learning methods. Based on a large database of flight data, the research applies several regression and ARMA time series modeling to investigate the comparative significance of regional, temporal, and operational factors in influencing flight delays. Arrival and departure delay-specific regression models are specified, and variable definitions are provided. The results indicate that geographic areas, in conjunction with meteorological conditions and transportation disruptions, impose considerable impacts on both arrival and departure delays. The findings' implications call for region-specific delay reduction strategies and form the basis of more efficient delay forecasting methods. 

1. Introduction 

Flight delays represent a major challenge to U.S. aviation operations, affecting both operational efficiency and passenger satisfaction (Bureau of Transportation Statistics, 2023). Accurate delay prediction and understanding are of great value to airlines, regulators, and travelers. Traditional studies overlook the impact of geographic regionalization on delay patterns. This study aims to quantify regional factors' contributions to delay volatility and to create predictive models that can aid in operational decision-making. 

2. Literature Review 

Past research has established that flight delays are caused by a set of factors, including meteorological conditions, airline performance, airport congestion, and air traffic control (Xu et al., 2020; Glickman et al., 2019). The impact of geographic boundaries—such as regional categorizations of airports—is, however, not examined exhaustively. It is argued in some research that regional climatic conditions and differences in infrastructure may cause consistent differences in delay patterns (Wang & Memon, 2020). 

3. Methodology 

3.1 Variable Definitions and Model Specification 

A. Arrival Delay (ARR_DELAY) Model 

Dependent Variable: 

ARR_DELAY: Arrival delay in minutes. 

Independent Variables: 

DEST_REGION: Region of destination (categorical; dummy variables required). 

DEST_AIRPORT_ID: Destination airport ID (categorical; dummy encoding or clustering if too many categories). 

OP_CARRIER_AIRLINE_ID: Operating carrier airline ID (categorical). 

IS_WEEKEND: Dummy variable (1 if flight was on a weekend, 0 otherwise). 

ACTUAL_ELAPSED_TIME: Actual flight duration in minutes. 

ARR_TIME: Scheduled or actual arrival time (numeric or categorical time blocks). 

CARRIER_DELAY, WEATHER_DELAY, NAS_DELAY, SECURITY_DELAY, LATE_AIRCRAFT_DELAY: Components of delay by cause (all numeric). 

** i indexes individual flights and t indexes time (day).** 

Regression Model: 

ARR_DELAYit =β0 +β1 DEST_REGIONi +β2 DEST_AIRPORT_IDi +β3 OP_CARRIER_AIRLINE_IDi +β4 IS_WEEKENDt +β5 ACTUAL_ELAPSED_TIMEit +β6 ARR_TIMEit +β7 CARRIER_DELAYit +β8 WEATHER_DELAYit +β9 NAS_DELAYit +β10 SECURITY_DELAYit +β11 LATE_AIRCRAFT_DELAYit +ϵit   

 

B. Departure Delay (DEP_DELAY) Model 

Dependent Variable: 

DEP_DELAY: Departure delay in minutes. 

Independent Variables: 

ORIGIN_REGION: Region of origin (categorical; dummy variables required). 

ORIGIN_AIRPORT_ID: Origin airport ID (categorical). 

OP_CARRIER_AIRLINE_ID: Operating carrier airline ID (categorical). 

IS_WEEKEND: Dummy variable (1 if Saturday or Sunday, 0 otherwise). 

ACTUAL_ELAPSED_TIME: Actual flight duration in minutes. 

DEP_TIME: Scheduled or actual departure time (continuous or binned). 

CARRIER_DELAY, WEATHER_DELAY, NAS_DELAY, SECURITY_DELAY, LATE_AIRCRAFT_DELAY: Components of delay by cause (all numeric). 

** i indexes individual flights and t indexes time (day).** 

Regression Model: 

DEP_DELAYit =β0 +β1 ORIGIN_REGIONi +β2 ORIGIN_AIRPORT_IDi +β3 OP_CARRIER_AIRLINE_IDi +β4 IS_WEEKENDt +β5 ACTUAL_ELAPSED_TIMEit +β6 DEP_TIMEit +β7 CARRIER_DELAYit +β8 WEATHER_DELAYit +β9 NAS_DELAYit +β10 SECURITY_DELAYit +β11 LATE_AIRCRAFT_DELAYit +ϵit   

Note: 

 Categorical variables (regions, airports, airlines) are converted  handled as fixed effects. Delay components are expected to have a positive association with the dependent variable. 

3.2 Data Collection 

Data were sourced from the U.S. Department of Transportation, covering the years 2014–2024. The dataset includes millions of records with details on arrival/departure delays, delay causes, geographic information, and operational factors. 

3.3 Data Processing 

Cleaning: Duplicates and missing values were removed; categorical variables were mapped using state FIPS codes. 

Feature Engineering: Created new features such as weekend indicators and lagged delay variables. 

Aggregation: Monthly average delays by region were computed for trend analysis. 

3.4 Statistical and Time Series Analysis 

Correlation Analysis: Heatmaps were used to examine relationships between variables. 

Stationarity Tests: KPSS tests and differencing were employed to prepare data for time series modeling. 

Regression Modeling: Multiple regression was used to estimate the effect of regional and operational factors on delays, following the explicit model specifications above. 

3.5 Time Series Modeling: ARMA and ARMAX 

ARMA (AutoRegressive Moving Average) Models: 

 ARMA models were used to model the temporal dependencies in the time series of average delays. ARMA models capture autocorrelation by modeling both autoregressive (AR) and moving average (MA) terms, making them better suited to predict delay patterns that recur over time. 

ARMAX (AutoRegressive  Moving Average with eXogenous Variables) Models: 

 The ARMA/ARMAX approach extends ARMA by allowing for non-stationary data (differencing) and incorporating exogenous regressors such as region codes or other relevant variables. 

Model Selection: Model parameters (p, d, q) were chosen using ACF/PACF plots and stationarity diagnostics. 

Exogenous Regressors: Regional variables (e.g., ORIGIN_REGION, DEST_REGION) were included to directly test the impact of geography on delay dynamics. 

Diagnostics: Model residuals were checked for autocorrelation (Ljung-Box), normality (Jarque-Bera), and heteroskedasticity to validate model fit. 

Prediction: The models were used for both in-sample and out-of-sample prediction of average delays. 

4. Results 

4.1 Exploratory Analysis 

Correlation matrices revealed that: 

Delay causes (weather, NAS, carrier, late aircraft) are positively correlated with total delays. 

Regional variables (origin and destination regions) show moderate but significant correlations with delays. 

4.2 Regression Results 

Arrival Delay Model:  

Significant predictors: DEST_REGION, NAS_DELAY, CARRIER_DELAY, WEATHER_DELAY, LATE_AIRCRAFT_DELAY (p < 0.01). 

R²: 0.017, indicating delays are influenced by many unobserved factors. 

Departure Delay Model:  

Significant predictors: ORIGIN_REGION, NAS_DELAY, CARRIER_DELAY, WEATHER_DELAY, LATE_AIRCRAFT_DELAY (p < 0.01). 

R²: 0.012. 

4.3 Out-of-Sample Regression Prediction: Low-End and High-End Airlines 

To test the practical predictive ability of the regression models for different airline categories, out-of-sample forecasts were carried out on two different carriers, including one low-cost carrier and one premium carrier: 

Low-End Carrier: Frontier Airlines (OP_CARRIER_AIRLINE_ID = 20436) 

High-End Carrier: Delta Airlines (OP_CARRIER_AIRLINE_ID = 19790) 

Testing and Evaluation Process: 

The respective test datasets for 2023–2024 were filtered by airline. 

Regression models (for both ARR_DELAY and DEP_DELAY) were used to predict delays for each airline. 

Predictions were compared to actual values using Mean Squared Error (MSE) and Mean Absolute Error (MAE). 

Results: 

Arrival Delay Prediction: 

Frontier (Low-End):  

MSE: 3612.54 

MAE: 28.58 minutes 

Delta (High-End):  

MSE: 2663.31 

MAE: 24.05 minutes 

Departure Delay Prediction: 

Frontier (Low-End):  

MSE: 3389.64 

MAE: 25.39 minutes 

Delta (High-End):  

MSE: 2454.81 

MAE: 20.70 minutes 

Interpretation: 

The regression models have a modest degree of predictive power for low-end and high-end carriers, but mean absolute error (MAE) is somewhat lower for Delta, indicating that high-end carriers tend to have more stable or less volatile delay patterns. 

The models can be utilized for operational forecasting, though with the caveat that variability in delay continues to be high, particularly in low-cost carriers. 

4.4 ARMAX/ARIMAX Model Results 

Model Fitting and Coefficient Interpretation 

Departure Delay (DEP_DELAY): 

 An ARIMA(9, 0, 9) model with DEST_REGION as exogenous variable was fitted: 

DEST_REGION is highly significant (p = 0.006), showing strong regional effects. 

Several AR and MA terms are statistically significant, confirming the temporal dependence in delays. 

Model diagnostics (see SARIMAX output) indicate good fit:  

Ljung-Box Q = 0.06 (p = 0.81): No autocorrelation in residuals. 

Jarque-Bera JB = 4.27 (p = 0.12): Residuals are approximately normal. 

Skew = 0.15, Kurtosis = 3.40: Residuals are fairly symmetric and close to normal. 

Heteroskedasticity H = 0.66 (p = 0.02): Some evidence of non-constant variance. 

Arrival Delay (ARR_DELAY): 

 ARIMA(12, 0, 9) with ORIGIN_REGION as exogenous variable: 

ORIGIN_REGION highly significant (p < 0.001). 

Model diagnostics indicate no autocorrelation and near-normal residuals. 

Some evidence of heteroskedasticity. 

Model Performance (see plots and tables): 

Picture 

Picture 

 

 

Picture 

Picture 

 

Predicted vs Actual (see SARIMAX plots):  

The ARIMAX model’s predicted series (orange dashed) closely tracks the actual series (blue) for both arrival and departure delays. 

The ARMAX models effectively capture seasonal and short-term fluctuations, with some deviations during extreme events. 

 

5. Discussion 

 

The results indicate that geographic region is a statistically significant explanatory factor for delays even after controlling for operational and weather factors. The relatively low R² values exhibited in regression models illustrate the high variance and complexity inherent in flight operations; however, the significance placed on region still holds. In addition, time series models confirm the predictive utility of regional variables, which implies that airlines and policymakers must consider regional effects when scheduling and allocating resources. 

  

Limitations consist of possible unobserved confounders (e.g., airport-specific practices, real-time weather events) and the utilization of aggregated regional proxies instead of granular airport- or city-level variables. 

6. Conclusion 

This study demonstrates that U.S. geographic divisions meaningfully affect flight delay patterns. Both regression and time series analyses highlight the importance of region alongside traditional delay causes. The explicit regression model structure provides clarity for future modeling efforts. The methodology and findings provide a basis for developing more robust, regionally tailored delay mitigation strategies. 

 

References 

Bureau of Transportation Statistics (2025). Airline On-Time Performance Data. 

Glickman, T., et al. (2019). "Assessing the Impact of Weather on Aviation Delays." Journal of Air Transport Management, 75, 56–66. 

Wang, S., & Memon, M. (2020). "Regional Variability in U.S. Flight Delays." Transportation Research Record, 2674(5), 123–134. 

Xu, X., An, Y., & Chen, H. (2020). "A Review of Flight Delay Prediction Models." Aerospace, 7(8), 101. 
