# Project Title - Financial Planning

## Introduction
This project aims to build a financial planning tool prototype for a large credit union which will allow its members to evaluate their financial health through monthly budgets and retirement planning.   


## Technologies
**Python Libraries**

`python 3.9.12`<br>
`python-dotenv` 1.0<br>
`requests 2.27.1`<br>
`json 0.9.6`<br>
`pandas 1.4.2`<br>
`alpaca_trade_api 3.0`<br>
`%matplotlib inline 0.1.2`<br>


## Installation Guide

[Install anaconda](https://www.anaconda.com/download/)

To clone and run this application, you'll need Git installed on your computer.
From your command line:
```
#Create a new conda environment
conda create -n your_env_name python=3.8

# Install dependencies in conda environment
pip install jupyter lab
conda install -c anaconda requests
conda install -c jmcmurray json
pip install python-dotenv
pip install alpaca-trade-api

# Clone this repository
git clone https://github.com/AlexanderValenzuela/financial_planning

# Activate conda environment
conda activate your_env_name

# In the conda environment, run Jupyter Lab
jupyter lab 
```
---

## Usage
Part 1. Create a Financial Planner for Emergencies<br>
In this section, you’ll create a personal financial planner for emergencies. To develop the prototype, assume the following:<br>
- The average monthly household income for each credit union member is $12,000.<br>
- Each credit union member has a savings portfolio that consists of a cryptocurrency wallet, stocks, and bonds.<br>

 Use the starter code in `financial_planning_tools.ipynb` to complete the steps in the following subsections.

Evaluate the Cryptocurrency Wallet by Using the Requests Library<br>
In this section, you’ll determine the current value of a member’s cryptocurrency wallet. You’ll collect the current prices for the Bitcoin and Ethereum cryptocurrencies by using the Python Requests library. For the prototype, you’ll assume that the member holds the 1.2 Bitcoins (BTC) and 5.3 Ethereum coins (ETH). To do all this, complete the following steps:<br>

1. Create a variable named `monthly_income`, and set its value to `12000`.

2. Use the Requests library to get the current price (in US dollars) of Bitcoin (BTC) and Ethereum (ETH) by using the API endpoints that the starter code supplied.

3. Navigate the JSON response object to access the current price of each coin, and store each in a variable.

4. Calculate the value, in US dollars, of the current amount of each cryptocurrency and of the entire cryptocurrency wallet.


Evaluate the Stock and Bond Holdings by Using the Alpaca SDK<br>
In this section, you’ll determine the current value of a member’s stock and bond holdings. You’ll make an API call to Alpaca via the Alpaca SDK to get the current closing prices of the SPDR S&P 500 ETF Trust (ticker: SPY) and of the iShares Core US Aggregate Bond ETF (ticker: AGG). For the prototype, assume that the member holds 110 shares of SPY, which represents the stock portion of their portfolio, and 200 shares of AGG, which represents the bond portion. To do all this, complete the following steps:

1. In the `Starter_Code` folder, create an environment file (`.env`) to store the values of your Alpaca API key and Alpaca secret key.

2. Set the variables for the Alpaca API and secret keys. Using the Alpaca SDK, create the Alpaca `tradeapi.REST` object. In this object, include the parameters for the Alpaca API key, the secret key, and the version number.

3. Set the following parameters for the Alpaca API call:

- `tickers`: Use the tickers for the member’s stock and bond holdings.

- `timeframe`: Use a time frame of one day.

- `start_date` and `end_date`: Use the same date for these parameters, and format them with the date of the previous weekday (or `2020-08-07`). This is because you want the one closing price for the most-recent trading day.

4. Get the current closing prices for `SPY` and `AGG` by using the Alpaca `get_bars` function. Format the response as a Pandas DataFrame by including the df property at the end of the `get_bars` function.

5. Navigating the Alpaca response DataFrame, select the `SPY` and `AGG` closing prices, and store them as variables.

6. Calculate the value, in US dollars, of the current amount of shares in each of the stock and bond portions of the portfolio, and print the results.

Evaluate the Emergency Fund<br>
In this section, you’ll use the valuations for the cryptocurrency wallet and for the stock and bond portions of the portfolio to determine if the credit union member has enough savings to build an emergency fund into their financial plan. To do this, complete the following steps:

1. Create a Python list named `savings_data` that has two elements. The first element contains the total value of the cryptocurrency wallet. The second element contains the total value of the stock and bond portions of the portfolio.

2. Use the `savings_data` list to create a Pandas DataFrame named `savings_df`, and then display this DataFrame. The function to create the DataFrame should take the following three parameters:

- `savings_data`: Use the list that you just created.

- `columns`: Set this parameter equal to a Python list with a single value called `amount`.

- `index`: Set this parameter equal to a Python list with the values of `crypto` and `stock/bond`.

3. Use the `savings_df` DataFrame to plot a pie chart that visualizes the composition of the member’s portfolio. The y-axis of the pie chart uses `amount`. Be sure to add a title.

4. Using Python, determine if the current portfolio has enough to create an emergency fund as part of the member’s financial plan. Ideally, an emergency fund should equal to three times the member’s monthly income. To do this, implement the following steps:

- Create a variable named `emergency_fund_value`, and set it equal to three times the value of the member’s `monthly_income` of $12000. (You set this earlier in Part 1).

- Create a series of three if statements to determine if the member’s total portfolio is large enough to fund the emergency portfolio:

     - If the total portfolio value is greater than the emergency fund value, display a message congratulating the member for having enough money in this fund.

     - Else if the total portfolio value is equal to the emergency fund value, display a message congratulating the member on reaching this important financial goal.

     - Else the total portfolio is less than the emergency fund value, so display a message showing how many dollars away the member is from reaching the goal. (Subtract the total portfolio value from the emergency fund value.)

Part 2: Create a Financial Planner for Retirement<br>
In this section, you’ll use the Alpaca API to get historical closing prices for a retirement portfolio. You’ll then run Monte Carlo simulations to forecast the portfolio performance 30 years from now. You’ll use the simulated data to answer questions in your Jupyter notebook about the portfolio.

Use the starter code in `financial_planning_tools.ipynb` to complete the steps in the following subsections.

Create the Monte Carlo Simulation<br>
In this section, you’ll use the MCForecastTools library to create a Monte Carlo simulation for the member’s savings portfolio. To do this, complete the following steps:<br>

1. Make an API call via the Alpaca SDK to get 3 years of historical closing prices for a traditional 60/40 portfolio split: 60% stocks (SPY) and 40% bonds (AGG).

2. Run a Monte Carlo simulation of 500 samples and 30 years for the 60/40 portfolio, and then plot the results. The following image shows the overlay line plot resulting from a simulation with these characteristics. However, because a random number generator is used to run each live Monte Carlo simulation, your image will differ slightly from this exact image:
![5-4-monte-carlo-line-plot](https://user-images.githubusercontent.com/111409358/233838237-db0eec40-f1f2-43c5-89c9-be84ffca5c1b.png)

3. Plot the probability distribution of the Monte Carlo simulation. The following image shows the histogram plot resulting from a simulation with these characteristics. However, because a random number generator is used to run each live Monte Carlo simulation, your image will differ slightly from this exact image:
![5-4-monte-carlo-histogram](https://user-images.githubusercontent.com/111409358/233838305-ddf5f2e3-68c9-489a-8e44-e12357b658c7.png)

4. Generate the summary statistics for the Monte Carlo simulation.

Analyze the Retirement Portfolio Forecasts<br>
Using the current value of only the stock and bond portion of the member's portfolio and the summary statistics that you generated from the Monte Carlo simulation, answer the following question in your Jupyter notebook:<br>

- What are the lower and upper bounds for the expected value of the portfolio with a 95% confidence interval?

Forecast Cumulative Returns in 10 Years<br>
The CTO of the credit union is impressed with your work on these planning tools but wonders if 30 years is a long time to wait until retirement. So, your next task is to adjust the retirement portfolio and run a new Monte Carlo simulation to find out if the changes will allow members to retire earlier.<br>

For this new Monte Carlo simulation, do the following:<br>

- Forecast the cumulative returns for 10 years from now. Because of the shortened investment horizon (30 years to 10 years), the portfolio needs to invest more heavily in the riskier asset—that is, stock—to help accumulate wealth for retirement.

- Adjust the weights of the retirement portfolio so that the composition for the Monte Carlo simulation consists of 20% bonds and 80% stocks.

- Run the simulation over 500 samples, and use the same data that the API call to Alpaca generated.

- Based on the new Monte Carlo simulation, answer the following questions in your Jupyter notebook:

    - Using the current value of only the stock and bond portion of the member's portfolio and the summary statistics that you generated from the new Monte Carlo simulation, what are the lower and upper bounds for the expected value of the portfolio (with the new weights) with a 95% confidence interval?

    - Will weighting the portfolio more heavily toward stocks allow the credit union members to retire after only 10 years?



## Contributors
Alexander Valenzuela<br>
[LinkedIn Profile](<https://www.linkedin.com/in/alex-valenzuela-97826842/>)


## License
Licensed under the MIT License



