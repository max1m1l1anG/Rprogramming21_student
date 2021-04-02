
<!-- rnb-text-begin -->

---
title: "Lecture 5"
subtitle: "Simulation-based Statistics"
author: "Misja Mikkers and Gertjan Verhoeven"
output: html_notebook
---

# Packages

For this notebook we need the tidyverse package (which should already be installed).


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeSh0aWR5dmVyc2UpXG5gYGAifQ== -->

```r
library(tidyverse)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiUmVnaXN0ZXJlZCBTMyBtZXRob2RzIG92ZXJ3cml0dGVuIGJ5ICdkYnBseXInOlxuICBtZXRob2QgICAgICAgICBmcm9tXG4gIHByaW50LnRibF9sYXp5ICAgICBcbiAgcHJpbnQudGJsX3NxbCAgICAgIFxuLS0gQXR0YWNoaW5nIHBhY2thZ2VzIC0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLSB0aWR5dmVyc2UgMS4zLjAgLS1cbnYgZ2dwbG90MiAzLjMuMyAgICAgdiBwdXJyciAgIDAuMy40XG52IHRpYmJsZSAgMy4wLjUgICAgIHYgZHBseXIgICAxLjAuM1xudiB0aWR5ciAgIDEuMS4yICAgICB2IHN0cmluZ3IgMS40LjBcbnYgcmVhZHIgICAxLjQuMCAgICAgdiBmb3JjYXRzIDAuNS4xXG4tLSBDb25mbGljdHMgLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tIHRpZHl2ZXJzZV9jb25mbGljdHMoKSAtLVxueCBkcGx5cjo6ZmlsdGVyKCkgbWFza3Mgc3RhdHM6OmZpbHRlcigpXG54IGRwbHlyOjpsYWcoKSAgICBtYXNrcyBzdGF0czo6bGFnKClcbiJ9 -->

```
Registered S3 methods overwritten by 'dbplyr':
  method         from
  print.tbl_lazy     
  print.tbl_sql      
-- Attaching packages --------------------------------------------------------------------------- tidyverse 1.3.0 --
v ggplot2 3.3.3     v purrr   0.3.4
v tibble  3.0.5     v dplyr   1.0.3
v tidyr   1.1.2     v stringr 1.4.0
v readr   1.4.0     v forcats 0.5.1
-- Conflicts ------------------------------------------------------------------------------ tidyverse_conflicts() --
x dplyr::filter() masks stats::filter()
x dplyr::lag()    masks stats::lag()
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



# Statistical Testing vs simulation

R has its origins as **statistical** programming language. 
So let's do statistics.
A lot of people associate doing statistics with performing **statistical tests**.
There are various problems associated with this approach to statistics.

As computers have become faster, and software better, a different way of doing statistics has become possible.
An important part is about **simulation** of data.
This means generating "fake" data according to our model / assumptions, doing this many times, and analyzing the outcomes.

This notebook provides an introduction to this new way of doing statistics.

# Probability

Very often when we analyse data, there is an element of chance involved.
This element of chance introduces uncertainty when we want to draw conclusions.

For example, suppose we ask twenty students in the hallway of the Tilburg University building their height and their sex.
And suppose we obtain the following set of numbers:


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZGYgPC0gcmVhZC5jc3YyKFwic291cmNlZGF0YS9zdXJ2ZXkuY3N2XCIpXG5cbmRmXG5gYGAifQ== -->

