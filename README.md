<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a name="readme-top"></a>

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#disclaimer">❗ Disclaimer ❗</a></li>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
    </li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About The Project

**No Phishing** is an advanced browser extension using artificial intelligence to detect phishing threats with 91% accuracy in real time and provides instant notifications about potential phishing threats. It's very easy to install and operate, providing a seamless browsing experience. It's designed for Google Chrome to enhance online security for both individuals and businesses.

### Disclaimer
This extension is intended as a supplementary tool for online safety. While it demonstrates high accuracy, it is not infallible. As the developer, I am not a certified cybersecurity professional, and the extension could make errors. Users are advised to exercise caution and judgment. By using "No Phishing," you acknowledge and accept responsibility for your online safety.

### Built With

* [![Python](https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue)](https://www.python.org)
* [![ChatGPT](	https://img.shields.io/badge/ChatGPT-74aa9c?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com/product)
* [![VScode](https://img.shields.io/badge/VSCode-0078D4?style=for-the-badge&logo=visual%20studio%20code&logoColor=white)](https://code.visualstudio.com/)

<p align="right">(<a href="#readme-top">back to top</a>)</p>


## ScrapeOps Proxy
This LinkedIn spider uses [ScrapeOps Proxy](https://scrapeops.io/proxy-aggregator/) as the proxy solution. ScrapeOps has a free plan that allows you to make up to 1,000 requests per month which makes it ideal for the development phase, but can be easily scaled up to millions of pages per month if needs be.

You can [sign up for a free API key here](https://scrapeops.io/app/register/main).

To use the ScrapeOps Proxy you need to first install the proxy middleware:

```python

pip install scrapeops-scrapy-proxy-sdk

```

Then activate the ScrapeOps Proxy by adding your API key to the `SCRAPEOPS_API_KEY` in the ``settings.py`` file.

```python

SCRAPEOPS_API_KEY = 'YOUR_API_KEY'

SCRAPEOPS_PROXY_ENABLED = True

DOWNLOADER_MIDDLEWARES = {
    'scrapeops_scrapy_proxy_sdk.scrapeops_scrapy_proxy_sdk.ScrapeOpsScrapyProxySdk': 725,
}

```

Then activate the ScrapeOps Proxy by adding your API key to the `SCRAPEOPS_API_KEY` in the ``settings.py`` file.

```python

SCRAPEOPS_API_KEY = 'YOUR_API_KEY'

# Add In The ScrapeOps Monitoring Extension
EXTENSIONS = {
'scrapeops_scrapy.extension.ScrapeOpsMonitor': 500, 
}


DOWNLOADER_MIDDLEWARES = {

    ## ScrapeOps Monitor
    'scrapeops_scrapy.middleware.retry.RetryMiddleware': 550,
    'scrapy.downloadermiddlewares.retry.RetryMiddleware': None,
    
    ## Proxy Middleware
    'scrapeops_scrapy_proxy_sdk.scrapeops_scrapy_proxy_sdk.ScrapeOpsScrapyProxySdk': 725,
}

```

## Running The Scrapers
Make sure Scrapy and the ScrapeOps Monitor is installed:

```

pip install scrapy scrapeops-scrapy

```

To run the LinkedIn spiders you should first set the search query parameters you want to search by updating the `profile_list` list in the spiders:

```python

def start_requests(self):
    profile_list = ['reidhoffman']
    for profile in profile_list:
        linkedin_people_url = f'https://www.linkedin.com/in/{profile}/' 
        yield scrapy.Request(url=linkedin_people_url, callback=self.parse_profile, meta={'profile': profile, 'linkedin_url': linkedin_people_url})


```

Then to run the spider, enter one of the following command:

```

scrapy crawl linkedin_people_profile

```


## Customizing The LinkedIn People Profile Scraper
The following are instructions on how to modify the LinkedIn People Profile scraper for your particular use case.

Check out this [guide to building a LinkedIn.com Scrapy people profile spider](https://scrapeops.io/python-scrapy-playbook/python-scrapy-linkedin-people-scraper//) if you need any more information.

### Configuring LinkedIn People Profile Search
To change the query parameters for the people profile search just change the profiles in the `profile_list` lists in the spider.

For example:

```python

def start_requests(self):
    profile_list = ['reidhoffman', 'other_person']
    for profile in profile_list:
        linkedin_people_url = f'https://www.linkedin.com/in/{profile}/' 
        yield scrapy.Request(url=linkedin_people_url, callback=self.parse_profile, meta={'profile': profile, 'linkedin_url': linkedin_people_url})

```

### Extract More/Different Data
LinkedIn People Profile pages contain a lot of useful data, however, in this spider is configured to only parse:

- Name
- Description
- Number of followers
- Number of connections
- Location
- About
- Experienes - organisation name, organisation profile link, position, start & end dates, description.
- Education - organisation name, organisation profile link, course details, start & end dates, description.

You can expand or change the data that gets extract by adding additional parsers and adding the data to the `item` that is yielded in the `parse_profiles` method:


### Speeding Up The Crawl
The spiders are set to only use 1 concurrent thread in the ``settings.py`` file as the ScrapeOps Free Proxy Plan only gives you 1 concurrent thread.

However, if you upgrade to a paid ScrapeOps Proxy plan you will have more concurrent threads. Then you can increase the concurrency limit in your scraper by updating the `CONCURRENT_REQUESTS` value in your ``settings.py`` file.

```python
# settings.py

CONCURRENT_REQUESTS = 10

```

### Storing Data
The spiders are set to save the scraped data into a CSV file and store it in a data folder using [Scrapy's Feed Export functionality](https://docs.scrapy.org/en/latest/topics/feed-exports.html).

```python

custom_settings = {
        'FEEDS': { 'data/%(name)s_%(time)s.csv': { 'format': 'csv',}}
        }

```


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/cprite/cover-letter-builder.svg?style=for-the-badge
[contributors-url]: https://github.com/cprite/cover-letter-builder/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/cprite/cover-letter-builder.svg?style=for-the-badge
[forks-url]: https://github.com/cprite/cover-letter-builder/network/members
[stars-shield]: https://img.shields.io/github/stars/cprite/cover-letter-builder.svg?style=for-the-badge
[stars-url]: https://github.com/cprite/cover-letter-builder/stargazers
[issues-shield]: https://img.shields.io/github/issues/cprite/cover-letter-builder.svg?style=for-the-badge
[issues-url]: https://github.com/cprite/cover-letter-builder/issues
[license-shield]: https://img.shields.io/github/license/cprite/cover-letter-builder.svg?style=for-the-badge
[license-url]: https://github.com/cprite/cover-letter-builder/blob/master/LICENSE.md
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/niknmirosh
