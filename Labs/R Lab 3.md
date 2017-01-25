---
title: "MA 204 Third Lab"
author: "Your Name Here"
date: "Thursday, February 2, 2015"
---

###Introduction

Today in lab, we will talk more about Bernoulli and Binomial Random variables.    

We will also talk about how to debug your RStudio code

###Bernoulli Random Variables

Remember that if X~Bernoulli(p) then P(X=1)=p, P(X=0)=1-p

How can we simulate Bernoulli variables?  

Let's say I wanted to simulate a Bernoulli Random variable called `X`, such that X~Bernoulli(.33)  In other words, the variable X has a 13/100 chance of equalling 1, and an 87/100 chance of equalling 0:



```r
#Make a list of 100 values where 13 are ones, and 87 are 0's:

mylist<-c(rep(1, 13), rep(0,87))
mylist
```

```
##   [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
##  [36] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
##  [71] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
```

```r
#the rep(a,b) command will make a vector that repeats a b times.
#the c puts the two vectors together to be one vector

#Randomly choose 1 value of the 100 values:

X<-sample(mylist, 1)
X
```

```
## [1] 0
```



####An aside about a cool thing you can down with RStudio:

When we generate a random value, it may be different each time we knit our code.  Here is a way you can deal with that.  Knit this R Markdown document and see what happens with the next line:

Here I found X equal to 0. 

This is a way to insert r objects into our text!

####Back to the Bernoulli distribution:

Let's say I wanted to simulate 500 Bernoulli Random variable called `Y_i`, such that `Y_i`~Bernoulli(.022) for i in 1 :500.  In other words, the variable `Y_i` has a 22/1000 chance of equalling 1, and an 978/1000 chance of equalling 0:


```r
#Make a list of 1000 values where 22 are ones, and 978 are 0's:

mylist<-c(rep(1, 22), rep(0,978))


#the rep(a,b) command will make a vector that repeats a b times.
#the c puts the two vectors together to be one vector

#Randomly choose 500 value of the 1000 values with replacement (aka independently):

Y<-sample(mylist, 500, replace=TRUE)

mean(Y)
```

```
## [1] 0.02
```

There are 10 Y values that equal 1, out of the 500 Y's that we just sampled.  In other words, the proportion of 1's was equal to 0.02.  


####Trying a few more simulations

500 is a pretty big number, but let's choose a number that is closer to infinity.  So now, let's simulate 1000000 Bernoulli Random variable called `Y_i`, such that `Y_i`~Bernoulli(.022) for i in 1 :1000000.  In other words, the variable `Y_i` has a 22/1000 chance of equalling 1, and an 978/1000 chance of equalling 0:



```r
#Make a list of 1000 values where 22 are ones, and 978 are 0's:

mylist<-c(rep(1, 22), rep(0,978))


#the rep(a,b) command will make a vector that repeats a b times.
#the c puts the two vectors together to be one vector

#Randomly choose 500 value of the 1000 values with replacement (aka independently):

Y<-sample(mylist, 1000000, replace=TRUE)

mean(Y)
```

```
## [1] 0.022255
```

There are 2.2255 &times; 10<sup>4</sup> Y values that equal 1, out of the 1000000 Y's that we just sampled.  In other words, the proportion of 1's was equal to 0.022255.  

In general, the more simulations that we do of a Y, the closer the proportion of 1's is going to be to .22

When you do your simulations, it is a good idea to start out with a small number of simulations to make sure that the simulation is doing what it should.  But once you have ascertained that your simulation works, you should bump up the simulations to a large number so that you get the most accurate simulationresults.


###Binomial Random Variables

Remember that if X~Binomial(n,p) X equals the sum of n independent Bernoulli trials with parameter p.  

Since we can we simulate Bernoulli variables, we can also simulate Binomial random variables.  

Let's say that we are interested in Henry's success in the kitchen.  Everytime Henry makes a pancake, he has a 0.73 chance of ruining the pancake by burning it.  Henry made 4 pancakes. Assume that Henry never learns from his mistakes and that whether or not one pancake burned is independent of whether or not another pancake burned. 

Let X= the number of pancakes that Henry burned.  

So here X~Binomial(4, 0.73) 

Let's simulate this Binomial Random variable:


```r
#Make a list of 100 values where 13 are ones, and 87 are 0's:

mylist<-c(rep(1, 73), rep(0,27))


#the rep(a,b) command will make a vector that repeats a b times.
#the c puts the two vectors together to be one vector

#Randomly choose 4 value of the 100 values with replacement (aka independently)

Bern.Trials.4<-sample(mylist, 4, replace=TRUE)

Bern.Trials.4
```

```
## [1] 1 1 0 0
```

```r
X<-sum(Bern.Trials.4)  #Adding up the 4 Independent Bernoulli Trials to get my Binomial variable
X
```

```
## [1] 2
```

Here I found that Henry burned 2 Pancakes.  


