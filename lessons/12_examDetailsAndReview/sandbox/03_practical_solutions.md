### Participation 3: starter

#### Name :


#### Date :
17 Nov 2020

#### General Instructions:
Please copy this file and its directory into your practicals repository. Once you have copied over your directory, please follow the included code and respond to the associated questions. Please do not forget to `push` your work



#### Question1
We will plot data from the `Table1` dataset from R which can be viewed using `View(Table1)`.

```
ggplot(table1, aes(year, cases)) + geom_line(aes(group = country),colour = "grey50") + geom_point(aes(colour = country))
```

Using the point-slope equation from algebra, we can build an equation (of the form, y = mx + b) for the line that connects the points for Brazil.


```
# Two points in cartesian format.
x1 <- 1999  # years
x2 <- 2000
y1 <- 37737 # cases
y2 <- 80488
```

We find the slope and build the line equation with the following function. The `x_input` is the year for which we want a corresponding value of cases.  

```
getCases <- function(bx1, bx2, by1, by2, x_input)
  {
  # find slope
  m = (by2 - by1)/(bx2 - bx1)
  return (m*bx2 - m*(x_input) + by1)
}
```

At x = 1999.5 (years), what does y equal (for cases)?
# SOLUTION: y = 59112.5 when `getCases(x1,x2,y1,y2,1999.5)` is entered.

Above, we used the two points from the Brazil data to draft a line equation and then we calculated the value for _y_ when _x_ equaled 1999.5. Is the _y_ value that we calculated at this point a useful value if this were a predictive model? Explain why or why not.

# SOLUTION: There is not enough data to have any real understanding of the data between these points.



#### Question2

We use the Iris dataset which is built into R. Make a scatter plot of the `Sepal.Length` by `Petal.Length`.

```
ggplot(iris, aes(x = Sepal.Length, y = Petal.Length)) +  geom_point(aes(colour = Sepal.Length))
```
and
```
ggplot(iris, aes(y = Sepal.Length, x = Petal.Length)) +  geom_point(aes(colour = Sepal.Length))
```

We note that all the points on the plot are the same color. Create a plot in which the three species of iris (found by `unique(iris$Species)`) are color-coded and share the same canvas. Use the below code to create three datasets to make your color-coded plot.

```
library(tidyverse)
iris_setosa <- filter(iris, Species == "setosa")
iris_versicolor <- filter(iris, Species == "versicolor")
iris_virginica <- filter(iris, Species == "virginica")
```


Add your code to create a plot of all three on the same canvas.

# SOLUTION:

```
ggplot(iris_setosa) + geom_point(mapping = aes(x = Sepal.Length, y = Petal.Length), color = "blue")  + geom_point(data = iris_versicolor, mapping = aes(x = Sepal.Length, y = Petal.Length), color = "red") + geom_point(dat = iris_virginica, mapping = aes(x = Sepal.Length, y = Petal.Length), color = "green")
```

Note: an identical solution is the following,
```
library(tidyverse)
ggplot(iris, aes(x = Petal.Length, y = Sepal.Length)) + geom_point(aes(colour = Species))
```


#### Question3

Do you see a correlation? Use `pairs.panels()` from the `psych` library to find the strongest correlation between two variables of the `iris` dataset.

# SOLUTION

```
cor(iris$Petal.Length, iris$Petal.Width)
```

or

```
library(psych)
pairs.panels(iris)
```
The strongest correlation is between `Petal.Length` and `Petal.Width`



#### Question 4

Run a t-test between the two variables that had the strongest correlation in the `iris` dataset. Show your code. What do you conclude about the null hypothesis?


# SOLUTION

```
t.test(iris$Petal.Length, iris$Petal.Width)
```

Reject the null hypothesis on account of the p-value being close to zero.



#### Question 5

Run a linear model over the variables having the strongest correlation in the `iris` dataset. What do you conclude in terms of variable prediction?


# SOLUTION:

```
summary(lm(iris$Petal.Width ~ iris$Petal.Length))
```

Conclusion: One variable is very good at explaining the growth of the other.




(Did you remember to add your name and data to the top of this document?)
