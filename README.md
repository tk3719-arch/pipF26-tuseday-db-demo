# Used car prices: should the dealer buy this car?

Taeyun Kang. Code and analysis for the regression assignment. The script reproduces every number on the slides.

## What it does

`analysis/car_regression.py`:

1. Splits the 240 cars in `data/used_car_sales.csv` (sold by the dealer in the last year) at random into 70% training (168 cars) and 30% test (72 cars), seed 42.
2. Fits a linear regression (statsmodels OLS) of `Sale_Price` on mileage, age, horsepower, accident and number of owners. Number of owners is not significant (p = 0.87), and dropping it raises adjusted R², so v1 is the model without it.
3. Compares v1 with the baseline (the training-set average price) on the test cars: R² and typical error (RMSE) in dollars, plus a predicted-vs-actual chart.
4. Applies the dealer's rule to the 40 cars in `data/auction_lots.csv`: buy if auction price + $1,500 is below the predicted price, otherwise pass (`should_buy`). It does the same for the baseline rule and reports cars bought, money-losing cars bought, and total profit (`Later_Sale_Price − Auction_Price − 1,500`).

## Run it

```
pip install -r requirements.txt
python analysis/car_regression.py
```

It prints both regression summaries and writes:

| File | Contents |
|---|---|
| `analysis/car_regression_report.md` | every number: coefficients, p-values, adjusted R², test fit, auction results |
| `analysis/car_regression_results.json` | the same numbers, machine-readable |
| `analysis/car_auction_decisions.csv` | each auction lot's predicted price, both decisions and profit |
| `analysis/car_pred_vs_actual.png` | predicted vs actual sale price on the test cars, baseline and v1 |
