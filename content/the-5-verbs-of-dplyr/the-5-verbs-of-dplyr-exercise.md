Exercise - The 5 verbs of dplyr
================
Ben

# Getting started

As always, the first thing we will do is load the tidyverse.

*Note: If you haven’t yet installed the tidyverse, you’ll first have to
run the code install.packages(“tidyverse”).*

``` r
library(tidyverse)
```

Here’s the dataframe that we’ll analyze in this
exercise:

``` r
scores <- data_frame(name = c("mike", "carol", "greg", "marcia", "peter", "jan", "bobby", "cindy", "alice"),
           school = c("south", "south", "south", "south", "north", "north", "north", "south", "south"),
           teacher = c("johnson", "johnson", "johnson", "johnson",  "smith", "smith", "smith", "perry", "perry"),
           gender = c("male", "female", "male", "female", "male", "female", "male", "female", "female"),
           math_score = c(4, 3, 2, 4, 3, 4, 5, 4, 5),
           reading_score = c(1, 5, 2, 4, 5, 4, 1, 5, 4)) 
```

Let’s first take a look at it:

``` r
scores
```

    ## # A tibble: 9 x 6
    ##   name   school teacher gender math_score reading_score
    ##   <chr>  <chr>  <chr>   <chr>       <dbl>         <dbl>
    ## 1 mike   south  johnson male            4             1
    ## 2 carol  south  johnson female          3             5
    ## 3 greg   south  johnson male            2             2
    ## 4 marcia south  johnson female          4             4
    ## 5 peter  north  smith   male            3             5
    ## 6 jan    north  smith   female          4             4
    ## 7 bobby  north  smith   male            5             1
    ## 8 cindy  south  perry   female          4             5
    ## 9 alice  south  perry   female          5             4

Before we get started, I want to make sure you understand the difference
between doing something and assigning it to a new name and just doing it
without naming it. For example, make sure you understand the following:

``` r
# get the first 3 rows
scores %>% 
  slice(1:3)
```

    ## # A tibble: 3 x 6
    ##   name  school teacher gender math_score reading_score
    ##   <chr> <chr>  <chr>   <chr>       <dbl>         <dbl>
    ## 1 mike  south  johnson male            4             1
    ## 2 carol south  johnson female          3             5
    ## 3 greg  south  johnson male            2             2

``` r
# get the first 3 rows, and assign it to a new name "scores_small"
scores_small <- scores %>% 
  slice(1:3)

# see what's in "scores_small"
scores_small
```

    ## # A tibble: 3 x 6
    ##   name  school teacher gender math_score reading_score
    ##   <chr> <chr>  <chr>   <chr>       <dbl>         <dbl>
    ## 1 mike  south  johnson male            4             1
    ## 2 carol south  johnson female          3             5
    ## 3 greg  south  johnson male            2             2

In this exercise we’ll typically just print the results and not save
them, but it’s an option if you want it\!

Now we can get to the exercise. Most sections will begin with an example
for you to look at. When questions require a written answer, there will
be an “Answer” line for you to complete.

# Arrange

## Example

**Question:** Sort the data by math\_score from high to low. Who had the
best math score?

``` r
scores %>% 
  arrange(desc(math_score))
```

    ## # A tibble: 9 x 6
    ##   name   school teacher gender math_score reading_score
    ##   <chr>  <chr>  <chr>   <chr>       <dbl>         <dbl>
    ## 1 bobby  north  smith   male            5             1
    ## 2 alice  south  perry   female          5             4
    ## 3 mike   south  johnson male            4             1
    ## 4 marcia south  johnson female          4             4
    ## 5 jan    north  smith   female          4             4
    ## 6 cindy  south  perry   female          4             5
    ## 7 carol  south  johnson female          3             5
    ## 8 peter  north  smith   male            3             5
    ## 9 greg   south  johnson male            2             2

**Answer:** Bobby and alice both tied for the highest math score

## Q1

**Question:** Sort the data by name from first to last in the alphabet.

## Q2

**Question:** Sort the data by gender so females show up first. Which
gender appears to have better reading scores?

**Answer:**

## Q3

**Question:** Sort the data by school, then teacher, then gender, then
math\_score, and finally by reading\_score.

# Select

## Example

**Question:** Select only the name, math\_score, and reading\_score
columns.

``` r
scores %>% 
  select(name, math_score, reading_score)
```

    ## # A tibble: 9 x 3
    ##   name   math_score reading_score
    ##   <chr>       <dbl>         <dbl>
    ## 1 mike            4             1
    ## 2 carol           3             5
    ## 3 greg            2             2
    ## 4 marcia          4             4
    ## 5 peter           3             5
    ## 6 jan             4             4
    ## 7 bobby           5             1
    ## 8 cindy           4             5
    ## 9 alice           5             4

## Q1

