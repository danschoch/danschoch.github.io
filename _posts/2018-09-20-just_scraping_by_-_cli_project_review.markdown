---
layout: post
title:      "Just Scraping By - CLI Project Review"
date:       2018-09-20 06:00:44 +0000
permalink:  just_scraping_by_-_cli_project_review
---


I realized pretty quickly heading into my first portfolio project that I had a decent grasp on Object-Oriented Ruby and how to formulate clear, consise code for most of the project. The thing I knew I would struggle with was data scraping. I didn't help myself by choosing a very dynamic, complicated website that was heavy on Javascript components that I know nothing about at this point. However, I made it through and at least have a fully functional program that accurately scrapes what I need. Here are a few tricks I picked up along the way.

- Writing the rest of your program first helps A LOT. I spent about four days of pretty much full-time work on this. Half was spent building the scraper class I needed. Not only does using sample code before you build your scraper allow you to play with what data you actually want to scrape, but it provides huge self-esteem boost if you struggle with scraping like I do. Knowing that if I could just turn the corner and get the scraper working would mean that I was practically done with my project kept me working on it for long hours. I may very well have given into frustration if I knew that the scraper was only the beginning.

- Google Chrome is your friend (Part 1): Chrome's web inspector was a life saver. I spent the beginning of my time indentifying and plugging in CSS selectors one at a time. However, once I felt comfortable that I knew what I was doing, I discovered the inspector's shortcut for copying selectors. While you still need to know how to effectively use this tool, it saved me a bunch of time. If I was trying to parse a table with different pieces of data that I needed, I could copy the CSS selector for the table in 5 seconds and immediately set to the task of pulling out the individual data. This was incredible considering the complexity of this site and how many levels down in the HTML I was going to find what I needed.

- Google Chrome is your friend (Part 2): As mentioned above, I happened to pick a site that was heavy on Javascript. This was incredibly frustrating when trying to find the selectors that I needed to parse the HTML and return the value I expected. After some searching around, I found a Chrome extension called "Disable Javascript" that did just that. I was able to turn off the Javascript actions on the page and inspect a static site, where I was able to easily identify the elements I needed. I'm sure this won't be the last time that I'm saved by a tool on the Chrome Web Store.

- Set up a console to test selectors before you do anything else. Whether you use pry or the bundler gem console (like I did), scraping is, more than anything, educated guessing and testing. The only way to get through it is to try as many combinations of selectors as quickly as you can. The console is your friend when scraping. Get to know it well.


