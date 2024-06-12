# NYBG IMAGE CLASSIFIER🌱
For my Break Through Tech AI Spring AI Studio project, we partnered with New York Botanical Garden to create an Image Classifier to correctly identify and sort the XXX number of specimens into the 10 image classes. 
## 10 Image classes
- Biocultural Specimens: Human made objects; brooms, carpets, etc.
- sme
- qsk
- nas
- am
- mkqs

Our most accurate model lies in the 'epoch.ipynb' file. We achieved an accuracy score over 90% and utilized a Tensorflow Xception Model. This competition was sourced through kaggle and you can find my team's submission here: https://www.kaggle.com/competitions/bttai-nybg-2024/overview

## **Our Objectives:**
- [ ] Exploratory Data Analysis
- [ ] Data Cleaning
- [ ] Model Creation
- [ ] Hyperparameter Tuning
- [ ] Performance Comparison

> [!NOTE]
> Our data contains 28022 rows and 50 columns.


## **EDA**
When first looking at our data, you can see that there are a lot of object-type columns with information like the title of the place, reviews (comments), host info, etc. You could use *NLP sentiment 
analysis* in the future to do rating predictions; more positive buzzwords would contribute to a higher predicted rating.

I did look at the 'host_total_listings_count' column for how many unique values there were(to gauge the variance and decide whether it would be as influential). I did this cause if there are hosts with more listings, 
they would probably have higher ratings since they're more successful.
I also looked at the 'host_location' column and found 1,364 unique values (variations on the NYC area) but, I found the 'neighbourhood_group_cleansed' column was the 5 boroughs of NYC so that played into the decision
of choosing whether to drop that column or not.

- [X] Exploratory Data Analysis
- [ ] Data Cleaning
- [ ] Model Creation
- [ ] Hyperparameter Tuning
- [ ] Performance Comparison
