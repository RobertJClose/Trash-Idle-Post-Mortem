As discussed in [[01 _ Using The Cauchy Distribution In A Game]], my initial attempts at using the Cauchy distribution as a game design element focused on random hit chances and random loot tables. I struggled to incorporate the distribution into those scenarios however. One of the issues was that in these scenarios, we typically make use of a random number between zero and one. The Cauchy distribution spans the entire real number-line however. 

A natural idea then is to use the distribution's location and scale parameters to squish the distribution almost entirely within the range of zero to one. Here is a Cauchy distribution which has been squished in the $[0,1]$ range using the location and scale parameter:

![[Cauchy_SquishedZeroToOne.png]]
*Desmos*

Once we've squished the function, we *truncate* the distribution - if we draw a value outside of the range $[0,1]$, we discard it and draw again until we have a value within the appropriate range.

We could also consider clamping the values drawn, however it is easier to study the behaviour of truncated distributions from a maths perspective, and that's what I have tried to do.

>[!Summary] The Following Analysis Is Unfinished
>I tried my best to analyse the statistical behaviour of the squished and truncated Cauchy distribution above, however I was only able to get so far. 
>I'll share as much progress as I have.
# Truncated Distributions
In order for a graph to represent a probability distribution, the area under the curve must be equal to one square-unit. This fact then allows us to interpret area-under-the-curve as the probability of drawing a number within a certain range.

