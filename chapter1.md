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

--- type:MultipleChoiceExercise lang:r xp:50
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

--- type:NormalExercise lang:r xp:100
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
To check the data, type `print(data)`.

*** =pre_exercise_code
```{r}
# Read data
data = data.frame(years = c(1,9,1,4,3,3,7,9,7,6,6,1), outcomes = c(2,8,3,6,6,7,9,8,5,6,7,4))
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

--- type:NormalExercise lang:r xp:100
## Correlation Coefficient

Check out how Pearson's correlation coefficient, `r` is calcuated in this [page](http://cnx.org/contents/XgdE-Z55@40.9:XEKQgmhr@12/Correlation-Coefficient-and-Co)

Now, we are going to calculate `r` in R, again, with a line of code. The `cor` value is what you are interested.

*** =instructions
- Using the same dataset we just plotted, type in the following line in the R console: `cor.test(data$years, data$outcomes)`

*** =hint
To check the data, type `print(data)`.

*** =pre_exercise_code
```{r}
# Read data
data = data.frame(years = c(1,9,1,4,3,3,7,9,7,6,6,1), outcomes = c(2,8,3,6,6,7,9,8,5,6,7,4))
```

*** =sample_code
```{r}
# Calculate the r coeffient
```

*** =solution
```{r}
# Calculate the r coeffient
cor.test(data$years, data$outcomes)
```

*** =sct
```{r}
test_error()
test_object("x",
            incorrect_msg = "Have you correctly calculated r!")
success_msg("Good job! Head over to the next exercise")
```

--- type:NormalExercise lang:r xp:100
## To dive a bit deeper...

Check out this [great tutorial](http://varianceexplained.org/RData/lessons/lesson3/segment2/), and play more. 

In this tutorial, the professor used a dataset named `mtcars`. Now, can you plot `mpg` (mile per gallon) and `hp` (horse-power) together using the `plot` function we tried earlier (instead of ggplot2 used by the professor)?

*** =instructions
- Plot `mpg` and `hp`

*** =hint
Use the dollar sign (`$`) to query each variable, e.g., `mtcars$mpg`

*** =pre_exercise_code
```{r}
# Read data
data = data.frame(years = c(1,9,1,4,3,3,7,9,7,6,6,1), outcomes = c(2,8,3,6,6,7,9,8,5,6,7,4))
```

*** =sample_code
```{r}
# Plot mpg and hp in mtcars
```

*** =solution
```{r}
# Plot mpg and hp in mtcars
plot(mtcars$mpg, mtcars$hp)
```

*** =sct
```{r}
test_error()
test_object("x",
            incorrect_msg = "Have you correctly calculated r!")
success_msg("Good job! Head over to the next exercise")
```

--- type:VideoExercise xp:50 key:ac82ca6647
## Extra: Correlation vs. Causation (Part 1)

*** =video_link
//player.vimeo.com/video/115188874

--- type:VideoExercise xp:50 key:d0e2534974
## Extra: Correlation vs. Causation (Part 2)

*** =video_link
//player.vimeo.com/video/115124741


--- type:MultipleChoiceExercise lang:r xp:50 key:faf1fc56ca
## Extra: Correlation vs. Linearity

> The Pearson correlation coefficient indicates the strength of a linear relationship between two variables, but its value generally does not completely characterize their relationship.

Consider the following diagram. Four datasets corresponding to the scatterplots have the same correlation of 0.816, but the distribution of the variables is very different.

![](https://upload.wikimedia.org/wikipedia/commons/e/ec/Anscombe%27s_quartet_3.svg)
