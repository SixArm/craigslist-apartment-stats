# craigslist-apartment-stats:<br>Calculate statistics for Craigslist apartment listings

What this does:

  1. Fetch a given URL
  2. Render the HTML
  3. Filter for the number of bedrooms
  4. Calculate price statistics

Syntax:

    craigslist-apartment-stats [options] <url> ...

Example:

    craigslist-apartment-stats \
    http://sfbay.craigslist.org/search/sfc/apa?bedrooms=3&min_price=1000&max_price=9000

Options:

  * --bedrooms <number>: the number of bedrooms for the filter; default is 1.
  * -h, --help, -?: show help
  * -V, --version: show version

## Filter hints ##

The Craigslist apartment listing web pages in some cities will let you
filter by neighborhood, or price, or whether pets are allowed, and so
on. These filters can be useful for scoping your search.

## Bedroom hints ##

If you use Craigslist and its web page to filter for number of
bedrooms, then Craigslist typically shows any listings that have that
number of bedrooms or more. This is probably *not* what you want for
calculating meaningful statistics.

This script provides the bedroom filter, so you can limit the bedrooms
to exactly one number.

## Price hints ##

Listing prices may vary by large ranges, depending if the price is per
week, per month, or per year. For example, if you want statistics on
apartments that are approximately $1000 per month, then you can make a
good guess that listing prices near $250 are actuallly per week not
per month, and listing prices near $12,000 are per year not per month.

You can get improve your results by filtering for a minimum price and
maximum price. To do this, use Craigslist's website search to create a
link that includes minimum price and a maximum price.

## Requirements ##

This script requires these commands:

  * `curl` fetches the web page
  * `pup`renders the web page HTML
  * `num` calculates the stats; get it at http://www.numcommand.com

