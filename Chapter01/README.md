# 1 WHAT IS R?

## 1.1 R in Context

In this section, we will discuss where R fits in the data science toolbox and its popularity among professionals.

### 1.1.1 Tools for working with data

There are many tools available for working with data, including spreadsheets and statistical applications. These tools offer user-friendly interfaces for data exploration and modeling. However, they may not be sufficient for all data tasks, especially those involving more complex questions or data formats.

### 1.1.2 Spreadsheets for working with data

Spreadsheets, such as `Microsoft Excel` and `Google Sheets`, are ubiquitous and widely used for organizing and analyzing data. They offer flexibility in organizing data in a variety of formats and can sort, filter, count, and summarize data quickly. Spreadsheets can also create relatively sophisticated graphs and visualizations.

While spreadsheets may be sufficient for many real-world data tasks, they may not be suitable for creating more complex statistical models. In these cases, more sophisticated tools like statistical applications or programming languages may be necessary. 

### 1.1.3 Statistical Applications for working with data

Statistical applications, such as `SPSS`, `SAS`, and `Jamovi`, offer user-friendly point-and-click interfaces for data exploration and modeling. They are designed to handle large datasets and can perform a wide range of statistical analyses. These applications are commonly used in fields like psychology, social work, education, and business.

While statistical applications are a powerful tool for data analysis, they may not be suitable for all data tasks. For example, they may not be able to handle data that does not fit neatly into rows and columns. In these cases, a more sophisticated tool like a data-oriented programming language may be necessary.

### 1.1.4 Data-oriented programming languages

Data-oriented programming languages, such as `Python`, `Julia`, and `R`, offer greater control and power in analyzing data. These languages allow for more advanced statistical modeling and data manipulation.

According to the KDnuggets Poll of data mining professionals from 2019, 
- Python is the most commonly used tool for data science tasks, with about two-thirds of respondents using Python. 
- R is also widely used, with about 50% of respondents reporting using it on a daily basis. 
- Excel is also a popular tool, especially for basic data tasks.

