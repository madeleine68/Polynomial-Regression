# Polynomial-Regression
The human resource team is working in a big company, are about to hire a new employee. They want to negotiate on the salary to be considered for this employee. 
The HR team will definitely look at previous employees’ annual salaries. Simple analysis using Excel and visualizing the data shows the non-linear relationship between position levels and associated salaries.
The polynomial regression model will learn the regression between position levels and salaries to predict the new salary.
I only interested in salary column and position level column, so I reset the data set to keep these two columns in machine learning model.

```
dataset = read.csv('Position_Salaries.csv')
dataset = dataset[2:3]
```
In order to build a polynomial regression, I will create a new column which is the square values of the independent variable (Level) as well as other column which is the cubic value of the Level data. or even increase the order of regression to improve the model.

```
dataset$Level2 = dataset$Level^2
dataset$Level3 = dataset$Level^3
dataset$Level4 = dataset$Level^4
poly_reg = lm(formula = Salary ~ .,
              data = dataset)
```

Let’s visualize the data against the regression model.

```
library(ggplot2)
ggplot() +
  geom_point(aes(x = dataset$Level, y = dataset$Salary),
             colour = 'red') +
  geom_line(aes(x = dataset$Level, y = predict(poly_reg, newdata = dataset)),
            colour = 'blue') +
  ggtitle('figure (Polynomial Regression)') +
  xlab('Level') +
  ylab('Salary')
  ```
  ![plot_zoom_png (1)](https://user-images.githubusercontent.com/46178706/63399727-6dbf9800-c39f-11e9-9ad5-5346a4fa12cc.jpg)
  
As it shown in figure, the model is fit very well with the data. now the HR people can have estimate for the new employee salary by using the regression model. 
For example, to find out the salary for someone in level 6.5, I create a new data frame containing this value, since 6.5 does not exist in data set.

```
predict(poly_reg, data.frame(Level = 6.5,
                             Level2 = 6.5^2,
                             Level3 = 6.5^3,
                             Level4 = 6.5^4))
 ```
 
 The result is 158862.5 
