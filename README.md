# This repository may be considered a late submission to the Kaggle competition [Trading At the Close](https://www.kaggle.com/competitions/optiver-trading-at-the-close)   
In this repository you will find progress and work done so far in the **Workspace** directory. You will find the final submission in the (not yet available) **Submission** directory.   
## Workspace   
The **Workspace** directory contains all approaches so far tried or started. The work can be found in **TDA_zone** and **Models** directories.  
## TDA_zone
The **TDA_zone** directory contains attempts to use and understand how one could apply topological data analysis and persistent homology towards this time series problem. The work there is unfinished (although it deserves another pass..).   
## Models   
The **Models** directory has most of the working substance so far. These attempts so far have used XGBoost's classifcation and regression.   
### First Model:
This model is quite simple as it attempts to naively use XGBoost point by point, accross all dates, for each stock (i.e. one regression tree for each stock). Any edge gained in this model is gained from the feature construction and the stacked modelling.   
1) The stacked modelling means that the regression is completed in two steps. First, a classifier is fit which decides whether the target is likely to move up or down. Then, this classifer probability is added as a feature to the regression and trained over a different subset of data.
2) The feature construction includes relative quantities as well as logged quantities.
   
*Important note*: The model is regressig on the change in the target over 60 seconds. Unfortunately, this is not available in the stream of data for submission. In fact, the target lagged by 60 seconds is even included as a feature in this model, which is also not allowed. Eventually, we will have to phase this feature out in future models. This will probably happen in the second of third model.   
### Second Model:   
This model keeps the stacked layering and adds a few new features. However, it has already done away with including the lagged target as a feature (although it is still trying to predict the change in the target, as of now 03/09/2026).   
This model tries to be more sophistacated by recognizing that there are certain periods that may trade differently than others. By using Optuna to decide on parameters such as the number of time bins and their size, we were able to "discover" that most stocks are optimized with two time bins -- one large time bin for early times, and one smaller time bin for the last 30 - 90 seconds or so. Of course, we also use Optuna to find the best tree parameters.   

### Third Model:   
Not yet worked on, howvever the idea will be to use some simple baseline (e.g. the First Model, or c*imbalance_size where c is some optimized constant for each stock) and if that baseline outperforms the Second Model, we use the baseline instead. The idea here is that, the regressor might have a lot of trouble capturing targets that are very volatile, and in those cases, the simple baseline has a chance of doing better. Otherwise, when the Second Model outperforms the baseline, it's likely it outperforms it by a good amount. The empirical question is how much the baseline can outperform the regression trees of the Second Model for volatile targets.
