---
title       : Data Types
description : We're going to get an overview, of the different types of variables that there are in R, and how to work with them. 
--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:8a1f23741a

## str

We're going to be using the following dataset for this module. 
Run this code in the console. 

```{r}
library(dslabs)
data(murders)
```

Next, use the function `str` to examine the structure of the murders object. We can see that this object is a data frame with 51 rows and five columns. 

Which of the following best describes the variables represented in this data frame:

*** =instructions
- The 51 states 
- The murder rates for all 50 states and DC 
- The state name, the abbreviation of the state name, the state's region, and the state's population and the total number of murders for 2010.
- `str` shows no relevant information

*** =hint
Check the output that you see with the `str` function.


*** =pre_exercise_code
```{r}
library(dslabs)
str(murders) 
```

*** =sct
```{r}
msg1 = "Try again! Read the question again."
msg2 = "Try again! Read the question carefully."
msg3 = "Well done. Proceed to the next exercise"
msg4 = "Try again! Check what the question is asking for"
test_mc(correct = 3, feedback_msgs = c(msg1,msg2,msg3,msg4))
```
----

--- type:NormalExercise lang:r xp:100 skills:1 key:a481e086d1

## Variable names

In the previous question, we saw the different variables that are a part of this dataset from the output of the `src()` function. The  function `names()` is specifically designed to extract the column names from a data frame. 

*** =instructions
What are the column names used by the murders data frame for the five variables?

*** =hint
Make sure you put the name of the dataset - `murders` - in parenthesis after names. 

*** =pre_exercise_code
```{r}
library(dslabs)
data(murders)
```

*** =sample_code
```{r}
# Load package and data

library(dslabs)
data(murders)

# Checking the column names 

```

*** =solution
```{r}
# Load package and data

library(dslabs)
data(murders)

# Checking the column names 
names(murders)
```

*** =sct
```{r}
test_error()
test_function("names", incorrect_msg = "Make sure you've put in the name of the dataset.") 
success_msg("Good job!")
```
----

--- type:NormalExercise lang:r xp:100 skills:1 key:e22e8e58ef
## Examining variables

In this module we have learned that every variable has a class. For example, the class can be character, numeric or logical. The function `class()` can be used to determine the class of an object.

Here we are going to determine the class of one of the variables in the murders data frame. To extract a variables from a data frame we use `$`, referred to as the accessor.

In the editor we show an example of how to do this. Let`s try it out for ourselves. 

*** =instructions
Use the accessor `$` to extract the state abbreviations and assign them to the object `a`. What is the class of this object?

*** =hint
Remember to assign the state abbreviations to the object `a`. 

*** =pre_exercise_code
```{r}
library(dslabs)
data(murders)
```

*** =sample_code
```{r}
# To access the population variable from the murers dataset use this code:
p <- murders$population 

# To determine the class of object `p` we use this code:
class(p)

# Use the accessor to extract state abbreviations and assign it to `a`

# Determine the class of `a`

```

*** =solution
```{r}
# To access the population variable from the murers dataset use this code:
m <- murders$population 

# To determine the class of object `m` we use this code:
class(m)

# Use the accessor to extract state abbreviations and assign it to `a`
a <- murders$abb 

