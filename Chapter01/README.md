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
<blockquote>
  
```
[1] "id"      "happy"   "year"    "age"     "sex"     "marital" "degree"  "finrela" "health"  "wtssall"
```
</blockquote>

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
<blockquote>

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
</blockquote>

```r
# Delete id and wtssall, which is a weighting variable that
# doesn't change results appreciably
df %<>%
  select(happy:health) %>%
  print()
```
<blockquote>

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
</blockquote>

```r
# Check levels of "happy"
levels(df$happy)
```
<blockquote>
  
```
[1] "not too happy" "pretty happy"  "very happy" 
```
</blockquote>
  
```r
# Reverse levels of "happy" so "very happy" is at the top of
# stacked bar charts
df %<>%
  mutate(happy = fct_rev(happy))

levels(df$happy)
```
<blockquote>
     
```
[1] "very happy"    "pretty happy"  "not too happy"
```
</blockquote>
  
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

#### OUTCOME VARIABLE: HAPPINESS
```r
# Bar chart of happy
df %>%
  ggplot() + 
  geom_bar(aes(happy, fill = happy)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )
```
> <img src="https://user-images.githubusercontent.com/19381768/230099937-5d344c73-ac5c-4aa2-8610-90db7a95f840.png" width=50%/>

```r
# Frequencies for happy
df %>% count(happy)
```
<blockquote>
  
```
# A tibble: 4 × 2
  happy             n
  <fct>         <int>
1 very happy    14800
2 pretty happy  25874
3 not too happy  5629
4 NA             4717
```
</blockquote>

```r
# Filter out the NA responses on happy
df %<>%
  filter(!is.na(happy))

# Frequencies for happy
df %>% count(happy)
```
<blockquote>
    
```
# A tibble: 3 × 2
  happy             n
  <fct>         <int>
1 very happy    14800
2 pretty happy  25874
3 not too happy  5629
```
</blockquote>
  
#### HAPPINESS AND GENDER
```r
# Bar chart of sex
df %>%
  ggplot() + 
  geom_bar(aes(sex, fill = sex)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )
```
> <img src="https://user-images.githubusercontent.com/19381768/230102773-473473ed-cbf8-49b6-bf48-d99bde4315bb.png" width=50%/>

```r
# Frequencies for sex
df %>% count(sex)
```
<blockquote>
  
```
# A tibble: 2 × 2
  sex        n
  <fct>  <int>
1 male   20357
2 female 25946
```
</blockquote>
  
```r
# 100% stacked bar chart
df %>%
  ggplot(aes(sex, fill = happy)) + 
  geom_bar(position = "fill")
# Looks pretty similar
```
> <img src="https://user-images.githubusercontent.com/19381768/230247293-09ae5036-f478-4775-a2b3-39e6e37f4e41.png" width=50%/>

#### HAPPINESS AND MARITAL STATUS
```r
# Bar chart of marital
df %>%
  ggplot() + 
  geom_bar(aes(marital, fill = marital)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )
```
> <img src="https://user-images.githubusercontent.com/19381768/230247658-5f3112d1-218d-49f5-8382-de135a205696.png" width=50%/>

```r
# Frequencies for marital
df %>% count(marital)
```
<blockquote>
  
```
# A tibble: 6 × 2
  marital           n
  <fct>         <int>
1 married       25662
2 never married  8979
3 divorced       5385
4 widowed        4652
5 separated      1618
6 NA                7
```
</blockquote>
    
```r
# 100% stacked bar chart
df %>%
  filter(!is.na(marital)) %>%
  ggplot(aes(marital, fill = happy)) + 
  geom_bar(position = "fill")
```
> <img src="https://user-images.githubusercontent.com/19381768/230248454-fa46da06-a1ca-4125-895e-9f8765dd9d3a.png" width=50%/>
  
```r
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
```
<blockquote>
    
```
# A tibble: 46,303 × 9
   happy          year   age sex    marital       degree         finrela       health    married
   <fct>         <dbl> <dbl> <fct>  <fct>         <fct>          <fct>         <fct>     <fct>  
 1 not too happy  1972    23 female never married bachelor       average       good      no     
 2 not too happy  1972    70 male   married       lt high school above average fair      yes    
 3 pretty happy   1972    48 female married       high school    average       excellent yes    
 4 not too happy  1972    27 female married       bachelor       average       good      yes    
 5 pretty happy   1972    61 female married       high school    above average good      yes    
 6 pretty happy   1972    26 male   never married high school    above average good      no     
 7 not too happy  1972    28 male   divorced      high school    above average excellent no     
 8 not too happy  1972    27 male   never married bachelor       average       good      no     
 9 pretty happy   1972    21 female never married high school    average       excellent no     
10 pretty happy   1972    30 female married       high school    below average fair      yes    
# ℹ 46,293 more rows
# ℹ Use `print(n = ...)` to see more rows
```
</blockquote>
  
