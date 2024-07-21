# Capital-Asset-Pricing-Model


The Capital Asset Pricing Model (CAPM) is a fundamental model in finance that describes the relationship between the expected return and the risk of investing in a security. It states that the expected return on a security is equal to the risk-free rate plus a risk premium. The formula is represented as:

\[ r_i = r_f + \beta_i (r_m - r_f) \]

Where:
- \( r_i \): Expected return of the security
- \( r_f \): Risk-free rate of return
- \( \beta_i \): Beta of the security
- \( r_m \): Expected return of the market

Components of CAPM

1. **Risk-Free Rate of Return (\( r_f \))
   - Assumed to be a zero-risk asset with zero standard deviation.
   - Typically represented by a U.S. government 10-year Treasury bill.
   - Investors who are risk-averse prefer this asset as it provides a low but guaranteed return.

2. **Market Portfolio Return (\( r_m \))**
   - Represents the overall return of the market.
   - A good representation is the S&P 500 index, which includes the 500 largest U.S. publicly traded companies.
   - The S&P 500 is a market-capitalization-weighted index viewed as a gauge of large-cap U.S. equities.

#### **Project Steps Using Python**

1. **Data Collection**
   - Gather historical data for the risk-free rate, market portfolio return (e.g., S&P 500), and the individual security's return.
   - Data can be sourced from financial APIs such as Yahoo Finance or Alpha Vantage.

2. **Data Preprocessing**
   - Clean the data to handle missing values and ensure consistency.
   - Calculate the daily, monthly, or yearly returns for the market portfolio and the individual security.

3. **Calculating Beta (\( \beta_i \))**
   - Use linear regression to determine the beta of the security.
   - The beta (\( \beta_i \)) is the slope of the regression line between the security's returns and the market returns.

4. **Implementing CAPM Formula**
   - Calculate the expected return of the security using the CAPM formula.
   - Compare the CAPM expected return with the actual historical return to evaluate the model's accuracy.

5. **Visualization**
   - Plot the security's historical returns against the market returns.
   - Visualize the regression line to depict the relationship and the beta value.

6. **Risk Premium Analysis**
   - Calculate the risk premium, which is the incentive for investing in a risky security over a risk-free asset.
   - Analyze the results to make informed investment decisions.

#### **Sample Python Code Snippet**

```python
import numpy as np
import pandas as pd
import yfinance as yf
from scipy.stats import linregress
import matplotlib.pyplot as plt

# Fetch data from Yahoo Finance
stock_data = yf.download('AAPL', start='2010-01-01', end='2020-01-01')
market_data = yf.download('^GSPC', start='2010-01-01', end='2020-01-01')
risk_free_rate = 0.01  # Example risk-free rate

# Calculate daily returns
stock_returns = stock_data['Adj Close'].pct_change().dropna()
market_returns = market_data['Adj Close'].pct_change().dropna()

# Perform linear regression to find beta
slope, intercept, r_value, p_value, std_err = linregress(market_returns, stock_returns)
beta = slope

# Calculate expected return using CAPM
expected_return = risk_free_rate + beta * (market_returns.mean() - risk_free_rate)

# Plotting the results
plt.scatter(market_returns, stock_returns, alpha=0.5)
plt.plot(market_returns, intercept + beta * market_returns, color='red')
plt.xlabel('Market Returns')
plt.ylabel('Stock Returns')
plt.title('CAPM Regression Line')
plt.show()

print(f'Beta: {beta}')
print(f'Expected Return: {expected_return}')
```

#### **Conclusion**

By implementing the CAPM model in Python, we can estimate the expected return on a security based on its beta and the market's expected return. This analysis helps investors understand the risk-return tradeoff and make informed investment decisions. The visualization and regression analysis provide insights into the relationship between the security and the market, highlighting the security's sensitivity to market movements.
