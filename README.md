# Asset-Allocation-Risk-Parity

I replicated the paper "Leverage Aversion and Risk Parity" by Cliord S. Asness, Andrea Frazzini, and Lasse H. Pedersen (2012, Financial Analysts Journal, Volumne 68, Number 1).

Problem 1
I retrieve the data from WRDS in the section CRSP > Annual Update> Treasuries > CRSP TREASURIES - Issue Descriptions and Monthly Time Series. My time period is from Jan 1926 to Dec 2018. I use monthly data. 
I exclude entries with returns -99 and   rows where we have missing data in at least one column.
I define weights of bond value weighted return as lagged capitalization of the firm divided by lagged total market capitalization. Then I found value weighted return of the market in each month by multiplying weights of the company by its return and summing it up under every month.


Problem 2
I retrieve the data from WRDS in the section CRSP > Annual Update> Index / Treasury and Ination > US Treasury and Inflation Indexes. My time period is from Jan 1926 to Dec 2018. I use monthly data. 
I find excess return of bonds and stocks as : value weighted return of bond/stock on particular month minus 30 day risk free rate.


Problem 3

I define Excess value weighted return on each month as excess stock return multiplied by total stock lagged capitalization and divided by (total stock lagged capitalization+ total bond lagged capitalization)
I define 60/40 portfolio as 0.6*excess stock return + 0.4 excess bond return for each month.
I find stock/bond inverse sigma as one divided 3 year rolling standard deviation of excess return series. 
I find k unlevered as one divided by the sum of stock inverse sigma and bond inverse sigma
I define weights as k unlevered multiplied by stock/bond inverse sigma.
I find Excess Unlevered RP as lagged weights of stock by 1 period multiplied by excess stock return plus lagged weights of bonds by 1 period multiplied by excess bond return.
we set k such that the annualized volatility of this portfolio matches the ex post realized volatility of the benchmark (the value-weighted market portfolio or the 60/40 portfolio).

I find Excess levered RP as k levered multiplied by lagged stock inverse sigma multiplied by excess stock return plus k levered multiplied by lagged bond inverse sigma multiplied by excess bond return

Then I subset my data to be from the period January 1930 to June 2010, at monthly frequency.



![alt text](https://github.com/rustemshinkaruk/Asset-Allocation-Risk-Parity/blob/master/table1.png)


I replicated the table 2 from the paper Leverage Aversion and Risk Parity" by Cli_ord S. Asness, Andrea Frazzini, and Lasse H. Pedersen (2012, Financial Analysts Journal, Volumne 68, Number 1).

I used monthly data to calculate all statistics that are presented below. I used all sample data that I have in calculations of kurtosis and skewness. To calculate all statistics I used R built in functions: mean(), sd(),skewness(),kurtosis(). Sharpe ratio was calculated as mean(market return-risk free)/sd(market return-risk free). T stats were calculated using function t.test().

The biggest part of discrepancy in the data comes from the fact that in the paper they use period from 1926 to 2010 and I used from 1930 to 2010. Also the difference can stem from the fact that I cleaned the data in the different way comparing to what they did in the paper. 

My Excess returns pretty close match the results in paper. In most cases the difference is in +/- 0.2%.

Volatility is economically negligible in most cases except for Levered Risk Parity portfolio. Mine is higher which can partially be explained by the fact that I used longer sample, and the 4 years that were before 1930 may be more volatile. 

Difference in t-stats and sharpe ratios can be explained by difference in mean and volatility. 

I annualized using the convention where I multiply mean by 12 and standard deviation by square root of 12.
