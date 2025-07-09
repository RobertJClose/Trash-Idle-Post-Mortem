# Trash Idle - Development
So I'd decided that the simplest way to bring the Cauchy distribution into a game was as a currency in an idle game. Here are some of the games I had in mind as I started on Trash Idle:

* **[Cookie Clicker](https://cookieclicker.com/)**
* **[AdVenture Capitalist](https://en.wikipedia.org/wiki/AdVenture_Capitalist)**
* **[(the) Gnorp Apologue](https://store.steampowered.com/app/1473350/the_Gnorp_Apologue/)** - My personal favourite
* A browser game where you grow larvae into many different classes of insect. Sadly I cannot remember the name of this game.

![](./Media/GnorpApologue.jpg)
***(the) Gnorp Apologue***
# How Trash Idle Works
For my idle game, I knew from the protagonist artwork that the simple interaction would be typing. I honestly think it's fun to just mash away at the keyboard sometimes. 

I then started exploring lots of ideas for a full-blown idle game. *However*, the jam's deadline intervened, and I had to strip back to the simple working core of what I had made. It's not exactly what I wanted to make, but actually the simple result is a good demonstration of the Cauchy distribution in action.

![](./Media/GameScreenshot.png)
*Trash Idle*

The game works like this:

1. The large bar under the protagonist automatically fills over time, and the player can type to make it fill faster. The amount that the bar fills is a uniform roll in the range \[0, 0.8\].
2. When the large bar is full, it resets to zero and a small amount of progress is added to the bar over the PC. The fill amount here is also a uniform roll.
3. When the bar over the PC is full, the player has created some trash! The reward is then some money. A uniform roll is made to decide which currency the player will get, and each currency is equally likely. 
4. Once the currency has been decided, we make a final random roll to decide how much of that currency the player will get. 

Each currency uses a different function:

The amount in 元 元 元 is drawn from the standard Cauchy distribution. The currency here is an alternative symbol for Chinese yuan. I chose it just because of how it looks.

The amount in £ £ £ is a uniform number in the range \[0, 1\].

The amount in $ $ $ is decided by something called a Lorentzian function. I copied the equation from the Cauchy distribution Wikipedia page at the last minute, knowing very little about it. After observing the game, I really wish I'd have used a Normal distribution instead. We will understand why later.

[Part Three](./Post-mortem%2003.md)