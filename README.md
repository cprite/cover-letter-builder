<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a name="readme-top"></a>

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="images/logo.png" alt="Logo" width="200" height="200">
  </a>

  <p align="center">
    <br />
    <br />
    <br />
    <a href="https://github.com/cprite/cover-letter-builder/issues">Report Bug</a>
    ·
    <a href="https://github.com/cprite/over-letter-builder/issues">Request Feature</a>
  </p>
</div>


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
    <li><a href="#contributing">Contributing</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About The Project

**No Phishing** is an advanced browser extension using artificial intelligence to detect phishing threats with 91% accuracy in real time and provides instant notifications about potential phishing threats. It's very easy to install and operate, providing a seamless browsing experience. It's designed for Google Chrome to enhance online security for both individuals and businesses.

### ❗❗❗ Disclaimer
This project is developed solely for educational purposes to demonstrate the capabilities of web scraping and AI-powered content creation. Please be aware that scraping LinkedIn is against their Terms of Service. Users choosing to implement or use this program do so at their own risk and are fully responsible for complying with LinkedIn's policies and any applicable laws. This tool is not endorsed by or affiliated with LinkedIn or OpenAI. Always consider ethical guidelines and the legal implications of web scraping before use.

### Built With

* [![Python](https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue)](https://www.python.org)
* [![ChatGPT](	https://img.shields.io/badge/ChatGPT-74aa9c?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com/product)
* [![VScode](https://img.shields.io/badge/VSCode-0078D4?style=for-the-badge&logo=visual%20studio%20code&logoColor=white)](https://code.visualstudio.com/)

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- GETTING STARTED -->
## Getting Started

1. Set up proxy
   - Since Linkedin doesn't allow user's to scrap their data, you have to set up a proxy.
   - You can [sign up for a free API key here](https://scrapeops.io/app/register/main). ScrapeOps has a free plan that allows you to make up to 1,000 requests per month.
   - Get your API key and add to the `SCRAPEOPS_API_KEY` in the ``settings.py`` file.
     ```python

      SCRAPEOPS_API_KEY = 'YOUR_API_KEY'
      
      SCRAPEOPS_PROXY_ENABLED = True
      
      DOWNLOADER_MIDDLEWARES = {
          'scrapeops_scrapy_proxy_sdk.scrapeops_scrapy_proxy_sdk.ScrapeOpsScrapyProxySdk': 725,
      }
      
      ```
     
3. Set up OpenAI API
   - To use this software, you need an OpenAI API key, which powers the AI-driven features, including generating personalized cover letters based on your LinkedIn profile.
   - Sign up for an account at [OpenAI](https://openai.com/)
   - Once you have an OpenAI account, log in and go to the API section and then to API Keys sidebar sectioon. Here, you'll find your API key, which is a unique token you'll use to authenticate your requests. 
   - Get your API key by pressing Create new secret key
   - Your API key is like a password. Keep it secure and do not share it. Store it in a safe place, as you will need it to configure the software.
   - Copy your API key and add to the `OPENAI_API_KEY` in the ``linkedin/spiders/linkedin_people_profile.py`` file.
     ```python

      """
        BUILDING COVER LETTERS BASED ON THE DATA FROM LINKEDIN
        """
        desired_role = input("Enter the desired role: ")
        company = input("Enter the company name: ")
        extra = input("Enter any additional information you want to focus on in your cover-letter (optional): ")

        client = OpenAI(api_key = 'OPENAI_API_KEY')
      
      ```
   
4. Clone the repo
   ```sh
   git clone https://github.com/cprite/cover-letter-builder.git
   ```
   
5. Install the required dependencies
   ```sh
   pip install -r requirements.txt
   ```
   
6. Ready to Go!
   - To run the program, execute the following command and follow simple instructions
     ```

      scrapy crawl linkedin_people_profile
      
      ```
   - All cover letters will be saved in the program folder in cover_letters.txt file

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>


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
