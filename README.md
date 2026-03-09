# This repository may be considered a late submission to the Kaggle competition [Trading At the Close](https://www.kaggle.com/competitions/optiver-trading-at-the-close)   
In this repository you will find progress and work done so far in the **Workspace** directory. You will find the final submission in the (not yet available) **Submission** directory.   
## Workspace   
The **Workspace** directory contains all approaches so far tried or started. The work can be found in *TDA_zone* and *Models* directories.  
## TDA_zone
The *TDA_zone* directory contains attempts to use and understand how one could apply topological data analysis and persistent homology towards this time series problem. The work there is unfinished (although it deserves another pass..).   
## Models   
The *Models* directory has most of the working substance so far. These attempts so far have used XGBoost's classifcation and regression.   
### First Model:
This model is quite simple as it attempts to naively use XGBoost point by point, accross all stocks and dates. Any edge gained in this model is gained from the feature construction and the stacked modelling.   
1) The stacked modelling means that the regression is completed in two steps. First, a classifier is fit which decides whether the target is likely to move up or down. Then, this classifer probability is added as a feature to the regression and traine dover a different subset of data.
2) The feature construction includes relative quantities as well as logged quantities.
   
**Important note**: The model is regressig on the change in the target over 60 seconds. Unfortunately, this is not available in the stream of data for submission. Eventually, we will have to phase this feature out in future models. This will probably happen in the second of third model.   
### Second Model:   
