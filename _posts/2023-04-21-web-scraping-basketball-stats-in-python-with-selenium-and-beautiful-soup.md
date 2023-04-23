---
title: "Web Scraping NBA Stats in Python"
last_modified_at: 2023-04-21T16:22:02-05:00
classes: wide
<!-- mathjax: true -->
categories:
  - Blog
tags:
  - python
  - web scraping
  - selenium
  - nba
---
<!-- _using Selenium and Beautiful Soup_

Getting the right data is hard. In fact, it's almost always the hardest, longest, and most arduous part. I recently needed to get a huge amount of NBA stats for a project I'm working on. I knew the information existed, spread across a number of publicly available websites, but I had no easy way to directly access it. The answer was web scraping.

In this article I will demonstrate a simply web scraping example for anyone who might be new to the process. It can seem daunting at first, but with a little bit of knowledge it is very manageable. Today's example involves NBA stats, but the web scraping techniques I cover can be applied to most situations.

Web scraping is the process of accessing a webpage, and pulling (or scraping) the information you want from it. If you only need a little information from just a page or two, it is easy enough to transcribe whatever you need. The real power of web scraping comes from the ability to automate the process in order to gather huge amounts of data.

While web scraping is a powerful tool, there are several dangers to consider. One is legality. Web scraping is currently legal across the US, _as long as the information is publicly available_. This is an important distinction. If it is information on a website that anyone can access, does not contain confidential data, and does not require any kind of login or account, then it is likely fine to scrape. If one of those conditions is not met, then you need to be very careful about what kind of information you are trying to collect.

Another danger is damage to the person or company who owns the site. Web scraping involves making calls to the server that is running the site. If done incorrectly, web scraping code can make rapid, repeated calls to the server, slowing down the site's performance for all users, and in extreme cases, can temporarily shut down a website.

It is also considered good practice to check the site for any policies or TOS related to web scraping, even if the information is publicly available.  My web scraping example comes from [basketball-reference.com](https://www.basketball-reference.com/). They are the go-to site for any data-loving basketball fans, and have a massive amount of data across their site. They have a set of policies on web scraping that can be found on their parent company's website [here](https://www.sports-reference.com/data_use.html).

According to their policies, you can web scrape as long as you meet a series of requirements, including:

- not using the data for illegal activites
- not adversly impacting the performance of the website
- not using the data for profit or to create a competing product

Since today's example is just some boxscore data from a single NBA game, we are in the clear.

The first step is to find the information we want to scrape. For this example, I'm interested in getting the boxscore stats from what is considered by many to be one of the greatest basketball games of all time: Celtics vs. Suns Game 5 of the 1976 NBA Finals. After navigating the site, I manage to find what I'm looking for: 

[Game 5](https://www.basketball-reference.com/boxscores/197606040BOS.html)

You can save yourself a lot of time and frustration by being certain what kind of information is accessible on the webpage and what exactly you need from it. There's a lot of information available. I'm only interested in the boxscores for each team. Now that I have identified the data I need, we can get our code ready to scrape it.

I will be using two main packages: [Selenium](https://www.selenium.dev/selenium/docs/api/py/index.html) and [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). It is worth noting that the simple web scraping I am going to demonstrate could be done using either package by itself, but I will introduce both since they are the two premier web scraping packages. In general, Beautiful Soup is easier to use, but has less functionality than Selenium.

To start, I need to import the necessary packages:

;;;;;;;;;;;;

Now I need to take a closer look at the webpage. Interacting with the various elements of the webpage requires a little knowledge about how a webpage is displayed, but I promise to only keep things on a need-to-know basis for this demonstration. Most webpages are constructed using html or xml. There is a lot more going on, of course, but for now we will focus on that. I could pull _all_ the information from the webpage and then try to whittle it down, but it will be much easier if I know what I'm looking for. To get a better look at the webpage's underlying code, you can simply right-click on the webpage and select 'Inspect'. This will pull up a window that contains detailed information about what is happening under the hood. It may look a bit different depending on your OS and browser, but it should look something like this (Windows Chrome):

;;;;;;;;;;;

The sheer amount of information can be a little overwhelming, but we want to focus on the html elements that can be found in the highlighted region:

;;;;;;;;;;

This displays all the basic information contained on the webpage, but stripped of all visual elements. The important thing to keep in mind is that html is written using tags, indicated by <> brackets. For example, the website header is denoted by the <head> tag. Within the <head> tag might just be a single picee of text, or it may have a series of other tags nested within it, depending on the complexity of the webpage. But everything between <head> and </head> (end tags include a '/') is considered to be part of the header.

As you can see by looking through the html on this page, the nested structures can get very large very fast. Instead of searching through all the tags to find the information, we can get it directly by right-clicking the specific information we want and selecting 'Inspect'. Since I want the boxscores, I will right click the boxscore title here:
 
;;;;;;;;;;

This time, the console shows the html of the specific item we selected:

;;;;;;;;;

Great. The table's title is within the <h2> tag, which is within a <div> tag. Another great feature is that while you have the console open, if you hover your mouse over any of the html elements, the corresponding information will be highlighted in your browser. This makes it significantly easier to narrow down to exactly what you want. If you look at some of the elements near the title we inspected, you see that the actual table, which contains all the data we want, is actually in a different tag:

;;;;;;;;;;;;

Opening the path for this <div> tag shows the table nested within in, and within that, all the information in each cell, broken down by row and column. It should look something like this:

;;;;;;;;;;;

The important things to note are the various sections: <thead> contains the column headers, and <tbody> contains each <tr> (table row), and within each row is the individual <td> cells with the data. Now we know the exact html path for the data we need!

I can use Selenium to access the 





best game all time: celtics suns game 5 1976 finals -->
