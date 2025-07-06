# Trash Idle Post-mortem
I recently made a game called **Trash Idle** which you can play [here](https://justrobjustrobjustrob.itch.io/trashy-idle)

![Game Screenshot](./Media/Long%20Run/619.png)

The game was my submission to the [Pompous Trash Jam 2025](https://itch.io/jam/pompous-trash-2025), and I used the occasion as an opportunity to try using an experimental game-design element that has been on my mind for some time.
# An Unusual Source Of Random Numbers
Several years ago while studying physics I came across a probability distribution with an interesting property: it has no average value. 

If you use this distribution to generate some random numbers, and you calculate the average of your samples, the resulting number can't be predicted ahead of time for this distribution. You can calculate a well defined average for *your* samples, but the resulting average will generally never agree with anyone else's samples. Drawing more samples won't help, your average value will forever jump around without purpose.

The probability distribution in question is called the **Cauchy Distribution**, and its probability density function looks like this:

![Cauchy PDF](./Media/Cauchy_Graph.png)
*Desmos*

This is a well-know shape - it's a bell-curve! It is not however, *the* bell curve known as the **Normal Distribution**. 

The Normal distribution is arguably the most important probability distribution in all of maths and science, and it has an almost universal role in modelling a massive range of situations involving random numbers. This is because of a result known as the **Central Limit Theorem**, which we will meet again later.

![Stable Distributions](./Media/StableDistributions.png)
*Desmos* - The Cauchy distribution is in red, while the Normal distribution is in blue.

Given its visual similarity to the Normal distribution, I found it hard to believe that the Cauchy bell-curve has no average value. Surely they both have their average value right there in the middle? 

What I wanted to explore was if the Cauchy distribution could be used to create some interesting experiences for players in a game. Random numbers are already a common game design-element, and I think most players are generally familiar with how randomness is used in games - could this distribution catch players by surprise? Would players be able to tell something strange is going on? 
# Structure Of This Post-mortem
I've created this post-mortem to share what I learned from making **Trash Idle**. This includes lessons about the maths of the distribution, but more importantly it includes lessons about the Cauchy distribution as a game-design element.

I've organised the post-mortem into a main-sequence of notes, which will stay as focused as possible on the game-design perspective. Throughout the main-sequence notes, I occasionally make reference to mathematical deep dives which explain the drawn conclusions - I've separated those lessons into standalone pages. Those deep dives can take time to explain, so I thought it best to keep the main reading as focused as possible.

Finally, I've also included a cheat-sheet containing all of the equations and code examples that are scattered throughout. 