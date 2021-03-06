---
title       : Basic Data Manipulation 
description : Just as the name suggests, we're going to practice the basics of data manipulation here.
--- type:NormalExercise lang:r xp:100 skills:1 key:fa7b6092fb

## dplyr

Load the `dplyr` package and the murders dataset.

```{r}
library(dplyr)
library(dslabs)
data(murders)
```

*** =instructions

Use the function `mutate` to add a murders rate column with the per 100,000 murder rate.

*** =hint
Use code `murders <- mutate(murders, rate =  total / population * 100000)`. 

*** =pre_exercise_code
```{r}
library(dplyr)
library(dslabs)
data(murders)
```

*** =sample_code
```{r}
# Loading the libraries
library(dplyr)
data(murders)

# Use mutate to add a column named rate and store in murders

```

*** =solution
```{r}
# Use mutate to add a rate column and store in `murders`
murders <- mutate(murders, rate =  total / population * 100000)
```

*** =sct
```{r}
test_error()
test_object("murders", undefined_msg = "Define murder first.", incorrect_msg = "Check the code again.")
success_msg("Awesome! Let's learn another command with mutate.")
```
----

--- type:NormalExercise lang:r xp:100 skills:1 key:545fbadeea
## Mutate 


*** =instructions
Use the function `mutate` again to add a column `rank` containing the rank, from highest to lowest murder rate. Note that if `rank(x)` gives you the ranks of `x` from lowest to highest, `rank(-x)` gives you the ranks from highest to lowest.

*** =hint
Use the function rank and remember by default it ranks form lowest to highest.

*** =pre_exercise_code
```{r}
library(dplyr)
library(dslabs)
data(murders)
rate =  murders$total)/ (murders$population) * 100000
```

*** =sample_code
```{r}
# Loading the libraries
library(dplyr)
data(murders)

# Defining rate
rate <-  murders$total/ murders$population * 100000

# Use mutate to add a rate column, rank from highest to lowest and store in `murders`

```

*** =solution
```{r}

# Use mutate to add a rate column, rank from highest to lowest and store in `murders`
murders <- mutate(murders, rank = rank(-rate))
```

*** =sct
```{r}
test_error()
test_object("murders", incorrect_msg = "Remember, rank from highest to lowest.")
success_msg("Good job!")
```
----
--- type:NormalExercise lang:r xp:100 skills:1 key:555ca41873
## filter 


*** =instructions

The `dplyr` function `filter` is used to select specific rows of the data frame to keep. Show the top 5 states with the highest murder rates. Do not change the murders dataset, just show the result.

*** =hint


*** =pre_exercise_code
```{r}
library(dplyr)
library(dslabs)
data(murders)

```

*** =sample_code
```{r}
# Loading the libraries
library(dplyr)
data(murders)

# Add the necessary columns
murders <- mutate(murders, rate = total/population * 100000, rank = rank(-rate))

# Filter to show the top 5 states with the highest murder rates

```

*** =solution
```{r}
# Loading the libraries
library(dplyr)
data(murders)

# Add the necessary columns
murders <- mutate(murders, rate = total/population * 100000, rank = rank(-rate))

# Filter to show the top 5 states with the highest murder rates
filter(murders, rank <= 5)
```

*** =sct
```{r}
test_error()
test_output_contains("filter(murders, rank <= 5)", incorrect_msg = "Make sure you've written murders in your code.")
success_msg("Great job!")
```
----

--- type:NormalExercise lang:r xp:100 skills:1 key:42352c70c5
## filter with !=

*** =instructions
Create a new data frame called `no_south` that removes states from the south. How many states are in this category? 

*** =hint
Use filter and the != operator. You can use nrow to quickly get the number of rows of a data frame.

*** =pre_exercise_code
```{r}
library(dplyr)
library(dslabs)
data(murders)
```

*** =sample_code
```{r}
# Loading the libraries
library(dplyr)
data(murders)

# Use filter Creat a new dataframe `no_south`

# Use nrow() to calculate the number of rows
```

*** =solution
```{r}
# Creating a new dataframe `no_south`
no_south <- filter(murders, region != "South" )

# Number of states (rows) in this category 
nrow(no_south)
```

*** =sct
```{r}
test_error()
test_object("no_south", undefined_msg = "Define no_south first!", incorrect_msg = "Make sure you`re excluding the ones not in the South.")
test_output_contains("nrow(no_south)", incorrect_msg = "You need the number of rows for the number of states.")
success_msg("That's great! Let's move to the next exercise.")
```
----

--- type:NormalExercise lang:r xp:100 skills:1 key:18111c7bfd
## filter with %in%


*** =instructions
Create a new dataframe called murders_nw with only the states from the northeast and the west. 
How many states are in this category? 


*** =hint
Use filter and the `%in%` operator. You can use nrow to quickly get the number of rows of a data frame.

*** =pre_exercise_code
```{r}
library(dplyr)
libary(dslabs)
data(murders)
```

*** =sample_code
```{r}
# Loading the libraries
library(dplyr)
data(murders)

# Create a new dataframe called `murders_nw` with only the states from the northeast and the west


# Number of states (rows) in this category 

