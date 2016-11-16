# United States 2016 Election results (President, Senate, House, Governor), plus Primaries, Ballot Measures and Exit Polls

These are csvs of results scraped from Politico and (for exit polls) CNN websites. If anyone uses this, I'd love to hear about it! [I wrote a brief blog post describing my motivation](http://prooffreaderplus.blogspot.ca/2016/11/i-scraped-all-2016-us-election-data.html)

#### Update 2016-11-16, 18:20 EST: Politico's website had the wrong names for several third-party candidates. I have re-run the script from scratch, without errors, using only 'democratic', 'republican' and 'indepdent_or_other' for the field 'individual_party'. This issue has now been closed.

For more about the ethics of scraping, see [this Quora post](https://www.quora.com/What-is-the-legality-of-web-scraping). I used Selenium, which automated the Google Chrome browser, so I put no more load on their servers than a normal visitor. The only thing the program did faster than a human is parse the results.

Note that the use of Selenium was crucial because, in the case of Politico, the Outer HTML only loaded completely when the browser reached the bottom of the page, so a scraper that could "tell" the website it was really a browser and had scrolled all the way down was necessary.

I make no warranty as to the accuracy of the data, either of the source data itself or of my scraping (although I did my best and tried to validate the completeness of my results). Please contact me if you find any issues not listed here.

I scraped most of the info from Politico, although the exit polls were from CNN. They include:

* Both General Election and Primaries
* Presidential, Senate, House and Governor races
* Ballot Measures
* Exit Polls
* By State and by County, where possible.

Further downballot races like state legislatures were not listed.

The following are known issues with the data as present on Politico (either the data just does not exist/is not reported, or it exists and for whatever reason, Politico does not have it):

* Alaska has no Presidential General Election listed by County; perhaps Politico was confused by the fact that they call their counties "Boroughs", although they had no problem with Louisiana's "Parishes"
* Between the primaries and the election, Shannon County changed its name to Oglala Lakota County
* Missing Kansas Presidential Primary by county
* Missing North Dakota Presidential Primary by county
* Colorado, Wyoming and Maine Republican primary results are not reported
* No page exists for Louisiana Senate or House Primary
* Missing Illinois 5th district Republican House Primary
* Politico has a "missing something" box in Illinois 12th district House Primary, but both Democratic and Republican primary results are present.
* Politico's page for Virginia House Primary lists individual district results for only the 2nd, 4th, 5th and 6th districts.
* Minnesota's Presidential Primary is reported by congressional district, while its Presidential General Election is reported by county
* Washington's open primaries for senate and house means that by county or district, the primaries are not divided between political parties

If merging this data with county demographic data, be aware of the following:
* The aforementioned Shannon County change to Oglala Lakota County in South Dakota; fips has changed from 46113 to 46102
* In 2015, the county of Bedford City, VA, fips 51515, was amalgamated into Bedford County, VA, fips 51019. There is no more fips 51515, while fips 51019 now has greater area and population (and different demographics)
* Kalawao County, Hawaii, fips 15005, has a population of 90 so they count in a neighboring county's totals (I could not determine which one)
* As mentioned above, for some reason Alaska's Presidential General Election was not listed per county, and the Presidential Primaries was listed per Congressional electoral district instead of per county. So Alaska has no county data in this dataset. Blame Politico.

I have merged this data, given the caveats above, with [Deleetdk's USA.county.data repo](https://github.com/Deleetdk/USA.county.data); the results are in ``/merged_with_demog``. Note that the demog info also has some political history info, in columns (wide), while my election data is tall/normalized; if you want to compare between elections, that will take some wrangling.

Note that if there is only one candidate with is_winner == True and votes == NaN, they ran uncontested.

A word about the ``individual_party`` and ``party`` fields. ``party`` is filled out when the entire subtable is for one party, e.g. a primary. ``individual_party`` is filled out when an individual line showing a candidate lists a political party.

As mentioned above, many of Politico's third-party names were wrong. When I have time, I'll try to correct them based on the New York Times website.

Note that the number of votes is reported as a float instead of an integer due to a particularity of the pandas/pydata ecosystem: since they contain NaNs (the uncontested winners mentioned in the previous note), and NaNs are dtype float, the column cannot be integer.

For the curious, the Jupyter notebooks I used to scrape the data are in the ``notebooks`` folder. They're not beautiful, but they work. The politico one, in particular, has lots of checks for consistency, both internally and with the demographic data mentioned above.
