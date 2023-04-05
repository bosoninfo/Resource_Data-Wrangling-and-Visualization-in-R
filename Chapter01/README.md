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

- A series of packages will be loaded to provide extra functionality.

- The data set from the Product Plots Package called `Happy` is used, which contains information on happiness from the General Social Survey.
- The data set has over 50,000 observations.
- The id and waiting variable are not necessary, and will be removed.
- The main outcome of interest is happiness, which has three categories: not too happy, pretty happy, and very happy.
- The values are flipped so that very happy comes first.
- The distribution of happiness is examined with a bar chart using ggplot2.
- The cases where respondents did not answer the happiness question are excluded.
- Gender is examined next, but no gender difference is observed.
- Marital status is the next variable examined, with the data set indicating that people who are married tend to be happier than those who are not.
- Education level is the next variable examined, and it appears that people who graduated from college tend to be happier.
- Financial status is the next variable examined, and it appears that people who have at least average finances are much more likely to say that they are very happy.
- Health is the last variable examined, and it appears that people who say they are in excellent health tend to say that they're very happy.
- The year of the survey and age are also examined.
- Density plots and box plots are used to examine the associations between happiness and year of survey, age, and year born.
- The point of visualization and wrangling the data is not to reach final conclusions, but to raise questions and guide further investigation.
- Visualization and wrangling the data can help to organize the data into a form that's best suited for answering questions and getting the visualizations that give insight and ideas for analysis.
