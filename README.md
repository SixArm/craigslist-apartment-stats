# craigslist-apartment-stats:<br>Calculate simple statistics for Craigslist apartment listings.

What this does:

  1. Fetch a given URL
  2. Render the HTML
  3. Filter for the number of bedrooms
  4. Calculate price stats

Example:

    craigslist-apartment-stats http://sfbay.craigslist.org/search/sfc/apa

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

Command: craigslist-apartment-stats
Version: 3.0.0
Created: 2014-12-24
Updated: 2016-02-10
License: GPL
Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
#
set -euf
uri=${1:-"http://sfbay.craigslist.org/search/apa"}
shift

bedroom="1"

while [ "$1" != "" ]; do
  case $1 in
    -b | --bedroom )
      shift
      bedroom=$1
      ;;
     *)
      printf "Unknown option %s\n" "$1"
      exit 1
      ;;
  esac
done

echo "min max range mean standarddeviation skewness kurtosis"
curl "$uri" |
html2text -nobs -width 10000 |
sed '/Few LOCAL results found/,$d' |
sed -n "s/^.* &#x0024;\([^ ]*\) \/ ${bedrooms}br - .*$/\1/p" |
awk '$1 > 200 && $1 < 10000 {print $1}' |
num min max range mean standarddeviation skewness kurtosis
