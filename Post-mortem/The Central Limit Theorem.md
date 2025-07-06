Consider rolling two dice, and taking the average of their values. This sample mean is itself a random variable, as its value is random according to whatever two values happen to appear on the two dice. 

The most common scenario is that the sum of the dice values is 7, and so the most common sample mean will be $3.5$. There is only a single combination which produces a sum of 2 or 12 however, so we're less like to find a sample mean of $1$ or $6$. We can plot this behaviour on a histogram:

![[Sum Of Two Dice Rolls.png]]
*Probability distribution of the sample mean of two dice rolls*

The above histogram represents the probability of the mean value of two dice rolls. What if we increase the number of dice rolls? 

![[Sum Of 4 Dice Rolls.png]]
![[Sum Of 30 Dice Rolls.png]]
*[Source](https://people.hsc.edu/faculty-staff/blins/StatsExamples/CentralLimit/)*

As the number of dice rolls increases, the distribution of the sample mean value increasingly resembles that of a normal distribution centred at the true population mean of $3.5$! Furthermore, the distribution is becoming narrower as the number of rolls increases. 

This is due to something called the *Central Limit Theorem*, and it is the reason why we expect the average value of dice rolls to get closer to $3.5$ over time. When rolling 100 dice, there are simply more ways to produce a sum of 350 compared to a situation where we roll all ones or sixes to get a sum of 100 or 600. 