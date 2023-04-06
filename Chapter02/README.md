# 2 GETTING STARTED

## :herb: 2.1 Installing R
1. Go to The R Project website at [r-project.org](https://cran.r-project.org/)
2. Click on the "Download R" link
3. Choose the mirror closest to your location
4. Depending on your operating system, select the appropriate option:
   - For Windows, click on "Install R for the first time"
   - For Mac, download the package and install like any other software
   - For Linux, follow the appropriate steps for your distribution
5. Install R like any other software on your computer
6. You're now ready to start using R!

## :herb: 2.2 Environments for R
When working with R, there are several options for running R on your computer:
1. Native R app: comes with R installation, can run commands and open multiple windows, but awkward to use and different keyboard commands depending on OS
2. Rstudio: most common choice, free and open-source app with a single window for typing code, displaying results, and plotting graphs
3. Rstudio.cloud: an online version of Rstudio, great for working with Chromebook or without installing software
4. Microsoft Azure Notebooks: free service that allows you to run R in a Jupyter notebook
5. Other surfaces such as Google Colab, IBM Watson, or Google AutoML: allows you to run R in different applications or interfaces
6. Jamovi: a free open-source application that runs on R, with a graphical user interface and an option for syntax mode to transition from a menu-based application to a code-based application like R.

## :herb: 2.3 Installing RStudio

To work with R, it is recommended to use an application called RStudio, which is a free and open-source interactive development environment for R. Here are the steps to install RStudio:

1. Go to [rstudio.com](https://posit.co/downloads/) and click on the "Products" tab.
2. Choose "RStudio", which is an IDE for R.
3. Select the desktop version and choose the open-source edition.
4. Click on the "Download RStudio" button.
5. Choose the desktop version again and click on the download button, which will automatically detect your operating system.
6. Install the downloaded application like any other software.

Once RStudio and R are installed, you will be ready to work on data. The next video will demonstrate how to navigate through RStudio to start working with R.

## :herb: 2.4 Navigating the RStudio Environment

Once you've installed RStudio, you'll see a collection of window panes that break up the single window into logical components.

- Top-left: This is where the scripts or programs that you write and then save go, and you can have more than one open at a time. You can add headers and comments to the code, and you'll see a document outline using headers.
- Below the script pane is the console. This is where text or numerical output goes.
- The terminal is also available, which is similar to Bash.
- Off to the right is the environment, where things that are being saved in memory are located. You can see saved data objects and their properties.
- Below that is the files pane, where you can navigate to and open files you're working with. If you open an R project file, you'll be automatically taken to that project and it will be easier to specify files.
- Next to the files pane is the packages pane. This is where you can see additional bits of code that you can install into R to give it extra functionality.
- You'll also find the help pane and viewers for certain kinds of interactive graphs.

|![image](https://user-images.githubusercontent.com/19381768/230288889-ad90afd2-3e95-448a-bc56-9769ccce7dba.png)|
|:--:|
|RStudio windows|

In addition, you can set a lot of other options for working in RStudio. 
- There are keyboard commands that you can modify, Tools -> Keyboard Shortcuts Help
- Also, you can zoom in and out of different panes. 
- It's also possible to set a margin for your code. This is useful if you're working on a small screen. You can set this in Options -> Preferences -> Code -> Display -> Show margin -> Margin column.
- Under the same prompt, you can change the Appearance to set up the theme for the editor.

RStudio is customizable and adaptable to your own preferences and work flow. It's an amazing environment for getting an overall picture of what's happening with your data, writing code, seeing the results, stepping through it, and getting a much richer picture of what's going on.

## :herb: 2.5 Entering data

### :apple: 2.5.1 Basic commands
- Small sets of data can be entered directly into R through the script window.
- Basic math can be performed in R. For example, `2 + 2` returns 4.

```r
2+2  # Basic math; press cmd/ctrl enter
1:100  # Prints numbers 1 to 100 across several lines
print("Hello, World!")  # Prints "Hello, World" in console
```

### :apple: 2.5.2 Assigning values
- To save information into variables, use the assignment operator (<-). For example, `a <- 1`.
```r
# Individual values
a <- 1            # Use <- and not =
2 -> b            # Can go other way, but silly
c <- d <- e <- 3  # Multiple assignments

# Multiple values
x <- c(1, 2, 5, 9)  # c = Combine/collect/concatenate
x                   # Print contents of x in Console
```

### :apple: 2.5.3 Sequences
- It is considered bad form to assign a value first and then the variable name.
- Multiple values can be assigned simultaneously using the `c()` command.
- Sequences can be created using the colon operator (:), or the `seq()` command.
```r
# Create sequential data
0:10     # 0 through 10
10:0     # 10 through 0
seq(10)  # 1 to 10
seq(30, 0, by = -3)  # Count down by 3
```

### :apple: 2.5.4 Math
- Simple math operations can be performed in R, such as addition and multiplication using the `+` and `*` operators respectively.
- To simultaneously save a command and show it in the console, surround the command with parentheses.
```r
# Surround command with parentheses to also print
(y <- c(5, 1, 0, 10)) 
x           # Take another look at x
x + y       # Adds corresponding elements in x and y
x * 2       # Multiplies each element in x by 2
2^6         # Powers/exponents
sqrt(64)    # Square root
log(100)    # Natural log: base e (2.71828...); NOT "ln"
log10(100)  # Base 10 log
```

### :apple: 2.5.5 Clean up
```r
# Clear environment
rm(list = ls()) 

# Clear console
cat("\014")  # ctrl+L

# Clear mind :)
```
## :herb: 2.6 Data types and structures

### :apple: 2.6.1 Data types
#### :bread: 2.6.1.1 Numeric
- The most common data type in R, doubles precision numbers are the default
- Use the `typeof()` command to check the data type of a variable
```r
n1 <- 15  # Double precision by default
n1
typeof(n1)

n2 <- 1.5
n2
typeof(n2)
```

#### :bread: 2.6.1.2 Character
- Use quotes to define a character variable
- R does not differentiate between a single character and a collection of characters
```r
c1 <- "c"
c1
typeof(c1)

c2 <- "a string of text"
c2
typeof(c2)
```

#### :bread: 2.6.1.3 Logical
- Boolean or binary variables with the values `TRUE` or `FALSE`, are not in quotes and must be in all caps
```r
l1 <- TRUE
l1
typeof(l1)

l2 <- F
l2
typeof(l2)
```

### :apple: 2.6.2 Data structures
#### :bread: 2.6.2.1 Vector
- A collection of numbers of the same data type, even a single number is considered a vector of size one
- Use the `c()` function to concatenate values and create a vector
```r
v1
is.vector(v1)

v2 <- c("a", "b", "c")
v2
is.vector(v2)

v3 <- c(TRUE, TRUE, FALSE, FALSE, TRUE)
v3
is.vector(v3)
```

#### :bread: 2.6.2.2 Matrix
- A two-dimensional structure with rows and columns of the ***same length and data type***
- Use the `matrix()` function to create a matrix
```r
m1 <- matrix(c(T, T, F, F, T, F), nrow = 2)
m1

m2 <- matrix(c("a", "b", 
               "c", "d"), 
               nrow = 2,
               byrow = T)
m2
```
#### :bread: 2.6.2.3 Array
- A multidimensional structure with data points in each column, row, or table of the same data type
- Use the `array()` function to create an array
```r
# Give data, then dimensions (rows, columns, tables)
a1 <- array(c( 1:24), c(4, 3, 2))
a1
```
#### :bread: 2.6.2.4 Data Frame
- The most common data structure in R, allows for different data types in the same memory object
- Use the `data.frame()` function to create a data frame
```r
# Can combine vectors of the same length

vNumeric   <- c(1, 2, 3)
vCharacter <- c("a", "b", "c")
vLogical   <- c(T, F, T)

df1 <- cbind(vNumeric, vCharacter, vLogical)
df1  # Coerces all values to most basic data type

df2 <- as.data.frame(cbind(vNumeric, vCharacter, vLogical))
df2  # Makes a data frame with three different data types
```

#### :bread: 2.6.2.5 List
- A flexible data structure that can contain different variable types and lengths
- Use the `list()` function to create a list
```r
o1 <- c(1, 2, 3)
o2 <- c("a", "b", "c", "d")
o3 <- c(T, F, T, T, F)

list1 <- list(o1, o2, o3)
list1

list2 <- list(o1, o2, o3, list1)  # Lists within lists!
list2
```

### :apple: 2.6.3 Coercing Types
- Coercing refers to converting a variable from one data type or structure to another
- Automatic coercion happens when R converts to the least restrictive data type
- Use `as.integer()`, `as.numeric()`, or `as.data.frame()` to specify the data type or structure to convert to
#### :bread: 2.6.3.1 Automatic Coercion
```r
# Goes to "least restrictive" data type

(coerce1 <- c(1, "b", TRUE))
typeof(coerce1)
```
#### :bread: 2.6.3.2 Coerce Numeric to Integer
```r
(coerce2 <- 5)
typeof(coerce2)

(coerce3 <- as.integer(5))
typeof(coerce3)
```
#### :bread: 2.6.3.3 Coerce Character to Numeric
```r
(coerce4 <- c("1", "2", "3"))
typeof(coerce4)

(coerce5 <- as.numeric(c("1", "2", "3")))
typeof(coerce5)
```
#### :bread: 2.6.3.4 Coerce Matrix to Data Frame
```r
(coerce6 <- matrix(1:9, nrow= 3))
is.matrix(coerce6)

(coerce7 <- as.data.frame(matrix(1:9, nrow= 3)))
is.data.frame(coerce7)
```
### :apple: 2.6.4 Clean up
```r
# Clear environment
rm(list = ls()) 

# Clear console
cat("\014")  # ctrl+L

# Clear mind :)
```