![[Normal-Area.jpg]]
*[Byjus](https://byjus.com/maths/probability-distribution/))*

When we truncate a distribution, we chop off it's tails and uniformly add the lost area to the middle section of the curve that remains. This keeps the total area under the curve equal to one.

![[Modellica.png]]
*Modellica - A truncated Normal distribution*

Mathematically, the probability function is restricted by a kind of filtering function $\text{filter}(x)$, and what remains is multiplied by a scaling factor $S$.
## The Scaling Factor $S$
The scaling factor $S$ depends on where we do the truncation. Continuing with the idea that we are chopping off the tails, I'm going to parameterise the behaviour of $S$ by asking, what percentage of the tails are we chopping off? 

We represent that amount as a number between zero and one and we'll call it $p$. I'll consider $p$ to be the fraction of *each* tail that we chop off, so the total fraction lost is $2p$. The resulting equation for $S$ is this:

$$
S(p) = \frac{1}{1-2p}
$$

So if we want to chop off 50% of the graph, then we are going to lose 25% of each tail. This gives us $p=0.25=1/4$. The equation then evaluates to $\frac{1}{1/2}$, giving us a final scale factor of $\frac{2}{1}=2$.

Once we've decided a value for $p$, we can also calculate where exactly on the tails we are performing the truncation. This can be done using the distribution's *quantile* function. The quantile function is an alternative equation for representing the same distribution. The quantile function takes a probability $0 \leq P \leq 1$ and tells us the $x$ value such that the probability of drawing a value between zero and $x$ is equal to $P$. 

The equation for the Cauchy distribution is this

$$
\text{Cauchy Quantile}(P) = \tan ( \pi \cdot (P - 1/2) )
$$

The graph of this description of the Cauchy is quite different to the bell-curve.

![[Cauchy Quantile Graph.png]]

The truncation position of the bottom tail is $\text{Quantile}(p)$, while for the top tail it is $\text{Quantile}(1 - p)$. If we write the truncation position of the top tail as $x_p$, we can derive

$$
x_p = - \tan\left(\pi \cdot (p - 1/2)\right)
$$

## The Filter Function
The filter function simply restricts the range:

$$
\text{filter}(x) = 
\begin{cases} 
1 & -x_p < x < x_p \\
0 & \text{Otherwise}
\end{cases}
$$
## The Truncated Cauchy
Bringing it all together, we start with the Cauchy distribution and multiply it by the scaling factor and the filter function.

$$
\begin{align}

\text{PDF}(x)_{truncated} &= S \times \text{filter}(x) \times \text{PDF}(x) \\ \\

\text{PDF}(x)_{Cauchy} &= \frac{1}{\pi (1 + x^2)} \\ \\

S(p) &= \frac{1}{1-2p} \\ \\

x_p &= - \tan\left(\pi \cdot (p - 1/2)\right) \\ \\

\text{filter}(x) &= 
\begin{cases} 
1 & -x_p < x < x_p \\
0 & \text{Otherwise}
\end{cases}

\end{align}
$$

This tells us the probability density function of the distribution, which we may then study. 

Generating truncated-Cauchy variables is almost the same as regular Cauchy variables. We simply discard those that lie outside our desired range:

``` C#
using UnityEngine;

public float SampleTruncatedCauchy(float p, float location, float scale)
	{
		float uniformSample;
		
		do 
		{
			uniformSample = Random.value;
		} 
		while (uniformSample < p || uniformSample > 1 - p);
		
		float sample = location + scale * 
						Mathf.Tan(Mathf.PI * (uniformSample - 0.5f));
		
		return sample;
	}
```
# Properties Of A Truncated Cauchy Distribution
I wanted to make us of the Cauchy distribution because it has no mean value. Sadly, any truncation of the Cauchy distribution removes this fact and restores the mean. However, if the truncation is very conservative, the resulting distribution is *nearly* a Cauchy. In such a case, it can take a large number of samples before the sample mean converges upon the true population mean.

I'd like to quantify the above. 

---

## A Truncated Cauchy
Sadly, when we truncate the Cauchy distribution, the resulting function does have a well defined population mean. This destroys the feature of the distribution which I found most interesting, although all is not lost.

Suppose we only chop off a tiny portion of the tails, so the truncated distribution is *nearly* identical to the Cauchy distribution. Although any degree of truncation does produce a distribution with an average value, it can still take a *very* long time for a sample mean to converge onto it. Perhaps we can squish our Cauchy distribution within $[0,1]$ such that performing a truncation into that range produces a distribution whose true average value takes an impractical amount of time to appear?

---
# Calculating The Moments
##### The Standard Deviation
Let's start with $\sigma$ - the standard deviation. This is defined as the square root of the *variance*, which for a continuous probability distribution is defined as:

$$
\newcommand\dif{\mathop{}\!\mathrm{d}}
\text{Var}(X) = \int_\mathbb{R} x^2 \cdot \text{PDF}(x) \dif x - \mu^2
$$

Where $\mu$ is the mean of the distribution, and the integral is evaluated over the whole real number line. Truncating the standard Cauchy produces $\mu = 0$ so we will omit it from here.

Returning to our definition of a truncated Cauchy distribution

$$
\text{Standard Cauchy PDF}(x) = \frac{1}{\pi (1 + x^2)}
$$
$$
\text{PDF}(x)_{truncated} = S \times \text{filter}(x) \times \text{PDF}(x) 
$$
$$
S(p) = \frac{1}{1-2p}
$$

We use this value to define the filter function, which then changes the limits of the integral to give us this expression for the variance of a truncated-Cauchy

$$
\newcommand\dif{\mathop{}\!\mathrm{d}}
\text{Var}(X) = \frac{S}{\pi} \int_{-x_p}^{x_p} \frac{x^2}{1 + x^2} \dif x
$$

I'm quite proud of the fact that despite many years away from formal maths education or professional work, I was still able to do this integral myself and (up to some rearranging) I got the same answer as Symbolab

$$
\text{Var}(X) = \frac{2S}{\pi} \left( x_p - \arctan x_p \right)
$$

The standard deviation is then the square-root of the variance

$$
\sigma = \sqrt{\frac{2S}{\pi} \left( x_p - \arctan x_p \right)}
$$

The fourth moment of a truncated-Cauchy is

$$
\mu_4 = \frac{2S}{\pi} \left[ \frac{x_p^3}{3} - x_p + \arctan x_p \right]
$$

From the above we may calculated the expected variance of the sample variance from the following

$$
\langle \text{Var}(s^2) \rangle = \frac{1}{N} \left( \mu_4 - \frac{N - 3}{N - 1} \mu_2^2 \right)
$$


Oh fucking hell!

$$
\mu_n = \frac{2S}{N} \left[ \sum_{i=0}^{n}  \right]
$$
$$
\text{for } n > 0
$$


---
---
---
# Oh Dear
To test the above equation for the variance, I wrote this C# code:

* https://dotnetfiddle.net/57g4yU

The sample variance consistently differs from the equation above. I've really tried to spot any mistakes in either the equation or the code, but I haven't been able to find anything. 

At the very least, if the above code is an accurate simulation of the truncated-Cauchy distribution, then we can use it to play around with values for $p$ and $n$. We can rerun the code and watch the sample mean to get a feel for how wildly it jumps around the population mean of zero for different degrees of truncation. We can also look directly at what kind of sample variance values we get. 

Having done this, I don't feel I should spend any more time trying to work it out. My instinct is that the truncated Cauchy won't be practical as an interesting game design element, but the idea does still feel worth exploring to completion. I'm sorry to leave it here, but I thought I'd share as much progress as I have on this topic.