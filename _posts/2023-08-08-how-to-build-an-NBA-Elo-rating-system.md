---
title: "How to Build an NBA Elo Rating System"
last_modified_at: 2023-08-08T16:22:02-05:00
classes: wide
categories:
  - Blog
tags:
  - python
  - nba
  - statistics
---
_A simple and effective way to predict NBA game winners._

![]

I recently worked on a project to predict the outcome of NBA games. I had data on tens of thousands of games, a variety of machine learning modeling techniques, and I ran countless tests to try and find the best method. But at the end of the day, the simplest method turned out to be one of the most effective: an Elo rating system. I will show you how to build an Elo system from scratch, including the math behind it and the code required to run it. While I used this system to predict NBA games, Elo systems are effective for a variety of competitions, and can be adjusted with relative ease.

**Note:** this article assumes a basic understanding of python.
{: .notice--primary}

The Elo rating system is named for the creator Arpad Elo. Originally designed to rank chess players, it can be used for any head-to-head competition. The Elo system I have created is based on the one used by [FiveThirtyEight](https://fivethirtyeight.com/). They have a great article titled [How we Calculate NBA Elo Ratings](https://fivethirtyeight.com/features/how-we-calculate-nba-elo-ratings/) that I highly recommend reading, but it does not provide any actual code or implementation, so that is what I will do. There are a few basic assumptions that determine how an Elo system works:

- all that is needed is each team's Elo rating and the game outcome
- competitors gain Elo rating points following a victory, and lose points following a loss.
- the system is zero-sum, meaning that the points gained by the victor will be equal to the points lost by the loser.

It's a surprisingly simple system, but has been proven to be very effective at ranking competitors and predicting match outcomes. The formula used to calculate a competitor's new Elo rating looks like this:

$R_1 = R_0 + K(S-E)$

$R_0$ is a team's current Elo rating, $R_1$ is the team's updated Elo rating after the game, $K$ is the constant used to determine the magnitude of the rating change, $S$ is the score/result, and $E$ is the expected win probability. For an NBA game, $S$ is either 1 for a win, or 0 for a loss. If a draw is possible, like in chess, then $S$ would be 0.5. $E$, the expected win probability, is slightly more complicated:

$E_a = \frac{1}{1+10^\frac{elo_b - elo_a}{400}}$

where $elo_a$ is the team's current Elo and $elo_b$ is their opponent's current Elo. What does this mean in practice? If two teams have the exact same rating going into a match then the expectation should be that each team has an equal chance at winning. As we can see in the formula, if the Elo's are equal, then the denominator equals $1+10^0$, which makes $E_a=1/2$. Each team is expected to win 50% of the time. Likewise, if team A has a higher Elo rating than their opponent, they should have a higher expected win probability. For example, if team A's Elo is 1600, and team B's Elo is 1400, then

$\frac{1}{1+10^\frac{-200}{400}}$ -------> $\frac{1}{1+10^-0.5}$

As in the example above, if team A has a higher Elo, the power in the denominator is negative, resulting in a positive fraction:

$$\frac{1}{1.316} = .759$

So the expected win probability is 75.9%. As the difference in Elo increases, the fraction becomes smaller, resulting in a much higher win probability. It is the exact opposite if team A's Elo is lower than team B's. The expected win probability will be somewhere below .5, depending on the difference in Elo rating.

