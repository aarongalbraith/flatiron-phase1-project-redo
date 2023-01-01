# Aaron Galbraith Flatiron Data Science Phase 1 Project

## Overview

<< DO LAST >>

## Business Understanding

The first question to answer is what constitutes a successful movie. In the end, we used both **profit** and **ROI**.

Profit and ROI tell different stories. If one type of project has a high average ROI, then it may be more reliable and thus preferable to a certain type of investor. But if this type of high-ROI project is typically done on a small budget, then it doesn't guarantee a very big profit and may not therefore be worth the studio's time.

On the other hand, if a type of project has a high average profit, then it is more likely to pay off handsomely, assuming it does pay off.

We considered but dismissed alternate metrics. One was viewership share. It's possible that Microsoft would want to prioritize long-term brand awareness and viewer loyalty (perhaps even subscriptions to a streaming platform) at the potential expense of short-term profits. To explore this, we would need to make deeper comparisons involving how many people are viewing each movie, which would require better data than we have access to, and which might not ultimately be relevant, depending on Microsoft's specific goals.

The second question to answer is *what* we should attribute the success (defined above) of a movie *to*. Within the constraints of the data and with a focus on what elements Microsoft could control, we chose to isolate the variables of running time, genre, MPAA rating, and the profit and ROI history of both the director and lead actor(s).

## Data Understanding

The available data comes from 5 families of resources. By far the richest of these resources is IMDb. IMDb has records for the most movies of any of the resources, and it has data on running time, genre, director and cast, all of which was ultimately relevant to our exploration.

The next most useful resource was The Numbers, which provided necessary data on movie grosses and budgets, from which we calculated profit and ROI. No other resource had any budget information at all, so each aspect of our analysis was necessarily limited to the 5,782 records from The Numbers.

The data from the original Rotten Tomatoes files was unusable since it none of the records included any titles. We replaced these with other Rotten Tomatoes records sourced from Kaggle, which were very rich indeed and actually provided more usable records than IMDb, given that records needed to overlap with those from The Numbers in order to be usable. The Rotten Tomatoes records included data on running time, genre, MPAA rating, and directors.

The other two resource families proved unusable because their data was redundant and less extensive than others. Box Office Mojo had incomplete data on box office grosses but no data on budgets. The Movie Data Base would have only added information on "popularity", which, upon further investigation, seems to have been defined in a very loose way that we cannot concretely relate to profit or ROI.

## Data Analysis

### Runtime

We analyzed runtime by (1) removing outliers (more than 2 standard deviations, for both runtime and profit), (2) by cutting the data into 15 equally-sized percentile bins for runtime, and (3) plotting those bins against profit and ROI.

![runtime v. profit and runtime v. ROI](images/im01.jpg)

The results show that profit generally increases with runtime and ROI generally decreases with runtime.

What this means for Microsoft depends on their goals and level of risk aversion. If they want to gun for big profits, the results suggest they should make longer movies. If they want reliable returns, they should make shorter movies (perhaps more of them).

### Genre

In order to analyze the effect of genre, it was necessary and took some effort to isolate single genres, as IMDb listed multiple genres in the majority of its records. After teasing the genres apart, it became quite clear that some were more profitable than others, namely the horror and mystery genres.

![genre v. ROI](images/image02.jpg)

The matter of quantifying a director's experience required more feature creation than the other criteria did. To do this, we looked at movies from 2015-2018 (inclusive). Then, for the director of each movie, we calculated two quantities: (1) the **sum** of the budgets of the movies he or she had directed in the previous 5 years, and (2) the **average** ROI of the movies he or she had directed in the previous 5 years. Further, we performed this analysis three times, considering (1) all directors and all movies, (2) all directors and only movies with a budget greater than $1 million, and (3) only movies and directors of movies with a budget greater than $1 million. In all cases, the correlation showed that a director's experience has little to no effect on a movie's ROI.

![director budget experience v. ROI](images/image03.jpg)
![director ROI experience v. ROI](images/image04.jpg)

In the language of statistical testing, this result would be known as "accepting the null hypothesis", where the "null hypothesis" is that there is **no** correlation between two phenomena. Such results are often overlooked, but they can often be just as illuminating as positive results, especially when they tend to contradict conventional wisdom, as we believe it does in this case.

## Conclusion

1. Produce a movie roughly 80-85 minutes in length
2. Produce a movie in the horror or mystery genre
3. Assign a director without concern for the director's previous experience
