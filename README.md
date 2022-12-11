# Cryptocurrencies
Module 18

# Project Overview

This project is intended to practice using machine learning using unsupervised algorithms. The intent is to be able to explore data with no predetermined goal, but, instead, find trends within the dataset. We will primarily be using K-means algorithm to group similar data into clusters. To speed up this process we will be using principal component analysis (PCA).

# Results

## Data Preprocessing & Transformation

The dataset we used was from [CryptoCompare](https://min-api.cryptocompare.com/data/all/coinlist). Using pandas, we extracted CoinName, Algorithm, IsTrading, ProofType, TotalCoinsMined, and MaxSupply (later renamed to TotalCoinSupply) from the dataset. 
To ensure we had meaningful data we preformed the following:
 1. Removed all cryptocurrencies that were not being traded and dropped the column
    - ['IsTrading'] == True
    - drop.(columns='IsTrading')
 2. Removed all cryptocurrencies with a non-functional algorithm
    - ['Algorithm'] != 'N/A'
 3. Removed all cryptocurrencies that had no yet been mined
    - ['TotalCoinsMined'] > 0
 4. Removed all rows with at least one null value
    - .isna() == True;l.pl;.
 5. Create a new DataFrame that contains all the cryptocurrency names then drop CoinName from the origianl DataFrame
 6. Create dummy variables, with respect to 'Algorithm' and 'ProofType', for all the text features into a variable 'X' and standardize that data with StandardScalar
 <img src="<link>" width="300">

## Reducing Data Dimensions Using PCA

After our data has been properly processed and transformed we move on to using principal component analysis, or PCA, to reduce the dimension of the 'X' DataFrame down to three principal components that will be put into 'crypto_pca'. Using 'crypto_pca' we will create a new DataFrame, 'pcs_df', with the three principal components as columns "PC 1", "PC 2", "PC 3" using 'crypto_df' as our index. 

## Clustering CryptoCurrencies Using K-Means

Using an elbow curve, we are able to determine that the appropriate K value should be 4. With that in mind we are able to initialize the K-Means Model and predict clusters. From there we will concatenate the 'crypto_df' and 'pcs_df' DataFrames to create a new DataFrame that we will use for our visualizations.

## Visualizing Cryptocurrency Results

Using the DataFrame created from the previous step we are able to create  a 3D scatter plot with "PC 1", "PC 2", and "PC 3" as the x, y, and z parameters, respectfully. 
We then used hvplot.table to create a data table of all tradable cryptocurrencies and made sure to include 'CoinName', 'Algorithm', 'ProofType', 'TotalCoinSupply', 'TotalCoinsMined', 'Class'.
Finally, we created a new cluster that included 'TotalCoinSupply', 'TotalCoinsMined', 'CoinName', and 'Class'. This gave us some insight on the current supply vs demand for available cryptocurrencies.

# Summary

By using unsupervised machine learning we were able to cluster various cryptocurrencies into meaningful data that was hidden from plain sight. The data here can be used to recommend, and possibly forecast, potential investment opportunities in the crypto space (away from FTX).

