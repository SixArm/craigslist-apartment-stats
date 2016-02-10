# craigslist-apartment-stats:<br>Calculate statistics for Craigslist apartment listings

What this does:

  1. Fetch a given URL
  2. Render the HTML
  3. Filter for the number of bedrooms
  4. Calculate price statistics

Syntax:

    craigslist-apartment-stats <url> [ ( -b | --bedrooms) <number> ]

Example:

    craigslist-apartment-stats http://sfbay.craigslist.org/search/sfc/apa --bedrooms 1

Example URIs:

  * New York: Brooklyn: Apartments (by owner, broker fee, broker no fee)
    http://newyork.craigslist.org/search/brk/aap?bedrooms=1

  * San Francisco: Noe Valley neighborhood:
    http://sfbay.craigslist.org/search/sfc/apa?nh=21&housing_type=1&bedrooms=1

  * San Francisco Bay Area: Peninsula: Palo Alto:
    http://sfbay.craigslist.org/search/pen/apa?nh=83&bedrooms=1

The default search uses these settings:

  * San Francisco, because it's where most users are searching.
  * Downtown neighborhood, because this is a good baseline for the city.
  * One bedroom, because this is a good baseline for multipliers.


This script requires:

 * `curl` fetches the web page
 * `html2text`renders the web page HTML
 * `num` calculates the stats; get it at http://www.numcommand.com

Heuristics:

  * Skip prices less than $200 because these are typically weekly prices.
  * Skip prices greater than $10000 because these are typically home purchases.
  * Skip any listings after "Few LOCAL results found".