# Determine the class of `a`
class(a)  
```

*** =sct
```{r}
test_error()
test_object ("a", undefined_msg = "You need to define the object `a`.", incorrect_msg = "Make sure to save the variable `abb` in the object `a`.")
test_function("class")
success_msg("That's great! Now, you know what the class of `abb` is. Play around to check the class of the other variables in the dataset!")
```
----


--- type:NormalExercise lang:r xp:100 skills:1 key:f9207929f3
## More than one way to access variables 

An important lesson you should learn early is that there are multiple ways of doing things in R. For example, to generate the first five integeers we note that `1:5`, and `seq(1,5)` return the same result. 

There are also other ways to variables from a data frame. For example we can use the square brackets `[[`
instead of the accessor `$`. Example code is included in the editor.

*** =instructions
Use the square brackets `[[` to extract the state abbreviations and assign them to the object `b`. Then use the identical function to determine if `a`, as defined in the previous exercises, and `b` are the same.

*** =hint
You need to use 2 sets of square brackets. 

*** =pre_exercise_code
```{r}
library(dslabs)
data(murders)
a <- murders$abb 
```

*** =sample_code
```{r}
# We extract the population like this:
p <- murders$population

# This is how we do the same with the square brackets:
o <- murders[["population"]] 

# We can confirm these two are the same
identical(o, p)

# Use square brackets to extract `abb` from `murders` and assign it to `b`

# Check if `a` and `b` are identical 

```

*** =solution
```{r}
# We extract the population like this:
p <- murders$population

# This is how we do the same with the square brackets:
o <- murders[["population"]] 

# We can confirm these two are the same
identical(o, p)

# Use square brackets to extract `abb` from `murders` and assign it to 
b <- murders[["abb"]]

# Check if `a` and `b` are identical 
identical(a,b)
```

*** =sct
```{r}
test_error()
test_object ("b", undefined_msg = "You need to define the object `b`.", incorrect_msg = "Make sure to save the variable `abb` in the object `b`.")
test_function("identical")
success_msg("You've now learned different ways of doing the same thing in R! You're making great progress!")
```
----

--- type:NormalExercise lang:r xp:100 skills:1 key:e3211138bb
## Factors

Using the `str()` command, we saw that the region column stores a factor. You can corroborate this by using the `class` command for region. 

The function `levels` shows us the categories included in the factor. 

*** =instructions

With one line of code, use the function `levels` and `length` to determine the number of regions defined by this dataset. 


*** =hint
Make sure you're using both commands - `length` and `levels`, to get the number of regions.  

*** =pre_exercise_code
```{r}
library(dslabs)
data(murders)

```

*** =sample_code
```{r}
# We can see the class of the region variable using class
class(murders$region)

# Determine the number of regions included in this variable 

```

*** =solution
```{r}
# We can see the class of the region variable using class
class(murders$region)

# Determine the number of regions included in this variable 
length(levels(murders$region))

```

*** =sct
```{r}
test_error()
test_output_contains("length(levels(murders$region))", incorrect_msg = "Run the code mentioned in the instructions exactly as is!")
success_msg("Good job!")

```
----

--- type:NormalExercise lang:r xp:100 skills:1 key:c79e23df50
## Tables

The function table takes a vector as input and returns the frequency of each unique element in the vector. 

*** =instructions

Use this function in one line of code to create a table showing the number of states per region.

*** =hint
Extract the variable region from the murders dataset and then use the `table` function to create the table. 

*** =pre_exercise_code
```{r}
library(dslabs)
data(murders)
```

*** =sample_code
```{r}
# Here is an example of what the table function does
x <- c("a", "a", "b", "b", "b", "c")
table(x)

# Write one line of code to show the number of states per region

```

*** =solution
```{r}
# Here is an example of what the table function does
x <- c("a", "a", "b", "b", "b", "c")
table(x)

# Write one line of code to show the number of states per region
table(murders$region)

```

*** =sct
```{r}
test_error()
test_function("table", incorrect_msg = "Make sure you extract the variable region from the dataset.")
success_msg("You got this! Now you're a pro at making tables in R!")

```
----

--- type:VideoExercise lang:r aspect_ratio:0 xp:0 skills:0 key:011b43bb92


## End of Section

This is the end of the programming assignment for this section.

You can now close this window to go back to the <a href='https://courses.edx.org/courses/course-v1:HarvardX+PH125.1x+2T2017/courseware/cfded5c208bc4e379606cb712cc54f25/5ba06674d0be41b99185b947e09e889b/?child=first'>course</a>.

If you want to continue the assessments without watching the videos, you can click on the arrow above to get the next exercise or hit Ctrl-K.

----