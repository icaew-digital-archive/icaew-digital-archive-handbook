# Downloading content from the Internet Archive Wayback Machine 

* The first step is to obtain an index of pages captured by the public IA crawls via the Internet Archive Wayback CDX Server API. Information and documentation can be found here: [Wayback CDX Server API](https://github.com/internetarchive/wayback/tree/master/wayback-cdx-server)  
  An example API query could be: http://web.archive.org/cdx/search/cdx?url=icaew.com&output=json&matchType=domain&filter=mimetype:application.*
    
* However, obtaining the index for a large site can produce a response with many lines and will often crash the browser when queried directly through the browser address bar.
    
* To overcome this limitation, one of the best methods is to request the index using wget and then save the resulting response into a local json file. The json file can be read and/or filtered using Python scripts.
    
* An example wget request:  
 
        wget 'http://web.archive.org/cdx/search/cdx?url=icaew.com&matchType=domain&output=json' -O icaew-com-index.json
        
    This request matches all captured URLs from the icaew.com domain (including sub-domains) and then outputs the result to icaew-com-index.json

* The second step is to use the [ia_cdx_json_to_txt.py ](https://github.com/craiglmccarthy/web-archiving-scripts/blob/main/downloading%20items%20from%20internet%20archive/ia_cdx_json_to_txt.py) script to convert the local json file to a list of URLs which can be given to wget (or another downloader/crawler). Usage of this script is explained in the description.
