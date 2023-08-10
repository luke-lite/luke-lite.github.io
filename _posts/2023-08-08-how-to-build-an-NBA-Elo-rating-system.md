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

The last variable is $K$, also known as the K-factor. The K-factor determines the magnitude of the rating change. If the K-factor is large, teams will win or loss a much larger number of rating points after each game. If the K-factor is small, the Elo ratings will only change a small amount. Since Elo is designed to measure the win probability of each competitor, it is important that the K-factor allow for an accurate depiction of a competitors current skill.

The K-factor is commonly set in the 20-30 range, depending on the competition, but it is challenging to determine the "best" K-factor. In fact, in chess the K-factor used by the sport's competitive bodies has changed throughout history. Arpad Elo originally set it at $K=10$, but the modern systems are significantly more complex. Some systems have different tiers of Elo ratings, and a different K-factor is used depending on which Elo range the competitor is in.

There are also a number of adjustments that can make the K-factor a variable instead of a fixed constant. The FiveThirtyEight Elo system uses margin of victory to affect the size of the K-factor. The formula is:

$K = \frac{20(MOV+3)^.8}{7.5 + 0.006(ED)}$

$MOV$ is the margin of victory (the difference in final score between the home and away team), and $ED$ is the difference in the two teams' Elo prior to the competition. The constants I have used match those used by FiveThirtyEeight system. The result is a K factor that increases or decreases the amount of points gained/lost based on the margin of victory, but only up to a certain point. The assumption is that there is a pretty big difference betwen a 5-point win and a 15-point win, but there is less of a difference between a 25-point win and a 35-point win, so as the overall margin of victory grows, there are diminishing returns on the amount of extra rating points gained/lost.

Another adjustment I use is home-court advantage. There is a notable home-court advantage in the NBA; over the past 10 seasons, the home team has won 57.2% of all regualr season games. It is possible to add complexity to this by creating team-dependent modifiers, but my system has a constant value of 100 for the home team. This means that before predicting the winner or calculating the new Elo ratings, I add 100 points to the home team's rating.

So in total, all I need to calculate Elo rating is each team's initial Elo, the home and away team, and the final score. But there is one final consideration: seasonal adjustments. NBA rosters and staff can change dramatically over the course of an off-season, so the system needs some way to account for these potential changes. One option is to fully reset each teams Elo at the start of a new season. The baseline for my Elo system is 1500, which represents the score of an "average" NBA team. Alternatively, you could make no seasonal adjustments. More often than not, good teams remain good, and bad teams remain bad, but whenever that is not the case, the system will be very slow to reflect a team's "true" rating, which will impact predictions in the meantime.

To account for seasonal adjustments, this Elo system does a partial reset: team's move toward the mean Elo rating of 1500, but retain 75% of their current rating. The formula is :

$new_season_elo = (0.75*elo) + (0.25*1505)$

Note that the mean is actually 1505. This is to account for league mergers, aquisitions, and expansions. The FiveThirtyEight article goes into some detail about why this is needed, but the good news is that we now have everything we need to build an Elo system. It is possible to increase the complexity of the system even further by adding adjustments for things like elevation, back-toback games, and road trips with consecutive games as the away team, but I will leave that possibility for another time. Now I need to write some code that will implement this system.

