# Web crawl process overview

This page outlines how to create a full archival capture of ICAEW.com. However, the methods and techniques will be applicable for archiving other websites.

## Overview

A complete capture of ICAEW.com is completed by the following steps:

- Media Library download from the backend of Sitecore
- Saving a copy of the ICAEW.com sitemap
- Pre-crawl work
- wget crawl
- Public and private crawls of ICAEW.com using [browsertrix-crawler](https://github.com/webrecorder/browsertrix-crawler)
- Verifying the capture using warc-reader.py
- Adding details to the web-crawl-log

## Media Library download

Log into the backend of Sitecore [here](http://master.icaew.com/sitecore/login).

The login credentials can be found at the [Logins page](../../logins.md).

Navigate to the Media Library by selecting it via the bottom toolbar.

![media-lib-1](../../assets/images/media-lib-1.png)

Right click the root level folder, i.e., “Media Library”. Select Scripts and then Download. The process will take quite a while and will result in a ~10 GB zip file that contains the media content that is being stored directly in Sitecore. It will not download items that a linked to from other media content providers such as Vimeo and StreamAMG.

![media-lib-2](../../assets/images/media-lib-2.png)

You should see the following -

![media-lib-3](../../assets/images/media-lib-3.png)

![media-lib-4](../../assets/images/media-lib-4.png)

Once the download is complete, ingest to Admin/Private Repository/Web Captures/Sitecore Media Library Downloads, following the established naming convention for the file.

## Saving a copy of the ICAEW.com sitemap

A copy of the sitemap is saved for multiple reasons:

- To help the crawls via input to wget and browsertrix-crawler
- For post-crawl testing, to ensure all URLs have been crawled
- For future reference, as a record of what the crawls/WARC files contain

The following script can be used to produce the sitemaps in .txt format - [https://github.com/craiglmccarthy/web-archiving-scripts/blob/main/sitemap%20tools/sitemap_xml_to_txt_or_html.py](https://github.com/craiglmccarthy/web-archiving-scripts/blob/main/sitemap%20tools/sitemap_xml_to_txt_or_html.py).  

The script requires the 'requests' library to be install via:  

        pip install requests

### Example sitemap_xml_to_txt_or_html.py usage

The following outputs a list of URLs from the sitemap to a text file with pages that contain "sprint-test-pages" or "active-members":

        python3 sitemap_xml_to_txt_or_html.py --to_file 202XXXXX_sitemap.txt https://www.icaew.com/sitemap_corporate.xml https://www.icaew.com/sitemap_careers.xml  --exclude_strings "sprint-test-pages" "active-members"

The .txt file should be ingested into Preservica at Admin/Private Repository/Web Captures/ICAEW-com-sitemaps

## Pre-crawl work

- Request a list of new templates that may have been added to the site since the last crawl. Check for problems that they may present for capture/playback in the Wayback Machine via pywb.
- Template file is located here - [sitecore templates and examples](https://icaew-my.sharepoint.com/:w:/p/meiyau_kan/ETvHzfz8y71HhgAdlkexAQsBCb8GX7d7tbLw8PhgJP8_BQ?e=4%3A3fO47O&at=9&wdLOR=cB1B39863-CDBA-40B0-8F06-935A151FA8D8)

## Wget crawl

To be used in conjunction with the Get cookies.txt LOCALLY browser extension.

- Login to the ICAEW.com as normally via a browser that has the [Get cookies.txt LOCALLY](https://chrome.google.com/webstore/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc) extension installed.
- Once logged in export the cookies via the Get cookies.txt LOCALLY extension, rename the cookies file to cookies.txt and move to the folder where you want the wget download to begin.
- Test that the cookies file works by using the following command. This uses a known logged in/restricted page to test whether wget has a successfully logged in session. This "known" logged-in page will need to be reviewed periodically.  

        wget --load-cookies cookies.txt --keep-session-cookies --page-requisites --adjust-extension --span-hosts --convert-links --restrict-file-names=windows https://www.icaew.com/technical/technology/tech-faculty/chartech-magazine/chartech-2020/chartech-november-december-2020/blockchain-moves-into-the-mainstream

- Once confirmed to be working, the following command will crawl ICAEW.com, replace “202XXXXX_sitemap.txt” with the latest sitemap obtained from the earlier stage in the crawl process.

        wget --load-cookies cookies.txt --keep-session-cookies --recursive --page-requisites --adjust-extension --span-hosts --convert-links --restrict-file-names=windows --domains icaew.com --no-parent icaew.com/ --reject-regex '(.*(l|L)(o|O)(g|G)((o|O)(f|F)(f|F)|(o|O)(u|U)(t|T)).*)|(.*membership\/active-members.*)|(^(http(s)?:\/\/)?(www\.)?(train|volunteer)\.icaew\.com\/?(?:(?!blog(\/)?).)+$)' --exclude-domains access.icaew.com,annualreturns.icaew.com,apps.icaew.com,dataprotection.icaew.com,demo.icaew.com,ebookshop.icaew.com,ebm.icaew.com,economia.icaew.com,elearning.icaew.com,events.icaew.com,examresults.icaew.com,fdw.icaew.com,find.icaew.com,ion.icaew.com,jobs.icaew.com,latest.icaew.com,learningshop.icaew.com,libcat.icaew.com,membersearch.icaew.com,my.icaew.com,recruit.icaew.com,review.icaew.com,students.icaew.com,uatapps.icaew.com,uatcdn.icaew.com,uatcloudcdn.icaew.com,uatevents.icaew.com,uatmy.icaew.com,vacancies.icaew.com,www.ion.icaew.com --random-wait -i '/mnt/fc6d53c3-3dad-406c-a8ff-222b171f9208/wget-icaew-com-logged-in-july-2022/202XXXXX_sitemap.txt

- Wget may find further subdomains, add the newly found subdomains to the --exclude-domains if needed.
- When complete, ingest into Preservica at Admin/Private Repository/Web Captures/Wget Captures

## browsertrix-crawler

### Public crawl

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse neque lacus, lacinia nec justo ac, mattis semper nisl. Integer scelerisque sem ornare, ornare eros varius, ullamcorper eros. In rhoncus sodales libero sed lacinia. Sed malesuada pretium sem et semper. Pellentesque ultricies sapien justo, ut malesuada eros suscipit ut. Nullam aliquet, ante nec condimentum malesuada, enim mi placerat tortor, sit amet hendrerit enim sem sit amet tellus. Etiam sodales lacus velit, non sollicitudin enim sagittis eget. In hac habitasse platea dictumst. Aliquam semper sodales ante, non ullamcorper sapien hendrerit non. 

### Private (logged-in) crawl

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse neque lacus, lacinia nec justo ac, mattis semper nisl. Integer scelerisque sem ornare, ornare eros varius, ullamcorper eros. In rhoncus sodales libero sed lacinia. Sed malesuada pretium sem et semper. Pellentesque ultricies sapien justo, ut malesuada eros suscipit ut. Nullam aliquet, ante nec condimentum malesuada, enim mi placerat tortor, sit amet hendrerit enim sem sit amet tellus. Etiam sodales lacus velit, non sollicitudin enim sagittis eget. In hac habitasse platea dictumst. Aliquam semper sodales ante, non ullamcorper sapien hendrerit non. 

## warc-reader.py

The WARC reader script (as found here - [https://github.com/craiglmccarthy/web-archiving-scripts/blob/main/warc-reader.py](https://github.com/craiglmccarthy/web-archiving-scripts/blob/main/warc-reader.py)) is used to check the sitemap against the capture.

The script needs to be edited here:

        # URL_LIST is most likely going to be a sitemap 'snapshot'
        URL_LIST = ''
        # WARC_FOLDER_PATH is a path to a folder containing WARC files
        WARC_FOLDER_PATH = ''
        # CSV_FILENAME is the filename for the CSV output
        CSV_FILENAME = ''

The URL_LIST should point to a .txt file of URLs, i.e. the 202XXXXX_sitemap.txt created earlier in the crawl process. WARC_FOLDER_PATH should point to a folder containing WARC files. CSV_FILENAME is the name of .csv file output.

## web-crawl-log

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse neque lacus, lacinia nec justo ac, mattis semper nisl. Integer scelerisque sem ornare, ornare eros varius, ullamcorper eros. In rhoncus sodales libero sed lacinia. Sed malesuada pretium sem et semper. Pellentesque ultricies sapien justo, ut malesuada eros suscipit ut. Nullam aliquet, ante nec condimentum malesuada, enim mi placerat tortor, sit amet hendrerit enim sem sit amet tellus. Etiam sodales lacus velit, non sollicitudin enim sagittis eget. In hac habitasse platea dictumst. Aliquam semper sodales ante, non ullamcorper sapien hendrerit non. 