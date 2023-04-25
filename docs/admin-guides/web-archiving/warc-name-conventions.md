# WARC file naming conventions

Before ingest into Preservica or uploading to Archive-It, WARC files should be given a descriptive name following this naming convention – _Prefix-Timestamp-Serial-Crawlhost.warc.gz_ as recommended by: [https://iipc.github.io/warc-specifications/specifications/warc-format/warc-1.0/#annex-b-informative-warc-file-size-and-name-recommendations](https://iipc.github.io/warc-specifications/specifications/warc-format/warc-1.0/#annex-b-informative-warc-file-size-and-name-recommendations).

An example for ICAEW use is -

- Business-finance-guide-20210304135532142-001-ICAEW.warc.gz

The explanation from the WARC specification for following this naming convention is as follows:

- Prefix is an abbreviation usually reflective of the project or crawl that created this file. Timestamp is a 14-digit GMT timestamp indicating the time the file was initially begun. Serial is an increasing serial-number within the process creating the files, often (but not necessarily) unique regarding the Prefix. Crawlhost is the domain name or IP address of the machine creating the file.
