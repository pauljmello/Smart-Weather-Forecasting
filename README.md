## Table of Contents

1. [Requirements ](#requirements)
2. [Problem Description](#problem-details)
3. [Project Objectives](#project-objectives)
4. [Data](#project-data)
5. [Model Types](#model-types)
6. [Analysis and Results](#analysis-and-results)
7. [Discuession](#discussion)

## Requirements

- Python 3.10
- NumPy
- pandas
- scikit-learn
- XGBoost
- PyTorch

## Problem Description

Weather forecasting is a traditionally difficult process. In recent decades progress has been made to create weather forecasting models on global scales capable of predicting the weather up to a week in advance. Recently advances in diffusion models have demonstrated superior weather forecasting capbiilities at a reduced computational costs to more traditional ML approaches. However, industrial models are primarily built using ML/DNN models on tabular data. These industrial models are difficult to train due to the immense computational costs as well as the immense training data that is necessary to create accurate predictions. This has resulted in weather forecasting to be consolodated to corporations with the resources to train these models. 

In a recently paper published, https://arxiv.org/pdf/2008.10789.pdf, they propose a different approach to these global models by instead selecting a few cities nearby a  target city and use their data to predict the weather of the target city. They demonstrate this approach to be realatively successful within reason. This approach puts weather forecasting models in the hands of researchers and individuals with access to less resources. Importantly, while this approach is relatively successful, the traditional large scale global models are still more accurate. As a result using both the results from a local model and the global model can be seen as a fine tuned improvement of local predictions.

## Project Objectives

In this code I attempt to replicate a nearily identitcal approach as seen in the paper, with various ablations, and attempt to recreate their success. Ultimately, this is a success as we demonstrate that our models can accurately predict the weather of a target city when given nearby data. 

## Data

The data is collected from https://open-meteo.com/ and focuses on key cities around the bay area, with the aim of predicting the temperature in San Jose. Notably, two types of weather data was collected, historical archive data of the cities dating back to the 1960s, and the predicted forecast for the following week starting on 4/27/2023. Models are trained to predict each data type (archive and forecast); However, the archive models are also then tested ti predict the forecasting data. This demonstrate the capabilities of these models to predict current and future weather. The freshness of this model will deteriorate over time and will need more data to continue to remain accurate. 

## Model Types

This notebook trains multiple regression methods which can be found in the "Models" folder. Unfortunately, the random forrest regression model must be omitted due to githubs file size requirements.

- Polynomial Regression
- Random Forest Regression
- Ridge Regression
- XGBoost Regression
- Deep Neural Network (using PyTorch)

## Analysis and Results

Ultimately, I was able to recreate the results of the paper above and introduce various abstract methods capable of handling the tricky instances presented in tabular weather forecasting. I performed PCA to demonstrate and select the relevant components for faster models and better feature extraction. 

![PCA on Features from Archive Data](/Images/ArchivePCA.png)

We can see from the results below that two approaches inparticular proved incredibly powerful in developing weather forecasting models, random forrest regression, followed by DNNs. These approaches were the 1st and second best results accross the board with particularly good RMSE on random forrest regression. 

![Weather Forecasting using Archive Data and Regression](/Images/Archive_Regression_RMSE.png)

![DNN Forecast Prediction from Archive Data](/Images/Predict_SJ_Temps_From_Archive_DNN.png)

I believe with improved hyperparameters, more features, and a various other changes to the notebook these scores may be significantly reduced. However, for the time being these demonstrate the feasibility and capabilities of weather forecasting and ML model predictions respectively. 

## Discussion

As previously stated, these approaches put weather forecasting in the hands of individuals with limited resources at the cost of preciseness. They should be used in a manner that considers the effectiveness and accuracy of global forecasting models trained with significant computation and data. However, for mundane tasks, this approach yields previously unseen results at a significant fraction of the cost and power of more traditional methods.
