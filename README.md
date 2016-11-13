# United States 2016 Election, Primaries and Exit Polls results

These are csvs of results scraped from Politico and (for exit polls) CNN websites.

For more about the ethics of scraping, see [this Quora post](https://www.quora.com/What-is-the-legality-of-web-scraping). I used Selenium, which automated the Google Chrome browser, so I put no more load on their servers than a normal visitor. The only thing the program did faster than a human is parse the results.

Note that the use of Selenium was crucial because, in the case of Politico, the Outer HTML only loaded completely when the browser reached the bottom of the page, so a scraper that could "tell" the website it was really a browser and had scrolled all the way down was necessary.

I make no warranty as to the accuracy of the data, either of the source data itself or of my scraping (although I did my best and tried to validate the completeness of my results). Please contact me if you find any issues not listed here.

The following are known issues with the data (some are due to Politico just not having the data; CNN, in some cases, does, but I'm too tired to build a new scraper to resolve these few problems):

* In South Dakota, the Presidential and Senate primaries have a "Shannon County" while the general elections have an "Oglala Lakota County"
* Missing Kansas Presidential Primary by county
* Missing North Dakota Presidential Primary by county
* Colorado, Wyoming and Maine Republican primary results are not reported
* No page exists for Louisiana Senate or House Primary
* Missing Illinois 5th district Republican House Primary
* Politico has a "missing something" box in Illinois 12th district House Primary, but both Democratic and Republican primary results are present.
* Politico's page for Virginia House Primary lists individual district results for only the 2nd, 45h and 6th districts.
* Minnesota's Presidential Primary is reported by congressional district, while its Presidential General Election is reported by county
* Washington's open primaries for senate and house means that by county or district, the primaries are not divided between political parties

Note that if there is only one candidate with is_winner == True and votes == NaN, they ran uncontested.

Note that the number of votes is reported as a float instead of an integer due to a particularity of the pandas/pydata ecosystem: since they contain NaNs (the uncontested winners mentioned in the previous note), and NaNs are dtype float, the column cannot be integer.

For the curious, the Jupyter notebooks I used to scrape the data are in the ``notebooks`` folder. They're not beautiful, but they work.