#### Looking at the simulated distribution for a Binomial Random Variable

Let's say that Henry makes 4 pancakes every day for 10,000 days (about 27 years of daily pancake making).  And he never ever changes his chances of burning a pancake. Oh Henry, when will you learn?

Let's simulate Henry's pancake making and make a plot of the number of pancakes burned on each of the 10,000 days:



```r
#Make a list of 100 values where 13 are ones, and 87 are 0's:

mylist<-c(rep(1, 73), rep(0,27))


#the rep(a,b) command will make a vector that repeats a b times.
#the c puts the two vectors together to be one vector

#Randomly choose 4 value of the 100 values with replacement (aka independently)

number.burned<-NULL #making an empty list
n.days<-10000  #number of days Henry makes pancakes

for (i in 1:n.days){

  Bern.Trials.4<-sample(mylist, 4, replace=TRUE)
  X<-sum(Bern.Trials.4)  #Adding up the 4 Independent Bernoulli Trials to get my Binomial variable
  number.burned<-c(number.burned, X)
}

table(number.burned)/n.days
```

```
## number.burned
##      0      1      2      3      4 
## 0.0055 0.0564 0.2346 0.4127 0.2908
```

```r
barplot(table(number.burned),names.arg=c(0,1,2,3,4), main="Number of Pancakes Henry Burned", col="chocolate4")  
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-1.png) 


Here I found that with this simulation that Henry burned no pancakes on 0.0055 of the days.  He burned exactly 1 pancake on 0.0564 of the days, he burned two pancakes on 0.2346 of the days, he burned three pancakes on 0.4127 of the days, he burned all four pancakes on 0.2908 of the days.   

####Let's use the Binomial pdf and our knowledge that X~Binomial(4, .73) to find out the EXACT probabilities on the board.

Enter in the exact probabilities here:

P(X=0)=
P(X=1)=
P(X=2)=
P(X=3)=
P(X=4)=

There has to be a quicker way to get RStudio to find these probabilities... and you get to learn about them in this week's lab exercises!!


###Exercise 1

R has many commands for working with probability distributions like the binomial distribution.  Try out the commands below entering in different parameters:

```r
dbinom(3, 9, .15)
```

```
## [1] 0.1069219
```

```r
pbinom(3, 9, .15)
```

```
## [1] 0.9660685
```

```r
rbinom(3, 9, .15)
```

```
## [1] 3 2 1
```


####1a Clearly define what each of the functions returns.  

[INSERT YOUR Response TO EXERCISE 1a HERE]

####1b Use the appropriate function (dbinom, pbinom, rbinom) to find the probability that a binomial random variable `X` is less than 7 given that the number of trials is 20, and p=.4.

[INSERT YOUR code chunk for EXERCISE 1b HERE]

[INSERT YOUR Response TO EXERCISE 1b HERE]

###Exercise 2

Which is more likely to happen? 
A. You flip a coin 10 times and get exactly 5 heads
B. You flip a coin 100 times and get exactly 50 heads
C. You flip a coin 1000 times and get exactly 500 heads

Use either `dbinom`, `rbinom` or `pbinom` (whichever is appropriate here) to find out.  Are you suprised by the answer?

[Exercise 2 INSERT CODE HERE]
[Exercise 2 INSERT RESULTS HERE]


###Exercise 3

Use the code below to visualize what a Binomial distribution looks like.  

```r
n<- 9 # number of trials
p<- .15 # probability of success for each trial
barplot(dbinom(0:n,n,p), names.arg=0:n)
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7-1.png) 

Try different values of `p` while keeping `n` equal to 9.  What values of `p` cause the distribution look most skewed? What values of `p` make the distribution look symmetric?

[INSERT YOUR ANSWERS FOR EXERCISE 3 HERE]

###Exercise 4

This exercise is very similar to what we did for Henry and his burned pancakes.

Here we are learning about a Surgeon named Dr. Frankenfurter.  Dr Frankenfurter performs 9 surgeries a day.  Dr. Frankenfurter is an excellent surgeon, but even excellent surgeons sometimes make mistakes.  Let's say that Dr. Frankenfurter has a .001 chance of making a mistake for each surgery, and that surgeries are independent of each other.  

####Exercise 4a
Simulate the random variable X, where X= the number of times that Dr. F makes a mistake in a surgery in a day, keeping in mind he performs 9 surgeries each day.

[Insert your code for 4a here]

####Exercise 4b
Simulate 1000000 days of Dr. Frankenfurter performing 9 surgeries a day.  Make a barplot of the number of mistakes he makes each day (as we did with Henry and his burned pancakes):

[Insert your code for 4b here]

####Exercise 4c
Based on your results in 4b, how likely is Dr. Frankfurter to make 2 or more mistakes in a day? Verify your results using either `dbinom`, `rbinom` or `pbinom.`
[Insert your response for 4c here]




