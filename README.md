Titanic Data Analysis - Final Report
Introduction
I used the Titanic dataset, which has 891 passenger records including survival, class, age, fare, family size, and where they boarded from. The main thing I wanted to understand was what actually affected survival. Was it mostly about being in a higher class, or did things like age and whether someone was traveling with family also matter?

Cleaning Summary
The dataset had a few issues that I needed to fix first.

The Age column had 177 missing values, so I filled them using the median since it’s more reliable when there are outliers. The Cabin column had too many missing values, so I decided to drop it completely. The Embarked column only had 2 missing values, which I filled with the most common value.

There were no duplicate rows. I also capped the Fare column at the 99th percentile to reduce the effect of extreme values, and I fixed some data types so everything would be consistent.

Feature Engineering Summary
To get more useful insights, I created some new features:

class_rank — I remapped Pclass so higher values mean better class (just to make it easier to understand)
family_size — SibSp + Parch + 1 to represent how many people were traveling together
fare_per_person — Fare divided by family_size since tickets could include multiple people
is_alone — a simple flag to show if someone was traveling alone
class_age_interaction — combines class_rank and age to see if age matters differently across classes
Fare_log — applied a log transformation to reduce the skew in fare values
age_group — grouped Age into Child, Teen, Adult, and Senior to make comparisons easier
Key Findings
Class was the biggest factor in survival
From the correlation analysis, class_rank and Fare_log were the strongest predictors (around 0.33-0.34). About 63% of first-class passengers survived, compared to only around 24% in third class. The difference in fares also shows this clearly, since first-class passengers paid much more on average.

Traveling alone made survival less likely
The is_alone feature had a negative correlation with survival (-0.20). People traveling alone were less likely to survive compared to those with family. One possible reason is that families could help each other during evacuation.

Age mattered, but not that much overall
Children had the highest survival rate (around 58%), while seniors had the lowest (about 27%). But for most adults, age didn’t make a big difference. Overall, age had a weak correlation with survival (-0.06), so it wasn’t as important as class or fare.

(Best chart: correlation heatmap — it makes it easy to see that class and fare have the strongest impact.)

What I Would Do Next
If I had more time, I would try building a model to predict survival, probably starting with logistic regression since the data is already clean.

I’d also look more into how sex and class interact, because being female in first class was probably very different from being female in third class. Another thing I’d revisit is the Cabin column — even though a lot of values are missing, the deck information might still be useful.
