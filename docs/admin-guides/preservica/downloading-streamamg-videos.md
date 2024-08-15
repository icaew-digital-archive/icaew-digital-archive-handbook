# StreamAMG Video Downloads and Metadata Export Guide

This guide provides clear, step-by-step instructions on how to download videos from StreamAMG and efficiently export metadata in bulk using StreamAMG's API and the [xml-to-csv.py script](https://github.com/icaew-digital-archive/digital-archiving-scripts/blob/main/xml_to_csv.py).

### Key Resources

Below are key links referenced throughout this guide:

- [KMC Management Console](https://kmc.mp.streamamg.com/login)
- [API Test Console](https://mp.streamamg.com/api_v3/testme/index.php)
- [API Documentation](https://mp.streamamg.com/api_v3/testmeDoc/index.php)

## Part 1: Downloading Videos from StreamAMG

Follow the steps below to download videos from StreamAMG:

### 1. Log in to the KMC Management Console

- Access the [KMC Management Console](https://kmc.mp.streamamg.com/login) and log in with your credentials.

### 2. Navigate to the Video Library

- Once logged in, go to the video library and select the videos you wish to download.

### 3. Initiate the Download

- With your videos selected, click on the "MORE ACTIONS" dropdown menu and choose the "Download" option.

![kmc-1](../../assets/images/kmc-1.png)

### 4. Choose the Download Format

- In the download options, select "Source" to download the original video file.

![kmc-2](../../assets/images/kmc-2.png)

### 5. Complete the Download

- You will receive an email with a download link. Right-click on the link and select "Save link as..." to save the file to your local device.

![kmc-3](../../assets/images/kmc-3.png)

## Part 2: Exporting StreamAMG Metadata

For best results, use Firefox for this process. The XML output might not render correctly in Chrome.

This process involves using the [API Test Console](https://mp.streamamg.com/api_v3/testme/index.php) and the [xml-to-csv.py script](https://github.com/icaew-digital-archive/digital-archiving-scripts/blob/main/xml_to_csv.py).

### 1. Obtain a "KS" String

- Open the [API Test Console](https://mp.streamamg.com/api_v3/testme/index.php).
- From the "Select service" dropdown, choose "session".
- From the "Select action" dropdown, choose "start".
- Enter your "secret" and "partnerId" (these can be found in the Integration Settings in the [KMC Management Console](https://kmc.mp.streamamg.com/login)).
- Set the "type (KalturaSessionType)" to "ADMIN".
- Click "Submit" to generate a "KS" string, which will be used in the following steps.

![api-1](../../assets/images/api-1.png)

### 2. Retrieve Metadata

- In the same API Test Console session, select "media" from the "Select service" dropdown and "list" from the "Select action" dropdown.
- Tick and edit the "pager (KalturaFilterPager)".
- Enter "500" in the "pageSize" (this is the maximum allowed).
- Enter "1" in the "pageIndex" for the first page of results. For subsequent pages, increment this number (e.g., 2, 3, 4).

![api-2](../../assets/images/api-2.png)

### 3. Save the Metadata XML

- The results will appear as an XML file. Right-click within the frame containing the XML, select "This Frame," and then choose "Save Frame As..." to save the XML file.
- Repeat this process for each subsequent page of metadata.

![api-3](../../assets/images/api-3.png)

### 4. Convert XML to CSV

- Once you have saved the XML files, use the [xml-to-csv.py script](https://github.com/icaew-digital-archive/digital-archiving-scripts/blob/main/xml_to_csv.py) to convert them to CSV format.
- The script requires specifying an `xml_file` as input and a `csv_file` as output.

By following these steps, you will successfully download videos from StreamAMG and export the associated metadata into a more manageable CSV format.
