<!-- ---
title: "Web Scraping NBA Stats in Python"
last_modified_at: 2023-04-21T16:22:02-05:00
classes: wide
mathjax: true
categories:
  - Blog
tags:
  - python
  - web scraping
  - selenium
  - nba
---
_using Selenium and Beautiful Soup_

Getting the right data is hard. In fact, it's almost always the hardest, longest, and most arduous part. I recently needed to get a huge amount of NBA stats for a project I'm working on. I knew the information existed, spread across a number of publicly available websites, but I had no easy way to directly access it. The answer was web scraping.

In this article I will demonstrate a simply web scraping example for anyone who might be new to the process. It can seem daunting at first, but with a little bit of knowledge it is very manageable.

Web scraping is the process of accessing a webpage, and pulling (or scraping) the information you want from it. If you only need a little information from just a page or two, it is easy enough to transcribe whatever you need. The real power of web scraping comes from the ability to automate the process in order to gather huge amounts of data.

While web scraping is a powerful tool, there are several dangers to consider. One is legality. Web scraping is currently legal across the US, _as long as the information is publicly available_. This is an important distinction. If it is information on a website that anyone can access, does not contain confidential data, and does not require any kind of login or account, then it is likely fine to scrape. If one of those conditions is not met, then you need to be very careful about what kind of information you are trying to collect.

Another danger is damage to the person or company who owns the site. Web scraping involves making calls to the server that is running the site. If done incorrectly, web scraping code can make rapid, repeated calls to the server, slowing down the site's performance for all users, and in extreme cases, can temporarily shut down a website.

It is also considered good practice to check the site for any policies or TOS related to web scraping, even if the information is publicly available.  My web scraping example comes from [basketball-reference.com](https://www.basketball-reference.com/). They are the go-to site for any data-loving basketball fans, and have a massive amount of data across their site. They have a set of policies on web scraping that can be found on their parent company's website [here](https://www.sports-reference.com/data_use.html).

According to their policies, you can web scrape as long as you meet a series of requirements, including:

- not using the data for illegal activites
- not adversly impacting the performance of the website
- not using the data for profit or to create a competing product

Since today's example is just some boxscore data from a single NBA game, we are in the clear.

The first step is to 

best game all time: celtics suns game 5 1976 finals -->