```r
df <- read.csv2("sourcedata/survey.csv")

df
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbImRhdGEuZnJhbWUiXSwibnJvdyI6MjAsIm5jb2wiOjIsInN1bW1hcnkiOltdfSwicmRmIjoiSDRzSUFBQUFBQUFBQnAxU3pVckRRQkRlSmswbGdWYWhlUUJmb0lHMjZIbEI4VllRVHowYWsvMEp4azFKVXV6UnB4RDBLZ2krZzQ5Z0g4U2I0TDA2bTltRm1vS0lBMHUrNzV2NVpuYVdYSnpPcDhFOElJUzRwQXZIOVFDUzNzbjVlSEkwSWFUckFPdEF4dGZmRlZRTkFXaHhBQ2VrN0UzSG12Smpyb1BLYXFxRDhudmsvT1VCNHBIS1orUmlpUG4wSFhYMmhKeDk2TEdFeXA3eGZhSXVDT3JjMXBsNThoVy80aER6cVkvOXhDVnlodjBCSHVoNzJnVm1GcHp0Z05rZndDL0YvK3V6NjlwU2ZqNitwK0liVnBtRkhDUDJKTXVFckExeks3WnF1Znl5dUkyc3M2K2RkL2lpWWJ0OWtzZVZiVy9GSUkzck9PSWwrSUZ0V3BhOVlsRm5oUUtUbzM4S3IyWHVsQzFoZjZuMFRkSlJJcGZxZWpUV0E1bzBSdC9nY0FzN09OTDVNcTA4dXpkVElsUE0zajJQcjFodXlBQTJiaGFPRm1XbTdOTUVvRlpSWGRTeHJRdVNJcmRLc3h2WmZBTkZURmJ5REFNQUFBPT0ifQ== -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["height"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["sex"],"name":[2],"type":["chr"],"align":["left"]}],"data":[{"1":"174.4","2":"M"},{"1":"177.7","2":"F"},{"1":"195.6","2":"F"},{"1":"180.7","2":"M"},{"1":"181.3","2":"M"},{"1":"197.2","2":"M"},{"1":"184.6","2":"M"},{"1":"167.3","2":"F"},{"1":"173.1","2":"M"},{"1":"175.5","2":"M"},{"1":"192.2","2":"F"},{"1":"183.6","2":"M"},{"1":"184.0","2":"M"},{"1":"181.1","2":"M"},{"1":"174.4","2":"M"},{"1":"197.9","2":"F"},{"1":"185.0","2":"F"},{"1":"160.3","2":"M"},{"1":"187.0","2":"F"},{"1":"175.3","2":"M"}],"options":{"columns":{"min":{},"max":[10],"total":[2]},"rows":{"min":[10],"max":[10],"total":[20]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

We are curious whether there is a structural difference in heights when we compare female with male students.

Let us first analyse the data with the methods we have learned so far.

# Exercise 1

Make a histogram of all heights in the dataset, regardless of sex.
Then make a histogram using `facet_wrap()` for each sex separately.
Finally, calculate the mean height by sex group.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyB5b3VyIGNvZGUgaGVyZVxuZ2dwbG90KCkgK1xuICBnZW9tX2hpc3RvZ3JhbShkYXRhID0gZGYsIGFlcyhoZWlnaHQpKVxuYGBgIn0= -->

```r
# your code here
ggplot() +
  geom_histogram(data = df, aes(height))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dfQ== -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG5nZ3Bsb3QoKSArXG4gIGdlb21faGlzdG9ncmFtKGRhdGEgPSBkZiwgYWVzKGhlaWdodCksIGJpbndpZHRoID0gNSkgK1xuICBmYWNldF93cmFwKH4gc2V4KVxuYGBgIn0= -->

```r

ggplot() +
  geom_histogram(data = df, aes(height), binwidth = 5) +
  facet_wrap(~ sex)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuTkFcbk5BXG5OQVxuYGBgIn0= -->

```r
NA
NA
NA
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




So we find a difference. But can we now conclude that female students are on average taller then male students (in the hallway of our university building)? 

To do so, we need a statistical model.

According to Wikipedia, a statistical model is:

> ... a mathematical model that embodies a set of statistical assumptions concerning the generation of sample data (and similar data from a larger population). A statistical model represents, often in considerably idealized form, the data-generating process.

For our idealized, mathematical model, we use the so-called "Normal distribution".

# The Normal distribution

Looking at the height data it appears that the values are spread out around a central location.
It also appears that values below 160 cm and above 200 cm are not observed.
I.e. there are no really extreme values such as 10 cm or 10 m.

For data with these characteristics, it is useful to **assume** that the data are generated by the Normal distribution.
The distribution is conveniently described by just two parameters, 

* the **central location** and 
* the amount of **spread** around the central location.

The central location is equal to the mean, this we all already familiar with.

The amount of spread of a set of numbers can be calculated by the **standard deviation** or **SD** for short.
In R, the function `sd()` is used for this. You will learn more about this in your statistics class.

# Exercise 2

First lets calculate the center location (mean) and the amount of spread in the heights.
Use the `sd()` function.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyB5b3VyIGNvZGUgaGVyZVxuZGYgJT4lXG4gIGdyb3VwX2J5KHNleCkgJT4lXG4gIHN1bW1hcmlzZShtZWFuID0gbWVhbihoZWlnaHQpLCBzZCA9IHNkKGhlaWdodCkpXG5gYGAifQ== -->

