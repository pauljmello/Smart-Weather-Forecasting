## Table of Contents

1. [Requirements ](#requirements)
2. [Problem Description](#problem-details)
3. [Project Objectives](#project-objectives)
4. [Data](#project-data)
5. [Model Types](#model-types)
6. [Analysis and Results](#analysis-and-results)
7. [Discussion](#discussion)

## Requirements

- Python 3.10
- NumPy
- pandas
- scikit-learn
- XGBoost
- PyTorch

## Problem Description

Weather forecasting is a traditionally difficult process. In recent decades progress has been made to create weather forecasting models on global scales capable of predicting the weather up to a week in advance. Recently advances in diffusion models have demonstrated superior weather forecasting capabilities at reduced computational costs to more traditional ML approaches. However, industrial models are primarily built using machine learning and or deep neural networks with tabular data. These industrial models are difficult to train due to the immense computational costs as well as the enormous training data that is necessary to create relatively accurate predictions. This has resulted in weather forecasting to be consolidated to corporations with the resources to train these models. Unfortunately, this approach leads to non-region specific models that suffer from precise predictions.

In a recent paper published, https://arxiv.org/pdf/2008.10789.pdf, they propose a different approach to these global models by instead selecting a few cities nearby a target city and using their data to predict the weather of the target city. They demonstrate this approach to be relatively successful within reasonable bounds. This approach puts weather forecasting models in the hands of researchers and individuals with access to less resources. Importantly, while this approach is relatively successful, the traditional large scale global models are still more accurate. As a result using both the results from a local model and the global model can be seen as a fine tuned improvement of local predictions. One notable caveat to this approach is the necessity of developing and training models for each region rather than a single large model. However, given the tighter spatial weather regions it is likely these models can converge quicker.


## Project Objectives

The objective of this project is to replicate a nearly identical approach to what is seen in the smart weather forecasting paper. We desire to recreate their success and attempt to use historical data as well as forecast data in order to develop stronger models with better prediction accuracies. We ultimately aim to predict the temperature of San Jose by using nearby cities in the bay area. We aim to improve on their results by utilizing large training data and attempt to demonstrate the feasibility of the model. 

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

A lot of potentially relevant data was collected from https://open-meteo.com, then preprocessed out depending on relevancy and similarity between forecast and archive data. Notably, the distinction between forecast and archive data is important as archive data may contain significantly more features, while forecast data consists of future predictions. Through this project I was able to recreate the results of the paper above and introduce various abstract methods capable of handling the tricky instances presented in tabular weather forecasting. In order to assert what features contributed the most to predicting the temperature in the target city I performed PCA to understand the data better and improve model speed.

![PCA on Features from Archive Data](/Images/ArchivePCA.png)

We can see from the results below that two approaches in particular proved incredibly powerful in developing weather forecasting models, random forest regression, followed by DNNs. These approaches were the 1st and second best results across the board with particularly good RMSE on random forest regression.

![Weather Forecasting using Archive Data and Regression](/Images/Archive_Regression_RMSE.png)

![DNN Forecast Prediction from Archive Data](/Images/Predict_SJ_Temps_From_Archive_DNN.png)

I believe with improved hyperparameters, more features, and a various other changes to the notebook these scores may be significantly reduced. However, for the time being these demonstrate the feasibility and capabilities of weather forecasting and ML model predictions respectively. 

## Discussion

As previously stated, these approaches put weather forecasting in the hands of individuals with limited resources at the cost of preciseness. They should be used in a manner that considers the effectiveness and accuracy of global forecasting models trained with significant computation and data. However, for mundane tasks, this approach yields previously unseen results at a significant fraction of the cost and power of more traditional methods.