|![image](https://user-images.githubusercontent.com/19381768/230088363-2c554254-45de-401a-8765-30f4d9ab54f6.png)|![image](https://user-images.githubusercontent.com/19381768/230088638-c9817e9a-0d40-46c4-92c9-a816a3a7c495.png)|
|:--:|:--:|
|KDnuggets Poll, 2019|Data Science Jobs on Indeed, 2017|
|![image](https://user-images.githubusercontent.com/19381768/230089032-393350f4-f959-4ba2-8b97-dc0a55aecbc8.png)|Python is strong in machine learning and database app development, while R is strong in data analysis for scientific research and social sciences.|
|Scholarly Articles, 2018|Comparison of Python and R|

It's important for data science professionals to be proficient in multiple tools, including R, Python, Java, C++, and SQL. R is a major tool for many companies and fields and is often the tool of choice for common data tasks.

### 1.1.5 Comparison of Different Data Tools

| Tool | Advantages | Limitations |
|---|---|---|
| Spreadsheets | Ubiquitous, flexible in organizing data, quick and easy to sort, filter, count, and summarize | May not be suitable for creating complex statistical models                                                                |
| Statistical applications | User-friendly point-and-click interfaces, designed to handle large datasets, perform complex analyses | May not be able to handle data that does not fit neatly into rows and columns                                             |
| Data-oriented programming languages | Greater control and power in analyzing data, more advanced statistical modeling and data manipulation | Steeper learning curve, may require more coding expertise, less user-friendly than spreadsheets or statistical applications |

## 1.2 Data science with R: A case study

R is capable of wrangling and visualizing data effectively. A case study based on actual data will be used to demonstrate these capabilities. 

### 1.2.1 Install and load packages

- A series of packages will be loaded to provide extra functionality.
```r
# INSTALL AND LOAD PACKAGES ################################

# Load base packages manually
# library(datasets)  # For example datasets

# Install pacman ("package manager") if needed
if (!require("pacman")) install.packages("pacman")

# pacman must already be installed; then load contributed
# packages (including pacman) with pacman
pacman::p_load(pacman, magrittr, productplots, psych, 
  RColorBrewer, tidyverse)
# pacman: for loading/unloading packages
# magrittr: for pipes
# productplots: for sample dataset "happy"
# psych: for statistical procedures
# RColorBrewer: for color palettes
# tidyverse: for so many reasons
```
### 1.2.2 Load and prepare data
- The data set from the Product Plots Package called `Happy` is used, which contains information on happiness from the General Social Survey.
- The data set has over 50,000 observations.
- The id and waiting variable are not necessary, and will be removed.
- The main outcome of interest is happiness, which has three categories: not too happy, pretty happy, and very happy.
- The values are flipped so that very happy comes first.

```r
# LOAD AND PREPARE DATA ####################################

# "happy" dataset from productplots package; dataset has
# 51,020 rows and 10 variables
?happy
names(happy)
```
```
[1] "id"      "happy"   "year"    "age"     "sex"     "marital" "degree"  "finrela" "health"  "wtssall"
```
```r
# Info on productplots package
# browseURL("http://j.mp/2GMXZCZ")  # Page on CRAN
# browseURL("http://j.mp/36ImMTy")  # Ref manual on CRAN
# browseURL("http://j.mp/37Wxvv7")  # Preprint PDF

# Save dataset to tibble named "df" (for "dataframe")
df <- happy %>%
  as_tibble() %>%
  print()
```
```
# A tibble: 51,020 × 10
      id happy          year   age sex    marital       degree         finrela       health    wtssall
   <dbl> <fct>         <dbl> <dbl> <fct>  <fct>         <fct>          <fct>         <fct>       <dbl>
 1     1 not too happy  1972    23 female never married bachelor       average       good        0.445
 2     2 not too happy  1972    70 male   married       lt high school above average fair        0.889
 3     3 pretty happy   1972    48 female married       high school    average       excellent   0.889
 4     4 not too happy  1972    27 female married       bachelor       average       good        0.889
 5     5 pretty happy   1972    61 female married       high school    above average good        0.889
 6     6 pretty happy   1972    26 male   never married high school    above average good        0.445
 7     7 not too happy  1972    28 male   divorced      high school    above average excellent   0.445
 8     8 not too happy  1972    27 male   never married bachelor       average       good        0.445
 9     9 pretty happy   1972    21 female never married high school    average       excellent   0.445
10    10 pretty happy   1972    30 female married       high school    below average fair        0.889
# ℹ 51,010 more rows
# ℹ Use `print(n = ...)` to see more rows
```
```r
# Delete id and wtssall, which is a weighting variable that
# doesn't change results appreciably
df %<>%
  select(happy:health) %>%
  print()
```
```
# A tibble: 51,020 × 8
   happy          year   age sex    marital       degree         finrela       health   
   <fct>         <dbl> <dbl> <fct>  <fct>         <fct>          <fct>         <fct>    
 1 not too happy  1972    23 female never married bachelor       average       good     
 2 not too happy  1972    70 male   married       lt high school above average fair     
 3 pretty happy   1972    48 female married       high school    average       excellent
 4 not too happy  1972    27 female married       bachelor       average       good     
 5 pretty happy   1972    61 female married       high school    above average good     
 6 pretty happy   1972    26 male   never married high school    above average good     
 7 not too happy  1972    28 male   divorced      high school    above average excellent
 8 not too happy  1972    27 male   never married bachelor       average       good     
 9 pretty happy   1972    21 female never married high school    average       excellent
10 pretty happy   1972    30 female married       high school    below average fair     
# ℹ 51,010 more rows
# ℹ Use `print(n = ...)` to see more rows
```
```r
# Check levels of "happy"
levels(df$happy)
```
```
[1] "not too happy" "pretty happy"  "very happy" 
```
```r
# Reverse levels of "happy" so "very happy" is at the top of
# stacked bar charts
df %<>%
  mutate(happy = fct_rev(happy))

levels(df$happy)
```
```
[1] "very happy"    "pretty happy"  "not too happy"
```
### 1.2.3 Outcome variable: happiness
- The distribution of happiness is examined with a bar chart using ggplot2.
- The cases where respondents did not answer the happiness question are excluded.
- Gender is examined next, but no gender difference is observed.
- Marital status is the next variable examined, with the data set indicating that people who are married tend to be happier than those who are not.
- Education level is the next variable examined, and it appears that people who graduated from college tend to be happier.
- Financial status is the next variable examined, and it appears that people who have at least average finances are much more likely to say that they are very happy.
- Health is the last variable examined, and it appears that people who say they are in excellent health tend to say that they're very happy.
- The year of the survey and age are also examined.
- Density plots and box plots are used to examine the associations between happiness and year of survey, age, and year born.
```r
# OUTCOME VARIABLE: HAPPINESS ##############################

# Bar chart of happy
df %>%
  ggplot() + 
  geom_bar(aes(happy, fill = happy)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )

# Frequencies for happy
df %>% count(happy)

# Filter out the NA responses on happy
df %<>%
  filter(!is.na(happy))

# Frequencies for happy
df %>% count(happy)

# HAPPINESS AND GENDER #####################################

# Bar chart of sex
df %>%
  ggplot() + 
  geom_bar(aes(sex, fill = sex)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )

# Frequencies for sex
df %>% count(sex)

# 100% stacked bar chart
df %>%
  ggplot(aes(sex, fill = happy)) + 
  geom_bar(position = "fill")
# Looks pretty similar

# HAPPINESS AND MARITAL STATUS #############################

# Bar chart of marital
df %>%
  ggplot() + 
  geom_bar(aes(marital, fill = marital)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )

# Frequencies for marital
df %>% count(marital)

# 100% stacked bar chart
df %>%
  filter(!is.na(marital)) %>%
  ggplot(aes(marital, fill = happy)) + 
  geom_bar(position = "fill")

# Create dichotmous married/not variable
df %<>%
  mutate(
    married = ifelse(
      marital == "married",
      "yes",
      "no")
  ) %>%
  mutate(married = as.factor(married)) %>%
 print()

# Frequencies for married
df %>% count(married)

# 100% stacked bar chart
df %>%
  filter(!is.na(married)) %>%
  ggplot(aes(married, fill = happy)) + 
  geom_bar(position = "fill")
# Married group has more in "very happy" and fewer in "not
# too happy"

# HAPPINESS AND LEVEL OF EDUCATION #########################

# Bar chart of degree
df %>%
  ggplot() + 
  geom_bar(aes(degree, fill = degree)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )

# Frequencies of degree
df %>% count(degree)

# 100% stacked bar chart
df %>%
  filter(!is.na(degree)) %>%
  ggplot(aes(degree, fill = happy)) + 
  geom_bar(position = "fill")
# Things look bad for "lt high school" with only small
# differences between other groups?

# Create dichotomous college/not variable for exploration
df %<>%
  mutate(
    college = ifelse(
      degree %in%
      c("junior college",
        "bachelor",
        "graduate"),
      "yes", "no")
  ) %>%
  print()

# Frequencies of college
df %>% count(college)

# 100% stacked bar chart
df %>%
  ggplot(aes(college, fill = happy)) + 
  geom_bar(position = "fill")

# HAPPINESS AND FINANCIAL STATUS ###########################

# Bar chart of finrela
df %>%
  ggplot() + 
  geom_bar(aes(finrela, fill = finrela)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )

# Frequencies for finrela
df %>% count(finrela)

# 100% stacked bar chart
df %>%
  filter(!is.na(finrela)) %>%
  ggplot(aes(finrela, fill = happy)) + 
  geom_bar(position = "fill")

# Create dichotomous varible for average finances or higher
df %<>%
  mutate(
    avg_fin = case_when(
      finrela %in%
        c("far below average",
          "below average") ~
          "no",
      finrela %in%
        c("average",
          "above average",
          "far above average") ~
          "yes",
      finrela == "NA" ~ "NA")
  ) %>%
  print()

# Get frequencies
df %>% count(avg_fin)

# 100% stacked bar chart
df %>%
  filter(!is.na(avg_fin)) %>%
  ggplot(aes(avg_fin, fill = happy)) + 
  geom_bar(position = "fill")
# Big differences in both "very happy" and "not too happy"

# HAPPINESS AND HEALTH #####################################

# Bar chart of health
df %>%
  ggplot() + 
  geom_bar(aes(health, fill = health)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )

# Frequencies of health
df %>% count(health)

# 100% stacked bar chart
df %>%
  filter(!is.na(health)) %>%
  ggplot(aes(health, fill = happy)) + 
  geom_bar(position = "fill")
# Looks pretty linear; should be a good predictor as is

# HAPPINESS AND YEAR OF SURVEY #############################

# Histogram of year
df %>% qplot(year, binwidth = 5, data = .)

# Descriptive statistics for year
df %>% select(year) %>% summary()
# This the year of the survey, so it might reflect
# historical patterns or events (maybe)

# Density plots of year by group
df%>%
  ggplot(aes(x = year, 
    fill = happy)) + 
  geom_density(alpha = 0.5) +
  facet_grid(happy ~ .) +  # facet_grid
  theme(legend.position = "none")  # Turn off legend

# Boxplots of year by group
df %>%
  ggplot(aes(x = happy, 
    y = year, 
    fill = happy)) + 
  geom_boxplot() +
  coord_flip() +
  xlab("") +
  theme(legend.position = "none")
# No obvious differences

# HAPPINESS AND AGE ########################################

# Histogram of age
df %>% qplot(age, binwidth = 5, data = .)

# Descriptive statistics for age
df %>% select(age) %>% summary()
# Could create general age groups

# Density plots of age by group
df %>%
  ggplot(aes(x = age, 
    fill = happy)) + 
  geom_density(alpha = 0.5) +
  facet_grid(happy ~ .) +  # facet_grid
  theme(legend.position = "none")  # Turn off legend
# Maybe a bulge in "very happy" for people 55-70 years old?

# Boxplots of age by group
df %>%
  ggplot(aes(x = happy, 
    y = age, 
    fill = happy)) + 
  geom_boxplot() +
  coord_flip() +
  xlab("") +
  theme(legend.position = "none")
# No obvious differences

# HAPPINESS AND YEAR BORN ##################################

# Calculate year of birth
df %<>%
  mutate(born = year - age)

# Histogram of born
df %>% qplot(born, binwidth = 5, data = .)

# Descriptive statistics for bon
df %>% select(born) %>% summary()

# Density plots of born by group
df %>%
  ggplot(aes(x = born, 
    fill = happy)) + 
  geom_density(alpha = 0.5) +
  facet_grid(happy ~ .) +  # facet_grid
  theme(legend.position = "none")  # Turn off legend

# Boxplots of born by group
df %>%
  ggplot(aes(x = happy, 
    y = born, 
    fill = happy)) + 
  geom_boxplot() +
  coord_flip() +
  xlab("") +
  theme(legend.position = "none")
# No obvious differences

# CLEAN UP #################################################

# Clear data
rm(list = ls())  # Removes all objects from environment

# Clear packages
detach("package:datasets", unload = T)  # For base packages
p_unload(all)  # Remove all contributed packages

# Clear plots
graphics.off()  # Clears plots, closes all graphics devices

# Clear console
cat("\014")  # Mimics ctrl+L

# Clear mind :)
```

- The point of visualization and wrangling the data is not to reach final conclusions, but to raise questions and guide further investigation.
- Visualization and wrangling the data can help to organize the data into a form that's best suited for answering questions and getting the visualizations that give insight and ideas for analysis.
