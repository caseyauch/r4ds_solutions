# r4ds-solutions

# 3.2.1
### Run `ggplot(data = mpg)` what do you see?
An empty gray plot. 
```{r}
ggplot(data = mpg)
```

### How many rows are in mpg? How many columns?
234 rows, 11 columns

### What does the `drv` variable describe?  Read the help for `?mpg` to find out.
```{r}
?mpg
```
`drv` is the type of drive train, where f = front-wheel drive, r = rear wheel drive, 4 = 4wd

### Make a scatterplot of `hwy` vs `cyl`.
```{r}
ggplot(mpg) + geom_point(mapping = aes(x=cyl, y=hwy))
```

### What happens if you make a scatterplot of `class` vs `drv`. Why is the plot not useful?
```{r}
ggplot(mpg, aes(x=class, y=drv)) + geom_point()
```
This plot isn’t useful because the two variables (`class` and `drv`) tell you nothing about fuel efficiency. You’ve got to use `cty` or `hwy`. EDIT: they're both categorical variables.  

# 3.3.1
### What's gone wrong with this code? Why are the points not blue?
To set aesthetic manually, it must be outside of aes(). 
```{r}
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
```

### Which variables in `mpg` are categorical? Which variables are continuous? 
Categorical: fl, class, cyl, trans, drv, manufacturer, model, year
Continuous: cty, hwy

### Map a continuous variable to `color`, `size`, and `shape`. How do these aesthetics behave differently for categorical vs. continuous variables? 
For continuous variables, `color` is a gradient of blue. A continuous variable can’t be mapped to `shape`. `size` should only be used for discrete variables. 

### What happens if you map the same variable across multiple aesthetics? What happens if you map different variables across multiple aesthetics?
There's lots of uniformality. You can't map different varaibles across the same aesthetic. 

### What does the `stroke` aesthetic do? What shapes does it work with?
The stroke is the border of a shape. It works well with squares and circles, not plus signs or triangles. 
```{r}
ggplot(data = mpg) + geom_point(aes(x = cty, y = hwy, stroke = displ), shape = 21)
```

### What happens if you set an aesthetic to something other than a variable name, like `displ < 5`?
Setting an aesthetic to an argument like `year < 2000` evaluates the argument for every point (true/false). 
```{r}
ggplot(data = mpg) + geom_point(aes(x = cty, y = hwy, colour = year < 2000))
```

# 3.5.1
### What happens if you facet on a continuous variable?
There are many plots, too many to be helpful, because you get a row/column for each unique variable.

### What do the empty cells in plot with `facet_grid(drv ~ cyl)` mean?
Empty cells are a result of no value matching those rows. For this example, there are no car in the data set wih 5 `cyl` and `4` wheel drive.

### What plots does the following code make? What does `.` do?
`.` is just a placeholder and does nothing. 

# 3.6.1
### What geom would you use to draw a line chart? A boxplot? A histogram? An area chart?
geom_smooth() = line chart,geom_boxplot() = box plot, geom_histogram() = histogram, geom_area() = area

### What does `show.legend = FALS` do? What happens if you remove it? Why do you think I used it earlier in the chapter?
It hides the legend, and if removed, the legend is shown on the right. In the example where `show.legend = FALSE` is used earlier in the chpater, the author removed the legend to match the other 2 plots.

### What does the `se` argument to `geom_smooth()` do?
`se = TRUE` displays the confidence interval, or the shadow-like figure on a plot. 

### Will these two graphs look different? Why/why not?
```
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()

ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
 ```
No, they will look the same. V1 is just a more concise way of writing the code. 

### Recreate the R code necessary to generate the following graphs.
1. `ggplot (data = mpg, mapping = aes(x = displ, y = hwy)) + geom_point() + geom_smooth(se = FALSE)`
2. `ggplot (data = mpg, mapping = aes(x = displ, y = hwy, group = drv)) + geom_point() + geom_smooth(se = FALSE)`
3. `ggplot (data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + geom_point() + geom_smooth(se = FALSE)`
4. `ggplot (data = mpg, mapping = aes(x = displ, y = hwy)) + geom_point(mapping = aes(color = drv)) + geom_smooth(se = FALSE)`
5. `ggplot (data = mpg, mapping = aes(x = displ, y = hwy)) + geom_point(mapping = aes(color = drv)) + geom_smooth(mapping = aes (linetype = drv), se = FALSE)`
6. 

# 3.7.1
### What is the default geom associated with `stat_summary()`? How could you rewrite the previous plot to use that geom function instead of the stat function?
Using the [geoms cheat sheet](https://rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf) it looks `stat_summary()` looks a lot like `geom_pointrange` but after some trial/error, geom_pointrange doesn't automate the ymax and ymin values like `stat_summary()`. Using  `geom_line()` and `stat_summary()` seems to work.

```ggplot(data = diamonds, mapping = aes(x = cut, y = depth)) +
     geom_line() +
     stat_summary(fun.y = "median", geom = "point", size = 3)
```
### What does `geom_col()` do? How is it different to `geom_bar()`?

### Most geoms and stats come in pairs that are almost always used in concert. Read through the documentation and make a list of all the pairs. What do they have in common?

### What variables does `stat_smooth()` compute? What parameters control its behaviour?

### In our proportion bar chart, we need to set group = 1. Why? In other words what is the problem with these two graphs?
```
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, y = ..prop..))
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = color, y = ..prop..))
  ```
# 3.8.1
### What is the problem with this plot? How could you improve it?
```
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point()
  ```
### What parameters to `geom_jitter()` control the amount of jittering?

### Compare and contrast `geom_jitter()` with `geom_count()`.

### What’s the default position adjustment for `geom_boxplot()`? Create a visualisation of the mpg dataset that demonstrates it.