```r
# your code here
df %>%
  group_by(sex) %>%
  summarise(mean = mean(height), sd = sd(height))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibnJvdyI6MiwibmNvbCI6Mywic3VtbWFyeSI6eyJBIHRpYmJsZSI6WyIyIHggMyJdfX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJndHlpVERtaXVCaVlHQmdabUFCWW1aV0lKT0J6VG5BME1qVWlJR0JoUW5JWXdUS2NJTG9DcUFxWWJCU0JnWUJJR2FDU2JqQkdMNUFnZzhrNDVEdWJBd0NEbWt4ZmtmZStCMkZpNnZXcGdXVlJ5OTBVQlJNMFBTT0tFQ3pnalV2TVRlMUdHbzhNMVNRdVRpMUFzcGt5VTFOeklPeW1ZcFQwSFJ6RnVXWDY4Rk00QVVwYVFBUy8vLy8vNGR1VFhKT1lqSE1HcGdnVjBwaVNhSmVXaEZRUDVDSHJvVTl2NkFrTXo4UHFJa0pGQVNzYUpvWmk5QUVCRXJ6UUM1SjBVM09LTTNMMWpVMkE5a0Fsb2RnWGlqTmhNUm1odGpKOUI5cUZpdlVMTGJVdlBUTXZGU1k0M01TazFKem9CdytvSmZCUHRZcktNck1LNEY1QlNoYXJGZVNYNUlJVThlVm5KOERFd0Y3anVFZkFJaHppS1Q3QVFBQSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":[""],"name":["_rn_"],"type":[""],"align":["left"]},{"label":["sex"],"name":[1],"type":["chr"],"align":["left"]},{"label":["mean"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["sd"],"name":[3],"type":["dbl"],"align":["right"]}],"data":[{"1":"F","2":"186.1000","3":"10.744921","_rn_":"1"},{"1":"M","2":"178.8846","3":"8.533937","_rn_":"2"}],"options":{"columns":{"min":{},"max":[10],"total":[3]},"rows":{"min":[10],"max":[10],"total":[2]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG5kZiAlPiUgXG4gIHN1bW1hcmlzZShtZWFuID0gbWVhbihoZWlnaHQpLCBzZCA9IHNkKGhlaWdodCkpXG5gYGAifQ== -->

```r

df %>% 
  summarise(mean = mean(height), sd = sd(height))
```

<!-- rnb-source-end -->

<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbImRhdGEuZnJhbWUiXSwibnJvdyI6MSwibmNvbCI6Miwic3VtbWFyeSI6eyJEZXNjcmlwdGlvbiI6WyJkZlssMl0gWzEgeCAyXSJdfX0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVB3YTRCTVJTOWFvYVloRWpzYmF4TmdyQVc3MzBBRnN5MlpvcUowY3BNNVZuWXZzK3g5em4yL2dHMzFVcDBjZE56eiswNTk1NzVielFJb2dBQXl1QmhsWDJFVVBtWjl2ckRQb0JIc0N2aHBLYmVFLzVxSVZCa1F4SGo5YVY5bmQzL1AzM252RmhPNU0wUitwenVXWUdncWNWdjB0c3p5ZzBtUmVKSWFybjRDNjJzcmdlNnZuM2pqQmJXMTVKQlFpVU4xemxxc1hzNGtxbzR5RlJ3RkJHVnhIZkVwZHdobWtldXJraTY4ZmJJZDkzQlNHMHc1OEQzYVI5TTNqdkowM2o1eHF2QytDYmx6QjZmMFJYTFROUEF1RHB0ZU1oVExtMFVaSXRRQ2tudHZ5QVdtV1YwT0hpOEFQcXhQN3JDQVFBQSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["mean"],"name":[1],"type":["dbl"],"align":["right"]},{"label":["sd"],"name":[2],"type":["dbl"],"align":["right"]}],"data":[{"1":"181.41","2":"9.742846"}],"options":{"columns":{"min":{},"max":[10],"total":[2]},"rows":{"min":[10],"max":[10],"total":[1]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuTkFcbk5BXG5OQVxuYGBgIn0= -->

```r
NA
NA
NA
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




In R we can simulate data from a Normal distribution using the function `rnorm()`.
Let us simulate a huge dataset of "fake" height values.
To ensure we obtain the same set of random numbers each time we run the code, we use the `set.seed()`function.
This line of code is already provided.

# Exercise 3

Find out what the arguments are for the `rnorm()` function.
Then use this to generate 10000 numbers from a Normal distribution with mean 181 and SD 10.
Finally, plot a histogram of these 10.000 numbers. Play around with the number of bins or with the binwidth parameter.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuc2V0LnNlZWQoMTIzKVxuXG5ub3JtZGlzdF8xODFfMTAgPC0gcm5vcm0oMTAwMDAsIG1lYW4gPSAxODEsIHNkID0gMTApXG5cbmdncGxvdCgpICsgXG4gIGdlb21faGlzdG9ncmFtKGFlcyhub3JtZGlzdF8xODFfMTApLCBiaW53aWR0aCA9IDMpXG5gYGAifQ== -->

