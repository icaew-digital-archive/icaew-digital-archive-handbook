# Downloading WARC files from Archive-It 

## Installation and configuration

The easiest method to download the WARC files from Archive-It is to use the [py-wasapi-client](https://github.com/unt-libraries/py-wasapi-client) tool.

It is installed via pip (best practice is to do it in a virtual environment):

        pip install py-wasapi-client

Basic usage is explained in the documentation on the Github page. It is best to setup a configuration file at ~/.wasapi-client like the following:

        [icaew]
        username = craig.mccarthy@icaew.com
        password = PASSWORD

## Example commands

Get a MD5 file manifest of all WARC files on Archive-It:

        wasapi-client --profile icaew --manifest

This gets the number of WARC files available after 2022-01-01:

        wasapi-client --profile icaew --collection 16306 --log /tmp/out.log --crawl-time-after 2022-01-01 --count

This will download the above:

        wasapi-client --profile icaew --collection 16306 --log /tmp/out.log --crawl-time-after 2022-01-01 -p 1


## Determining which WARC files need backing up from Archive-It to Preservica

There are regular crawls on Archive-It that will need to be backed up onto Preservica - at the time of writing the Insights Daily Summary and the public ICAEW.com capture.

The process for determining which WARC files need to be transferred is as follows:

- Run the get_asset_checksum_values.py script using the folder reference for "WACZ/WARC Files" (currently: f127c4de-f82f-4d8d-a7f7-d7552cdd4e97). This will output a list of MD5 checksums for all of the WARC files stored in Preservica.
- Run the wasapi-client --profile icaew --manifest command as outlined above. This will output a list of MD5 checksums for all of the WARCs stored in Archive-It.
- Run the preservica-archive-it-checksum-cross-reference.py script to compare the lists of checksums.
- Run the following bash script to download the missing files:  

        #!/bin/bash

        # Path to the text file to loop through
        file_path="/home/digital-archivist/Documents/apps/py-wasapi-client/files-not-present-in-preservica.txt"

        # Loop through each line in the file
        while read line; do

        # Extract the substring from the line (using sed command)
        sub_string=$(echo "$line" | sed 's/.*\(substring\).*/\1/')

        # Use the substring in a shell command (replace with your own command)
        # Replace the above echo statement with your own shell command that uses the sub_string
        echo "Downloading $sub_string"
        wasapi-client --profile icaew --filename $sub_string


        done < "$file_path"

The following collection IDs can be ignored:  

- 16126 (DELETEME-The Business Finance Guide - Local Brozzler)
- 14885 (DELETEME-ION (Public) - OLD)
- 14886 (DELETEME-ION (Excel Community) - OLD)
- 14752 (DELETEME-Insights - Daily Summary (Broken 2))
- 13348 (DELETEME-Insights - Daily Summary (Broken 1))