# Machine_Learning_Trading_Bot

In this notebook I test two machine learning models (SVC and LogisticRegression) against a hardcoded Simple Moving Average (SMA) trading algorithm. I then experiment with the models to increase their returns.

---

## Technologies

This code was written on Windows 11 running python 3.8.13. It also uses Pandas (Version 1.3.5), Scikit_learn (Version 1.0.2), Numpy (Version 1.21.5 and Matplotlib (Version 3.5.1)

---

## Installation Guide

All required packages can be installed with pip install.

---

## Experiment

This notebook was made to practice developing and improving trading algorithms. Currently, the notebook is set to run an SMA trading strategy. The short moving average is set to 4 and the long moving average is set to 100. The notebook also has a machine learning training dataset comprising 12 months of stock data.

These parameters can be adjusted by altering the variables 'short_window', 'long_window', and the DateOffset in variable 'training_end'.

Originally, the notebook was set with the same moving average windows but had a shorter 3 month training period. Here are the results.


![trading returns](Resources/all_3_month.png)


'Actual Returns' represents what the market did on its own. 'Strategy Returns' represents the hard-coded SMA strategy, 'Model Returns' represents the C-Support Vector Classification model (SVC), and 'LR Model Returns' represents the Logistic Regression (LR) model. This is the baseline performance.


After that I experimented with the training period to try and improve the models' returns. I tried 6 month, 12 month, 24 month, 36 month, and 48 month training windows. The rest of the data went to testing. Here are some results:

![trading returns](Resources/all_6_month.png)
![trading returns](Resources/all_48_month.png)

As demonstrated in the graphs, once the training time started getting too high returns suffered. The 48 month chart also demonstrates an issue that happened with higher training times: The model recommended holding almost all the time and mimic'd the actual returns. The sweet spot in the data set seemed to be about 12-24 months.

Finally, I experimented with different moving average windows. I changed the windows to 50 and 100 or 50 and 200 to mimic a classical 'golden cross' trading strategy. This actually proved hurtful for the base case model, but when I changed the training window I got interesting results, including one of the best runs.

![trading returns](Resources/3_200.png)
![trading returns](Resources/12_200.png)

I suspect the reason this hurts the models is because the models are actually trading on a short time window (the very next stock price). If I tried moving averages measured in hours or tried to get the models predicting over a longer time period this may have worked better.

---

## Conclusion

These were my 2 best runs. One was with a 12 month training and 4/100 (original) moving averages. The second was a 24 month training period with 50/200 moving averages.

![trading returns](Resources/all_12_month.png)
![trading returns](Resources/24_200.png)


Here are the classification reports:

![trading returns](Resources/best_lr_model_12_normal.png)
![trading returns](Resources/best_svc_model_24_200.png)

Interestingly the 24 month training period was an outlier with my SMA experimentation. Usually the longer windows worsened the model. That model is also different because the recall was close to 50/50, as opposed to almost 0% for the negative recall scenario and 90+% for the positive. While both these models produced similar returns, one is SVC and has an accuracy of .52, while the other is LogisticRegression and had an accuracy of .57.

---

## Contributors

Garrett Hernandez -gtkhhz@gmail.com

---

## License

This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, the author or authors
of this software dedicate any and all copyright interest in the
software to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
software under copyright law.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

For more information, please refer to <https://unlicense.org>
