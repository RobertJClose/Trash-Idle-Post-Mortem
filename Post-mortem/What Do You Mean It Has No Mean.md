Let's try to understand a bit more about what it means for this distribution to have an undefined mean. We will start with the far simpler example of rolling a dice.
## Dice Rolls
Let's take a fair six-sided dice and roll it a bunch of times. 

We'll denote the face value produced by the $i\text{-th}$ roll as $D_i$, and starting from $i=1$ we'll roll the dice $N$ times in total. We will assume that $N$ is a very large number. Our collection of dice rolls is then this set:

$$
D=\{D_1, D_2, ..., D_N\}
$$

Now we will take our recorded dice rolls and we'll calculate how the mean value of the rolls changed throughout the experiment. For example, we could consider the first three rolls and calculate what the mean value of those three rolls was. We will tag the mean values with a bar over the top of the letters, like $\bar{D}$.

To calculate the mean value up to the $n\text{-th}$ roll:

$$
\bar{D}_n = \frac{1}{n} \sum_{i=1}^n D_i 
$$

The end result is a new set that tells us how the mean value changed as we rolled the dice. 

$$
\bar{D}=\{\bar{D}_1, \bar{D}_2, ... , \bar{D}_N\}
$$

So the value of $\bar{D}_4$ is the average of the first four dice rolls.

A fair six-sided dice roll has a well defined true mean value of $3.5$, which is simply the average value of the faces. How do the values in $\bar{D}$ compare to the true mean value?

![[Average Dice Rolls.png]]
*Wikipedia*

To start with, the average value can deviate away from the true value quite dramatically. The more you roll the dice however, the averages get closer to the true mean value. 

You can explore this for yourself at [this website](https://researchdatapod.com/interactive-dice-roller/), where you may roll several dice simultaneously (this is equivalent to rolling the same dice several times). Each time you run the simulation, the mean value will be calculated automatically. If you roll just a few dice, the mean value can jump around quite dramatically. If you instead roll many dice at once, the mean value will rarely stray far from the expected value of $3.5$. 
## The Cauchy Distribution's Mean Values
Let's do the same experiment, only this time we will draw random numbers from the Cauchy distribution instead. 

Again we draw $N$ values. This time we'll denote them as $C_i$:

$$
C=\{C_1, C_2,...,C_N\}
$$

As before we calculate how the average value changed throughout the experiment:

$$
\bar{C}=\{\bar{C}_1,\bar{C}_2,...,\bar{C}_N\}
$$

What values do we find in this set for the Cauchy distribution? 

Unlike in our dice example, the values $\bar{C}_i$ do **not** converge on any particular value. The values $\bar{C}_i$ endlessly fluctuate, and never settle down upon any value. This is what it means for the Cauchy distribution to have no mean.

If the distribution has no mean, then what values end up in $\bar{C}$?
