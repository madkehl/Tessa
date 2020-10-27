# Starbucks recommendation project

The following code attempts to take information about different customers and their offer use habits to provide suggestions on what types of offers certain types of customers are most likely to respond to.

In order to do this we first asses what types of users are most likely to be impacted and then look at overall, what biases exist towards what types of demographic groups, and what the most impactful offers to offer may be.  This project consists of a web app, and a jupyter notebook, as well as this readme.  Methods and technical details and discussion are available in the notebook, while this file is intended as an overview/results summary, and the web app is a visualization of final results.

### Instructions:
[app hosted in Heroku](https://afternoon-gorge-22266.herokuapp.com/)

or

1. The code code to clean and model the data used is hosted in a Jupyter notebook instead of a series of scripts.  This is partially because the notebook provides a sort of 'appendix' to the app, which is rather simple.

2. Run the following command in the app's directory to run your web app.  Since this is a Dash app I believe that the normal port used is 8080 for local machines. By default the app is set to run smoothly with heroku, port 5000
    `python run.py 8080`

3. Go to http://0.0.0.0:8080/ or localhost:8080, depending on your computer



# Folders and files included:

* **app**:
	* **run.py**:  This will use several exports from the Starbucks_full_documentation.ipynb to create a visualization of the final results from that notebook.  
	* **df_combo_format.png**, **diff_df_exp_styler.png**, **diff_df_styler.png**:  These are images of pd.style object created in Starbucks_full_documentation.   They are imported as images because the style objects can't be rendered in Dash, and these are available in their full format in the .ipynb.
* **data**:  
	* **offer_info.csv**: This file contains a matrix linking offer_ids to their prominent characteristics
	* **portfolio.json**:  contains offer information, reward amount, duration and difficulty (from Udacity Data Science Nanodegree)
	* **profile.json**: contains person information (from UDSN) 
	* **transcript.json**: contains information on transactions, time.
  
* **models**: 
	* **Starbucks_full_documentation.ipynb**: This file contains code to clean the data, do initial regression models, and then implement FunkSVD and chi-square
	* **diff_df_exp_sc.csv**, **diff_df_sc.csv**: This contains the difference between observed and expected values for user item matrices, grouped by demographic categories, in a matrix format.  Each file is for a different type of FunkSVD.
	* **output_funksvd.csv**, **output_funksvd.csv**, these contain the u + v matrix stacked upon each other 

# Current Requirements:
dash==1.16.3
dash-bootstrap-components==0.10.7
dash-core-components==1.12.1
dash-html-components==1.1.1
scikit-learn==0.22.2
pandas==1.1.2
numpy==1.18.1
plotly==4.11.0
statsmodels==0.8.0
seaborn==0.8.1
matplotlib==2.1.2
jsonschema==2.6.0
gunicorn==19.10.0
scipy==1.3.2

# Results:
  
Unique combinations were found associated with each demographic group. Discounts were more effective with people who were younger, lower income, and/or male.  Older, higher income people were overrepresented in bogo orders.

# Notes:

There were several complexities of this analysis worth discussing (some are further elaborated in the notebook).  First of all, there was the challenge of determining offer impact, for which we used the ratio of reward used to money spent. Additionally, we made no attempt to account for all the possible interaction effects generated by this demographic data which is a major weakness of this analysis. If one specific population of interest it would be worth putting these to more rigorous statistical analyses. Finally, we were unable to find a suitable configuration of the standard FunkSVD algorithm that was able to perform well against a test set.  For this reason we include two iterations of the algorithm, one optimized with a test set but a high MSE (~ 300), and one that is likely overfit.  We place greater confidence in results shared by these two iterations.

# Discussion:

Our application of a chi sq emphasizes differences in population and allowed us to produce unique profiles for each demographic group of interest, except gender otherwise specified, which had very small effect sizes (perhaps because of being underrepresented). We found that women were the demographic group most likely to be impacted by discounts and small rewards, while men were most likely to use high rewards that last a long time and have high difficulty (although this may be related to high difficulty rewards are likely to have higher value).  The age range 25 to 40 and being in income group 2 or 3 (making > 40k a year) were most likely to be impacted by bogo rewards. Income group 3 (> 75k) was most likely to be impacted by mobile rewards of mid difficulty (in addition to bogo). 



# Contact: 

Madeline Kehl (mad.kehl@gmail.com)

# Acknowledgements:

* Udacity Data Science Nanodegree
* Starbucks


# MIT License

Copyright (c) 2020 Madeline Kehl

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
