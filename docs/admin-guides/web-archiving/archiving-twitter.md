* In order to crawl a Twitter feed, an account needs to be created/logged-in. These can be found on the [Logins page](../../logins.md).

* _Note: regarding Tweet limits (from the [Twitter Help Center](https://help.twitter.com/en/using-twitter/missing-tweets)) - only the 800 most recent Tweets are displayed in the Tweets tab, while only the latest 3,200 Tweets are displayed in the Tweets and replies tab._

### archiveweb.page

* The easiest way to capture a Twitter account is via archiveweb.page, either the Chrome extension or the Electron desktop applicaton. Both tools contain Twitter specific browser behaviours for capturing Twitter feeds.
* In order to capture Tweets older than the latest 3,200 Tweets you will need to capture the advanced search results feed. For example, for 2009, you would need to capture - **https://twitter.com/search?q=(from%3AICAEW)%20until%3A2009-12-31%20since%3A2009-01-01&src=typed_query&f=live**

### snscrape

* This tool can be used to scrape all of the Tweets (surpassing the 3,200 Tweet limit) of an account and output the results into a JSON file. It can also produce a list of URLs for each Tweet which can then be given to a web crawler/wget to create a web archive.

* Example commands (the first produces a list of Tweet URLs, the second produces the entire Tweet saved in JSON):  

        snscrape twitter-user ICAEW > ICAEW-tweet-URLs.txt
        snscrape --jsonl twitter-user ICAEW > ICAEW-tweets.json

* _Note: A snapshot of the ICAEW Twitter was taken using this tool on 24/11/2022 which includes the entire history of the @ICAEW account up until the snapshot. The .txt and .json files are currently being held in the admin section of Preservica. The ICAEW-tweet-URLs.txt was supplied to the crawler to ensure that all Tweets have been crawled by a web crawler._

### twarc

* _Note: Tested, but not currently in use as does not meet our requirements._

* This tool can be used to capture the latest 3,200 Tweets in JSON format.

* To make use of [twarc](https://github.com/DocNow/twarc), a developer account needs to be setup. There is a development account setup using the same credentials as above. The login details are on [Logins page](../../logins.md).
        
* twarc is installed via (creating a virtual environment with _python3 -m venv venv_ and then activating it with _. ./venv/bin/activate_ is always a good idea):  

        pip install twarc

* Enter API credentials by running:

        twarc2 configure