```r
# Frequencies for married
df %>% count(married)
```
<blockquote>
  
```
# A tibble: 3 × 2
  married     n
  <fct>   <int>
1 no      20634
2 yes     25662
3 NA          7
```
</blockquote>
  
```  
# 100% stacked bar chart
df %>%
  filter(!is.na(married)) %>%
  ggplot(aes(married, fill = happy)) + 
  geom_bar(position = "fill")
# Married group has more in "very happy" and fewer in "not
# too happy"
```
> <img src="https://user-images.githubusercontent.com/19381768/230249891-6e886fb6-4a36-4470-88fe-22affa53772e.png" width=50%/>

#### HAPPINESS AND LEVEL OF EDUCATION
```r
# Bar chart of degree
df %>%
  ggplot() + 
  geom_bar(aes(degree, fill = degree)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )
```
> <img src="https://user-images.githubusercontent.com/19381768/230249984-932b9bd5-b783-4fa7-a4ca-7138c3d110c2.png" width=50%/>

```r
# Frequencies of degree
df %>% count(degree)
```
<blockquote>
  
```
# A tibble: 6 × 2
  degree             n
  <fct>          <int>
1 lt high school 11053
2 high school    23880
3 junior college  2252
4 bachelor        6134
5 graduate        2840
6 NA               144
```
</blockquote>
    
```r
# 100% stacked bar chart
df %>%
  filter(!is.na(degree)) %>%
  ggplot(aes(degree, fill = happy)) + 
  geom_bar(position = "fill")
# Things look bad for "lt high school" with only small
# differences between other groups?
```
> <img src="https://user-images.githubusercontent.com/19381768/230250362-5524a88a-91cf-4fc0-8bac-94502f265dda.png" width=50%/>

```r
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
```
<blockquote>
    
```
# A tibble: 46,303 × 10
   happy          year   age sex    marital       degree         finrela       health    married college
   <fct>         <dbl> <dbl> <fct>  <fct>         <fct>          <fct>         <fct>     <fct>   <chr>  
 1 not too happy  1972    23 female never married bachelor       average       good      no      yes    
 2 not too happy  1972    70 male   married       lt high school above average fair      yes     no     
 3 pretty happy   1972    48 female married       high school    average       excellent yes     no     
 4 not too happy  1972    27 female married       bachelor       average       good      yes     yes    
 5 pretty happy   1972    61 female married       high school    above average good      yes     no     
 6 pretty happy   1972    26 male   never married high school    above average good      no      no     
 7 not too happy  1972    28 male   divorced      high school    above average excellent no      no     
 8 not too happy  1972    27 male   never married bachelor       average       good      no      yes    
 9 pretty happy   1972    21 female never married high school    average       excellent no      no     
10 pretty happy   1972    30 female married       high school    below average fair      yes     no     
# ℹ 46,293 more rows
# ℹ Use `print(n = ...)` to see more rows
```
</blockquote>
  
```r
# Frequencies of college
df %>% count(college)
```
<blockquote>
```
# A tibble: 2 × 2
  college     n
  <chr>   <int>
1 no      35077
2 yes     11226
```
</blockquote>
  
```r
# 100% stacked bar chart
df %>%
  ggplot(aes(college, fill = happy)) + 
  geom_bar(position = "fill")
```
> <img src="https://user-images.githubusercontent.com/19381768/230250993-cf913934-f2f5-41f8-bd22-2ae1d6bf9bf4.png" width=50%/>

#### HAPPINESS AND FINANCIAL STATUS
```r
# Bar chart of finrela
df %>%
  ggplot() + 
  geom_bar(aes(finrela, fill = finrela)) + 
  theme(
    axis.title.x = element_blank(), 
    legend.position = "none"
  )
```
> <img src="https://user-images.githubusercontent.com/19381768/230251104-9fcb6744-4196-4263-8080-d33f25015598.png" width=50%/>

```r
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