```

*** =solution
```{r}
# Create a new dataframe called `murders_nw` with only the states from the northeast and the west
murders_nw <- filter(murders, region %in% c("Northeast", "West") )

# Number of states (rows) in this category
nrow(murders_nw)
```

*** =sct
```{r}
test_error()
test_object("murders_nw", undefined_msg = "Define murders_nw first.", incorrect_msg = "Make sure you're using the %in% command.")
test_output_contains("nrow(murders_nw)", incorrect_msg = "You need the number of rows again, same as previous question.")
success_msg("This is great!")
```
----


--- type:NormalExercise lang:r xp:100 skills:1 key:e572c8806a
## filtering by two conditions 

*** =instructions
Suppose you want to live in the Northeast or West and want the murder rate to be less than 1. 
Create a table, call it `my_states`, that satisfies both these. 
How many states satisfy this?

*** =hint
Use the `my_states <- filter(murders, region %in% c("Northeast", "West") & rate < 1)` code. 

*** =pre_exercise_code
```{r}
library(dplyr)
library(dslabs)
data(murders)
```

*** =sample_code
```{r}
# Loading the libraries
library(dplyr)
data(murders)

# add the rate column
murders <- mutate(murders, rate =  total / population * 100000)

# Create a table, call it my_states, that satisfies both the conditions 

# Number of states (rows) in this category


```

*** =solution
```{r}
# Create a table, call it `my_states`, that satisfies both the conditions 
my_states <- filter(murders, region %in% c("Northeast", "West") & rate < 1)

# Number of states (rows) in this category
nrow(my_states)
```

*** =sct
```{r}
test_error()
test_object("my_states", undefined_msg = "Define my_states first!", incorrect_msg = "Use the filter, %in% and < commands.")
test_output_contains("nrow(my_states)", incorrect_msg = "You need the number of rows again, same as previous question.")
success_msg("Now you know how to combine functions and use them to get specific answers. Let's try it one more time!")
```
----

--- type:NormalExercise lang:r xp:100 skills:1 key:3d4de3a34a
## Using the pipe %>%

*** =instructions
Repeat exercise 5, but now instead of creating a new obejct, show the result and only include the state, rate, and rank columns. Use a pipe (`%>%`) to do this in just one line.

*** =hint
Use code: `filter(murders, region %in% c("Northeast", "West") & rate < 1) %>% 
    select(state, rate, rank)` 
    
*** =pre_exercise_code
```{r}
library(dplyr)
library(dslabs)
data(murders)
rate =  (murders$total)/ (murders$population) * 100000
```

*** =sample_code
```{r}
## Define the rate column
murders <- mutate(murders, rate =  total / population * 100000, rank = rank(-rate))

# show the result and only include the state, rate, and rank columns, all in one line
```
*** =solution
```{r}
## Define the rate and rank column
murders <- mutate(murders, rate =  total / population * 100000, rank = rank(-rate))

# show the result and only include the state, rate, and rank columns, all in one line
filter(murders, region %in% c("Northeast", "West") & rate < 1) %>%  
   select(state, rate, rank)
```
*** =sct
```{r}
test_error()
test_function("filter", incorrect_msg = "Everything needs to be in one line! Use a pipe to help!")
success_msg("You're getting a pretty good hang of stuff now!")
```
----
--- type:NormalExercise lang:r xp:100 skills:1 key:1b45c7acac
## mutate, filter and select  



*** =instructions
Now reload the original murders data frame using `data(murders)`. Then use just one line to create a new data frame, called, `my_states` that has murder rate and rank column, consideres only states in the Northeast or West, has a murder rate lower than 1 and contains only the state, rate, and rank columns. 

*** =hint
Use `mutate`, `filter` and `select` combining them with `pipes`.

*** =pre_exercise_code
```{r}
library(dplyr)
library(dslabs)
data(murders)
```

*** =sample_code
```{r}
# Loading the libraries
library(dplyr)
data(murders)

# Create new data frame called `my_states` (with specifications in the instructions)


```

*** =solution
```{r}
# Create new data frame called `my_states` (with specifications in the instructions)
my_states <- murders %>% 
    mutate(rate =  total / population * 100000, rank = rank(-rate)) %>%
    filter(region %in% c("Northeast", "West") & rate < 1) %>%
    select(state, rate, rank)
```

*** =sct
```{r}
test_error()
test_object("my_states", undefined_msg = "Define my_states!", incorrect_msg = "Make sure you put pipes to put everything in one line.")
success_msg("This is absolutely awesome! You now know how to use basic data manipulation techniques in R.")
```

----

--- type:VideoExercise lang:r aspect_ratio:0 xp:0 skills:0 key:011b43bb92


## End of Section

This is the end of the programming assignment for this section.

You can now close this window to go back to the <a href='https://courses.edx.org/courses/course-v1:HarvardX+PH125.1x+2T2017/courseware/cfded5c208bc4e379606cb712cc54f25/5ba06674d0be41b99185b947e09e889b/?child=first'>course</a>.

If you want to continue the assessments without watching the videos, you can click on the arrow above to get the next exercise or hit Ctrl-K.

----