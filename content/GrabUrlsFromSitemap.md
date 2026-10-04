---
layout: post
title: Grab All URLs Using Sitemaps
tags:
  - technology
---

For simple sites that are not too large, you can use a tool like [this one.](https://robhammond.co/tools/xml-extract) 

### How do I grab all URLs from a Site?
Prereq:
* [WSL2](https://docs.microsoft.com/en-us/windows/wsl/install-win10) or a Linux Environment with grep (usually built in)
* A website with a *sitemap index*
---

##### Step 1: Find the sitemap
Sitemaps contain all the links from a site for search engines to use. You can locate it from common locations, robots.txt, or online tools.
[Here](https://www.seerinteractive.com/blog/how-to-find-your-sitemap/) is a link to an article that can help you find a sitemap.
<br/>
<br/>
<br/>

##### Step 2: Get the sitemap files
Sites that have pages in the thousands or more will use a sitemap index. This is a list to gzipped files that contain the actual sitemap files.
[Ballotpedia](https://ballotpedia.org/wiki/sitemap/sitemap-index-ballotpedia.xml) is  an example. Copy the links for the gzip files (.gz) and open it with a tool like [7zip](https://7-zip.org) and drag it to a location, preferably its own folder. You will have to do this manually, and yes it is annoying, but it should not take you that long.
<br/>
<br/>
<br/>
##### Step 3: Extract the links
Using WSL2 (or just a terminal if you are on linux), navigate in your terminal to where you put your sitemap files and enter the following command with each sitemap file that you have. Replace `sitemapname.xml` with the name of the sitemap file that you extracted, and `outputfile.txt` with what you want your output file to be named. <br/>

`grep -Po '<loc>\K.*?(?=</loc>)' sitemapname.xml > outputfile.txt`

<br/>
<br/>
<br/>

##### That's it!
You will have files that contain all the links to each page on the website.
