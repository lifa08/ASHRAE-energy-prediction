# ![ASHRAE-energy-prediction](demo_dataclean.png)

# ASHRAE-energy-prediction

The code in this repository is for [Kaggle competition ashrae energy prediction](https://www.kaggle.com/c/ashrae-energy-prediction). I am still improving the code, so the resulting public score from this code might not be attractive enough yet :D

## Technologies
* Jupyter Notebook
* Pandas
* Numpy
* AWS Sagemaker
* lightGBM
* xgboost

## To do
* Construct different feature sets for different sites
* Train different models for different sites

## Descriptions of files

[ashrae_data_preparation.ipynb](ashrae_data_preparation.ipynb)

* Prepare data locally for training in AWS
* Output files can then be uploaded mannually to S3 for training

[ashrae_lightGBM.ipynb](ashrae_lightGBM.ipynb)

* Borrowed from [this Kaggle notebook](https://www.kaggle.com/aitude/ashrae-kfold-lightgbm-without-leak-1-08/comments)
* Starting point notebook
* Clean data very lightly
* Fill missing weather information with relevant mean value of the day of the month
* Use KFold lightGBM model
* The Kaggle public score was 2.227.

[ashrae_lightGBM_with_data_cleaned.ipynb](ashrae_lightGBM_with_data_cleaned.ipynb)
* Use data where outliers are removed more thoroughly
* Fill missing weather information with interpolate within a site
* Use KFold lightGBM model
* The Kaggle public score was 1.139.

_Note: we can see the magic of cleaning data from this example_

[ashrae_outliers_deletion.ipynb](ashrae_outliers_deletion.ipynb)
* Remove outliers site by site, building by building
* Removes about 4% rows of data

[ashrae_outliers_deletion_verbose.ipynb](ashrae_outliers_deletion_verbose.ipynb)
* verbose version of [ashrae_outliers_deletion.ipynb](ashrae_outliers_deletion.ipynb)
* Include plots that display data before and after deleting outliers
* The plots alone explain clearly why certain data are considered as outliers and need to be deleted

### [ashrae_aws](ashrae_aws/) - AWS Sagemaker notebooks

[data_preparation.ipynb](ashrae_aws/data_preparation.ipynb)
* Prepare data in AWS
* Write the output files to S3

[xgboost_train.ipynb](ashrae_aws/xgboost_train.ipynb)
* Train a model with AWS built-in xgboost algorithm

_Note: the model was trained with only 6 rounds due to the lack of mememory. I once trained it untill 28 rounds when the validation stops improving. But model trained with 28 rounds wasn't deplolyed successfully due to lack of mememory eventhough I have already created two support cases to ask for more resources (instances with more mememory). I stop trying more powerful instances when the bills went up :D._

[xgboost_prediction.ipynb](ashrae_aws/xgboost_prediction.ipynb)
* Use the trained xgboost model to predict