**Question:** Select all of the columns except the gender column.

## Q2

**Question:** Select all of the columns except the math\_score and
reading\_score columns.

## Q3

**Question:** Keep all of the columns but rearrange them so gender is
the first column.

# Filter

## Example

**Question:** Filter to students who are male and went to south.

``` r
# Option 1
scores %>% 
  filter(gender == "male" & school == "south")
```

    ## # A tibble: 2 x 6
    ##   name  school teacher gender math_score reading_score
    ##   <chr> <chr>  <chr>   <chr>       <dbl>         <dbl>
    ## 1 mike  south  johnson male            4             1
    ## 2 greg  south  johnson male            2             2

``` r
# Option 2
scores %>% 
  filter(gender == "male", school == "south")
```

    ## # A tibble: 2 x 6
    ##   name  school teacher gender math_score reading_score
    ##   <chr> <chr>  <chr>   <chr>       <dbl>         <dbl>
    ## 1 mike  south  johnson male            4             1
    ## 2 greg  south  johnson male            2             2

## Q1

**Question:** Filter to students who did well in math (you decide what
“well” means).

## Q2

**Question:** Use filter to figure out how many students had a math
score of 4 or more and a reading score of 3 or more.

**Answer:**

## Q3

**Question:** Explain the errors in each of the following code blocks,
then fix it to make it right\!

``` r
# code block 1
scores %>% 
  filter(school == south)
```

    ## Error in filter_impl(.data, quo): Evaluation error: object 'south' not found.

``` r
# code block 2
scores %>% 
  filter(school = "south")
```

    ## Error: `school` (`school = "south"`) must not be named, do you need `==`?

``` r
# fix it! 
```

**Answer:**

## Q4

**Question:** You are creating a remediation program. Filter to students
who got a 3 or worse in either math or reading.

## Q5

**Question:** Filter to students who got a reading score of 2, 3, or 4.

## Challenge

**Question:** Filter to students who have a name that starts with an
“m”. Hint: type “?substr” in the console and then scroll to the
bottom of the help file to see useful examples.

# Filter with groups

## Example

**Question:** Filter to teachers whose best math student got a score of
5.

``` r
scores %>% 
  group_by(teacher) %>% 
  filter(max(math_score) == 5)
```

    ## # A tibble: 5 x 6
    ## # Groups:   teacher [2]
    ##   name  school teacher gender math_score reading_score
    ##   <chr> <chr>  <chr>   <chr>       <dbl>         <dbl>
    ## 1 peter north  smith   male            3             5
    ## 2 jan   north  smith   female          4             4
    ## 3 bobby north  smith   male            5             1
    ## 4 cindy south  perry   female          4             5
    ## 5 alice south  perry   female          5             4

## Q1

**Question:** Filter to the gender with a mean math score of 4.

## Q2

**Question:** Explain why the following code removes students who have
perry as their teacher.

**Answer:**

# Mutate

## Example

**Question:** Both the math and reading scores were actually out of 50 –
replace both variables to be 10 times their original values.

``` r
scores %>% 
  mutate(math_score =  math_score * 10,
         reading_score = reading_score * 10)
```

    ## # A tibble: 9 x 6
    ##   name   school teacher gender math_score reading_score
    ##   <chr>  <chr>  <chr>   <chr>       <dbl>         <dbl>
    ## 1 mike   south  johnson male           40            10
    ## 2 carol  south  johnson female         30            50
    ## 3 greg   south  johnson male           20            20
    ## 4 marcia south  johnson female         40            40
    ## 5 peter  north  smith   male           30            50
    ## 6 jan    north  smith   female         40            40
    ## 7 bobby  north  smith   male           50            10
    ## 8 cindy  south  perry   female         40            50
    ## 9 alice  south  perry   female         50            40

## Q1

**Question:** Create a new column called “math\_reading\_avg” which is
the average of a students math and reading scores.

## Q2

**Question:** Create a new column “high\_math\_achiever” that is an
indicator of if a student got a 4 or better on their math\_score.

## Q3

**Question:** Create a new column “reading\_score\_centered” that is a
students reading score with the mean of all students’ reading scores
subtracted from it.

## Q4

**Question:** Create a new column “science\_score”. You can make up what
the actual scores are\!

# Mutate with groups

## Q1

**Question:** Mike and cindy both got a 4 for their math score. Explain
why why Mike has a higher “math\_score\_centered\_by\_gender” score.

