## Activity File: Exploring Kibana

* You are a DevOps professional and have set up monitoring for one of your web servers. You are collecting all sorts of web log data and it is your job to review the data regularly to make sure everything is running smoothly. 

* Today, you notice something strange in the logs and you want to take a closer look.

* Your task: Explore the web server logs to see if there's anything unusual. Specifically, you will:

---

### Instructions

1. Add the sample web log data to Kibana.

2. Answer the following questions:

    - In the last 7 days, how many unique visitors were located in India?  `228`

    - In the last 24 hours, of the visitors from China, how many were using Mac OSX? `10`

    - In the last 2 days, what percentage of visitors received 404 errors? How about 503 errors? `0`
    - In the last 7 days, what country produced the majority of the traffic on the website? `China`
    - Of the traffic that's coming from that country, what time of day had the highest amount of activity? `10 AM`
    - List all the types of downloaded files that have been identified for the last 7 days, along with a short description of each file type (use Google if you aren't sure about a particular file type). 
    ```
    1. CSS - Cascading style sheets is a styling language used for styling websites. 
    2. deb - This is a software installation files which is used by debian based operating system. 
    3. gz - This file type is for compressed files. A group of files compressed into a single file with this file type.
    4. rpm - Red Hat Package manager used by the linux distribution to install applications. 
    5. zip - Similar to the gz file, the zip file extension is also used for a compressed file. 
    ``` 

3. Now that you have a feel for the data, Let's dive a bit deeper. Look at the chart that shows Unique Visitors Vs. Average Bytes.
     - Locate the time frame in the last 7 days with the most amount of bytes (activity) `2021-01-24 within 3 hours timeframe`
     - In your own words, is there anything that seems potentially strange about this activity? `The avg bytes are above 22,000 by the number of visitors is just 3. Could be a possible DDOS attack. Considering a single request during that timeframe, India has 15,000  avg bytes`

4. Filter the data by this event.
     - What is the timestamp for this event? `2021-01-24 21:57:30`
     - What kind of file was downloaded? `.rpm files were downloaded`
     - From what country did this activity originate? `India`
     - What HTTP response codes were encountered by this visitor? `200`

5. Switch to the Kibana Discover page to see more details about this activity.
     - What is the source IP address of this activity? `35.143.166.159`
     - What are the geo coordinates of this activity? ` "lat": 43.34121, "lon": -73.6103075`
     - What OS was the source machine running? `win 8`
     - What is the full URL that was accessed? `https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-6.3.2-i686.rpm`
     - From what website did the visitor's traffic originate? `http://facebook.com/success/jay-c-buckey`

6. Finish your investigation with a short overview of your insights. 

     - What do you think the user was doing? `The user seems to be accessing the facebook website`
     - Was the file they downloaded malicious? If not, what is the file used for? `Does not look like the file was malicious as it was downloaded from a authentic source. The file being downloaded is the a metricbeat installer.`
     - Is there anything that seems suspicious about this activity? `The two URLs don't make sense. Why would someone while accessing the facebook profile want to download a metricbeat file.`
     - Is any of the traffic you inspected potentially outside of compliance guidlines? `This could possibly be a SSRF attack where the inital request was made to the facebook profile page which inturn is making call to a different domain to download a file. Such requests should not be allowed as it could potentially expoit the web server and the client machine.`
