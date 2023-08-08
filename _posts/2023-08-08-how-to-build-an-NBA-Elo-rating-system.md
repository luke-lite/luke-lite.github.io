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

The Elo rating system is named for the creator Arpad Elo. Originally designed to rank chess players, it can be used for any head-to-head competition. The Elo system I have created is based on the one used by FiveThirtyEight. They have a great article titled [How we Calculate NBA Elo Ratings](https://fivethirtyeight.com/features/how-we-calculate-nba-elo-ratings/) that I highly recommend reading, but it does not provide any actual code or implementation, so that is what I will do. There are a few basic rules that determine how the Elo system works:

-
