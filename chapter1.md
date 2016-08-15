---
title       : Correlation
description : This module covers correlations in a fun and interactive way.
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

--- type:MultipleChoiceExercise lang:r xp:50 key:88006d35f5
## What Are Correlations All About?

Correlations are essentially about the relationship between **variables**, in particular, about how the value of one variable changes when the value of another variable changes.

Correlations could be considered for variables of various **[levels of measurement](http://onlinestatbook.com/2/introduction/levels_of_measurement.html)**, even though it is more common to compute correlation between two **continuous** variables. For example, I am interested in the speed I run and my heart rate. In this case, both variables are **ratio**. In another case, I could be also interested in whether my heart rate differs when taking different courses (e.g., Stats, Math, and Pokémon Training). Here, the second variable besides my heart rate is **nominal** or **categorical**. We will have different statistical techniques to measure correlations in different cases. 

A **correlation coefficient** is a numerical index that reflects the relationship between two variables. The value of this descriptive statistic ranges from -1 to +1. When the coefficient is > 0, the correlation is called a **positive** or **direct** correlation; when it is < 0, the correlation is called a **negative** or **indirect** correlation. *Note*: In this case, positive does not mean good and negative does not mean bad. 

Case analysis: The less money you owe to a bank, the less interest you will pay. Is this a positive or negative correlation, or neither?

*** =instructions
- Positive
- Negative
- Neither

*** =hint
Here's a hint: Ask your former stats teacher, or discuss with anyone around you :)

*** =pre_exercise_code
```{r}
# no pec
```

*** =sct
```{r}
msg1 = "Try again!"
msg2 = "Well done. Proceed to the next page"
test_mc(correct = 1, feedback_msgs = c(msg2,msg1))
```

--- type:MultipleChoiceExercise lang:r xp:50 key:03bc384381
## The Scatterplot

A picture is worth a thousand words. Before diving into correlation coefficients, it is usually very helpful to visualize the data. For two continuous variables, we use a **scatterplot** to inspect their relationship. Consider the following three scatterplots. Which scatterplot shows a weak or neglectable correlation?

![](https://upload.wikimedia.org/wikipedia/commons/3/3c/Strong--weak--no-correlation.png)

*** =instructions
- 1
- 2
- 3

*** =hint
Here's a hint: Use your intuition.

*** =pre_exercise_code
```{r}
# no pec
```

*** =sct
```{r}
msg1 = "Try again!"
msg2 = "Not quite, give it another shot."
msg3 = "Well done. Proceed to the next page"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3))
```

--- type:NormalExercise lang:r xp:100 key:683b30e66f
## Let's make a Scatterplot!

Below are several additional examples of scatterplots, with underlying correlations illustrated as well. 

- A coefficient of 1 and -1 means a perfect correlation
- A coefficient of 0 means no correlation
- A strong correlation, with an absolute value >.60, would show a more *tightly* scattered points

![](https://upload.wikimedia.org/wikipedia/commons/0/02/Correlation_examples.png)

Now, let's try to make a scatterplot using `R`, a popular statistical language you should learn! A small dataset you have contains two varialbles:

- `years`: Years of teaching experience
- `outcomes`: A (fictional) score of their teaching performance

*** =instructions
- To make a scatterplot, you just need to type this line in the R console: `plot(data$years, data$outcomes)`

*** =hint
Image `data` is a spreadsheet containing two columns -- `years` and `outcomes`.

*** =pre_exercise_code
```{r}
# Read data
data = data.frame(years = c(1,9,1,4,3,3,7,9,7,6,6,1), outcomes = c(2,8,3,6,6,7,9,8,5,6,7,4))
print(data)
```

*** =sample_code
```{r}
# Plot the data file
plot(data$years, data$outcomes)
```

*** =solution
```{r}
# Plot it
plot(data$years, data$outcomes)
```

*** =sct
```{r}
test_error()
test_object("x",
            incorrect_msg = "Have you correctly plotted the data!")
success_msg("Good job! Head over to the next exercise")
```

--- type:NormalExercise lang:r xp:100 key:c986ddf834
## Check this lesson

http://varianceexplained.org/RData/lessons/lesson3/segment2/


--- type:VideoExercise xp:50 key:ac82ca6647
## Correlation vs. Causation (Part 1)

*** =video_link
//player.vimeo.com/video/115188874

--- type:VideoExercise xp:50 key:d0e2534974
## Correlation vs. Causation (Part 2)

*** =video_link
//player.vimeo.com/video/115124741


--- type:MultipleChoiceExercise lang:r xp:50 key:faf1fc56ca
## Correlation vs. Linearity

> The Pearson correlation coefficient indicates the strength of a linear relationship between two variables, but its value generally does not completely characterize their relationship.

Consider the following diagram. Four datasets corresponding to the scatterplots have the same correlation of 0.816, but the distribution of the variables is very different.

![](https://upload.wikimedia.org/wikipedia/commons/e/ec/Anscombe%27s_quartet_3.svg)

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:21afc4de08
## A really bad movie

Have a look at the plot that showed up in the viewer to the right. Which type of movie has the worst rating assigned to it?

*** =instructions
- Adventure
- Action
- Animation
- Comedy

*** =hint
Have a look at the plot. Which color does the point with the lowest rating have?

*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

movies <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")

library(ggplot2)

ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be a very bad action movie in the dataset."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:6d2be4c7f1
## More movies

In the previous exercise, you saw a dataset about movies. In this exercise, we'll have a look at yet another dataset about movies!

A dataset with a selection of movies, `movie_selection`, is available in the workspace.

*** =instructions
- Check out the structure of `movie_selection`.
- Select movies with a rating of 5 or higher. Assign the result to `good_movies`.
- Use `plot()` to  plot `good_movies$Run` on the x-axis, `good_movies$Rating` on the y-axis and set `col` to `good_movies$Genre`.

*** =hint
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`.

*** =pre_exercise_code
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code

library(MindOnStats)
data(Movies)
movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"),c("Genre", "Rating", "Run")]

# Clean up the environment
rm(Movies)
```

*** =sample_code
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

*** =solution
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```