``` r
scores %>% 
  group_by(gender) %>% 
  mutate(math_score_centered_by_gender = math_score - mean(math_score))
```

    ## # A tibble: 9 x 7
    ## # Groups:   gender [2]
    ##   name   school teacher gender math_score reading_score math_score_center…
    ##   <chr>  <chr>  <chr>   <chr>       <dbl>         <dbl>              <dbl>
    ## 1 mike   south  johnson male            4             1                0.5
    ## 2 carol  south  johnson female          3             5               -1  
    ## 3 greg   south  johnson male            2             2               -1.5
    ## 4 marcia south  johnson female          4             4                0  
    ## 5 peter  north  smith   male            3             5               -0.5
    ## 6 jan    north  smith   female          4             4                0  
    ## 7 bobby  north  smith   male            5             1                1.5
    ## 8 cindy  south  perry   female          4             5                0  
    ## 9 alice  south  perry   female          5             4                1

**Answer:**

## Q2

**Question:** Create a “reading\_score\_centered\_by\_teacher” column.
What can you learn from it?

**Answer:**

## Q3

**Question:** Make a “number\_of\_students\_in\_class” column that is
number of students in a student’s class. For example, it should be 4 for
mike and 3 for peter.

# Summarize

## Example

**Question:** Use the summarize command to find the mean math score for
all students.

``` r
scores %>% 
  summarize(math_score_mean = mean(math_score))
```

    ## # A tibble: 1 x 1
    ##   math_score_mean
    ##             <dbl>
    ## 1            3.78

## Q1

**Question:** Use the summarize command to find the mean reading score
for all students.

## Q2

**Question:** Use the summarize command to find the median for both math
scores and reading scores.

## Q3

**Question:** Look closely at the following code. Why is it throwing an
error? How can Rstudio help you see this error?

**Answer:** We need another “)” at the end of the code. The first “)” is
for the min function but we also need a “)” to end the summarize
function. Rstudio helps because if you go to the right of a paranthese,
it highlights the corresponding closing paranthese.

# Summarize with groups

## Example

**Question:** Find the minimum math score for each school.

``` r
scores %>% 
  group_by(school) %>% 
  summarize(min_math_score = min(math_score))
```

    ## # A tibble: 2 x 2
    ##   school min_math_score
    ##   <chr>           <dbl>
    ## 1 north               3
    ## 2 south               2

## Q1

**Question:** Find the maximum math score for each teacher.

## Q2

**Question:** If we grouped by gender, and then summarized with the
minimum reading score, how many rows would the resulting data frame
have?

**Answer:**

## Q3

**Question:** Remember that mutate always keeps the same number of rows
but summarize usually reduces the number of rows. Why doesn’t the
following use of summarize reduce the number of rows?

**Answer:**

## Q4

**Question:** Create a data frame with the mean and median reading score
by gender, as well as the number of students of that gender.

# Combining verbs

## Example

**Question:** Select just the name and math\_score columns. Then create
a new column “math\_score\_ec” that is a students math score plus 5
extra credit points. Finally, arrange the data frame by math\_score\_ec
from low to high.

``` r
scores %>% 
  select(name, math_score) %>% 
  mutate(math_score_ec = math_score + 5) %>% 
  arrange(math_score_ec)
```

    ## # A tibble: 9 x 3
    ##   name   math_score math_score_ec
    ##   <chr>       <dbl>         <dbl>
    ## 1 greg            2             7
    ## 2 carol           3             8
    ## 3 peter           3             8
    ## 4 mike            4             9
    ## 5 marcia          4             9
    ## 6 jan             4             9
    ## 7 cindy           4             9
    ## 8 bobby           5            10
    ## 9 alice           5            10

## Q1

**Question:** Select every column except the teacher column. Create a
new variabled called “mean\_score” that is the mean of a student’s math
and reading score. Finally, arrange the data frame by mean\_score from
low to high.

## Q2

**Question:** Remove any students with smith as a teacher, then find the
mean math\_score by gender.

## Q3

**Question:** Find the min, max, and median reading\_score for female
students at south school.

## Q4

**Question:** Inspect each of the following code blocks. They both do
about the same thing. Which one do you think is preffered from a
computer efficiency standpoint?

``` r
# code block 1
scores %>% 
  group_by(school, teacher) %>% 
  summarize(max_math_score = max(math_score)) %>% 
  filter(school == "south")
```

    ## # A tibble: 2 x 3
    ## # Groups:   school [1]
    ##   school teacher max_math_score
    ##   <chr>  <chr>            <dbl>
    ## 1 south  johnson              4
    ## 2 south  perry                5

``` r
# code block 2
scores %>% 
  filter(school == "south") %>% 
  group_by(teacher) %>% 
  summarize(max_math_score = max(math_score))
```

    ## # A tibble: 2 x 2
    ##   teacher max_math_score
    ##   <chr>            <dbl>
    ## 1 johnson              4
    ## 2 perry                5

**Answer:**

## Challenge

Play around with these tools. Write a question or two that you think
best exposes a misunderstanding you had or drills down on an important
thing to remember. I’d love to add these questions in the future\! Feel
free to email what you came up with to <stenhaug@stanford.edu>.