```r
set.seed(123)

normdist_181_10 <- rnorm(10000, mean = 181, sd = 10)

ggplot() + 
  geom_histogram(aes(normdist_181_10), binwidth = 3)
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG4jIHlvdXIgY29kZSBoZXJlXG5gYGAifQ== -->

```r

# your code here
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




# A simple model for heights

Great! Now we now how to simulate data according to assumptions we make of the world, or equivalently, assumptions on **how the data was generated**.

A good way to approach model building, is to start simple, and only add more complexity if the model does not describe the data well.

So let's make a simple model of heights and compare simulated data from the model with the actual observed data.

The simplest model is to assume that there are no structural differences in height between female and male students.

We already know that our height data has characteristics (central location with symmetric spread, no extreme values) that match those of the Normal distribution.

# Exercise 4

Simulate 10 datapoints from a normal distribution with mean and SD equal to our observed heights.
Calculate the mean for these 10 datapoints.


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuc2V0LnNlZWQoMTIzKVxubm9ybWRpc3RfbWFsZWZlbWFsZSA8LSBybm9ybSgxMCwgbWVhbiA9IDE4MS40MSwgc2QgPSA5Ljc0Mjg0NilcblxubWVhbihub3JtZGlzdF9tYWxlZmVtYWxlKVxuYGBgIn0= -->

```r
set.seed(123)
normdist_malefemale <- rnorm(10, mean = 181.41, sd = 9.742846)

mean(normdist_malefemale)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiWzFdIDE4Mi4xMzcxXG4ifQ== -->

```
[1] 182.1371
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyB5b3VyIGNvZGUgaGVyZVxuYGBgIn0= -->

```r
# your code here
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



# Exercise 5

Now write a **for loop** that execute the code you wrote in the previous exercise a 10000 times.
Store all the values of `mean(sample_heights)` in a vector `mean_vals`. You can use the pseudo code below as a starting point.

In this way we end up with 10000 means, all from different data, but from the same underlying model.
Plot a histogram with these 10000 means. 


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyB5b3VyIGNvZGUgaGVyZVxubWVhbl92YWxzIDwtIGMoKVxuXG5mb3IgKGkgaW4gMToxMDAwMCl7XG4gIG1lYW5fdmFsc1tpXSA8LSBtZWFuKHJub3JtKDEwLCBtZWFuID0gMTgxLjQxLCBzZCA9IDkuNzQyODQ2KSlcbn1cblxuZ2dwbG90KCkgK1xuICBnZW9tX2hpc3RvZ3JhbShhZXMoeCA9IG1lYW5fdmFscykpXG5cbmBgYCJ9 -->

```r
# your code here
mean_vals <- c()

for (i in 1:10000){
  mean_vals[i] <- mean(rnorm(10, mean = 181.41, sd = 9.742846))
}

ggplot() +
  geom_histogram(aes(x = mean_vals))

```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dfQ== -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




# Confronting the model with our observed data

Because we can simulate data as often as we want, we learn what are **plausible** values for the average height, the quantity we are interested in.
From the exercise above, we learn that, when we only have 10 observations, values between 174 and 190 for the average height are all plausible outcomes.

# Exercise 6

Go back to the group averages by sex you calculated in Exercise 1.
Plot these group averages as red vertical lines in the plot you created in Exercise 5.
use `geom_vline()` for this.



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyB5b3VyIGNvZGUgaGVyZVxuZ2dwbG90KCkgK1xuICBnZW9tX2hpc3RvZ3JhbShhZXMoeCA9IG1lYW5fdmFscykpICtcbiAgZ2VvbV92bGluZShhZXMoY29sb3IgPSBcInJlZFwiLCB4aW50ZXJjZXB0ID0gMTg2LjEwMDApKSArIFxuICBnZW9tX3ZsaW5lKGFlcyhjb2xvciA9IFwicmVkXCIsIHhpbnRlcmNlcHQgPSAxNzguODg0NikpXG5gYGAifQ== -->

```r
# your code here
ggplot() +
  geom_histogram(aes(x = mean_vals)) +
  geom_vline(aes(color = "red", xintercept = 186.1000)) + 
  geom_vline(aes(color = "red", xintercept = 178.8846))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbWzAsImBzdGF0X2JpbigpYCB1c2luZyBgYmlucyA9IDMwYC4gUGljayBiZXR0ZXIgdmFsdWUgd2l0aCBgYmlud2lkdGhgLlxuIl1dfQ== -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



Do these group averages for the separate sex groups provide compelling evidence that female students are taller than male students?
Or do they fall within the expected range of plausible values for a world where there are no height differences between the sexes at all?

End of Notebook

<!-- rnb-text-end -->

