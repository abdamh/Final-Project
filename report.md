# Titanic Data Analysis — Capstone Report

---

## Introduction

I used the Titanic dataset which has 891 passenger records covering survival, class, age, fare, family size, and port of embarkation. The main questions I wanted to answer were: what actually determined whether someone survived, and was it really just about being rich or were there other factors like age and family that played a role too?

---

## Cleaning Summary

The dataset had a few problems. Age had 177 missing values — I filled these with the median since the distribution was roughly normal and the median is less sensitive to outliers than the mean. Cabin was almost entirely missing so I dropped it. Embarked had 2 missing values which I filled with the mode. There were no duplicates. I also capped Fare at the 99th percentile to deal with extreme outliers, and fixed some incorrect data types.

---

## Feature Engineering Summary

I created several new columns to make the data more useful:

- **class_rank** — remapped Pclass so higher number = better class, making the direction more intuitive
- **family_size** — SibSp + Parch + 1, to capture the total group size travelling together
- **fare_per_person** — Fare divided by family_size, since group tickets covered multiple people
- **is_alone** — binary flag for solo travellers
- **class_age_interaction** — class_rank multiplied by scaled age, to capture how age effects differed by class
- **Fare_log** — log transform of Fare to reduce the heavy right skew
- **age_group** — Age binned into Child, Teen, Adult, Senior for easier group analysis

---

## Key Findings

**1. Class was the biggest predictor of survival**
The correlation heatmap showed class_rank and Fare_log were the strongest predictors of survival at around 0.33-0.34. 1st class passengers had a survival rate of around 63% vs roughly 24% for 3rd class. The boxplot made this obvious — 1st class median fare was ~£60 while 3rd class was ~£8, and that gap basically maps directly onto survival chances.

**2. Travelling alone was a disadvantage**
is_alone had a negative correlation with survival (-0.20). Solo travellers survived at a lower rate than passengers with family. This might be because families actively helped each other get to lifeboats, while solo passengers had to navigate the chaos on their own.

**3. Age mattered but only at the extremes**
The groupby summary showed children had the highest survival rate at 58% and seniors the lowest at 27%. But for everyone in between the difference was small — Age only correlated with survival at -0.06 overall. The "women and children first" policy clearly helped children, but being an adult didn't really give you an advantage or disadvantage on its own.

*(Best chart: correlation heatmap — shows all relationships at once and makes the class/fare dominance clear)*

---

## What I Would Do Next

If I had more time I'd want to try building an actual classification model to predict survival, probably starting with logistic regression since the features are now clean and encoded. I'd also look more into the interaction between sex and class since being female in 1st class was probably very different from being female in 3rd class. It would also be worth revisiting the Cabin column — even though most values are missing, the deck letter might carry useful information about where passengers were on the ship and how close they were to lifeboats.
