#  🏢 Companies House API 🏦

## Table of Contents

1. [Introduction](#one-introduction)
2. [Instructions](#two-instructions)
    - Option 1 - Use the dataset prepared by GenderPayGap mentors
    - Option 2 - Run a script to collect additional data
        - Preparing your local environment
        - Customising a query - endpoint
        - Customising a query - parameters
3. [Working with the Data](#three-working-with-the-data)
    - Data structure
    - Loading data from a text file
    - Access information within the data
4. [Contributions](#four-contributions)
5. [Authour](#five-authour)

## :one: Introduction

In this section of the GenderPayGapHack, we explore the the 💷UK Gender Pay Gap Data 💷 and UK company information as returned by querying the UK Companies House API. We will initially be focusing on company officers.

[Companies House API](https://developer.companieshouse.gov.uk/api/docs/index/gettingStarted/quickStart.html) is an authoritative source of company information: it provides a single API that exposes all company information delivered under the Companies Act and related legislation.

To be able to explore and query the Companies House API, you need to register a free [user account](https://account.companieshouse.gov.uk/oauth2/user/signin) with Companies House, and then generate an API key for use in each API request. 

Rate limiting is applied to the Companies House API: You can make up to 600 requests within a five-minute period. If you exceed this limit, you will receive a `429 Too Many Requests` HTTP status code for each request made within the remainder of the five-minute window. At the end of the period, your rate limit will reset back to its maximum value of 600 requests. This should be more than enough for you to play around on the day of the hack. However, please be aware that it _is_ possible to accidentally exceed the limit, e.g. by entering an infinite loop whilst making batch requests... :see_no_evil:

## :two: Instructions
There are two options for you to work on this topic.

### Option 1 - Use precollected dataset

Mentors of the GenderPayGapHack joined force :muscle::boom:

We analysed a large number of APIs, hand-picked ones that suited our purpose, and have created ready-to-use datasets.

In case of Companies House API, we collected officer information for each currently active officer of the 10,000+ companies that supplied the data that makes up the UK Gender Pay Gap Data. The exact query used to collect this data can be found in [`generate_officer_data.py`](./generate_officer_data.py), and you can find the data in [](./).

You're welcome to download the file and explore the data. For a detailed explanation of the data structure, how to load the data from the file etc., please see the section [:three: Working with the Data](#working-with-the-data).

### Option 2 - Run a script to collect additional data

You can also use the script [`query_companies_house.py`](./query_companies_house.py) provided in this directory as well to make your own custom queries.

We use [Requests](http://docs.python-requests.org/en/master/) to make HTTP GET requests to the Companies House API. This is a great opportunity to learn about Requests if you aren't familiar, as you can make HTTP to any APIs you can think of with Requests under your toolbelt. It's a really powerful tool :)

Right, in order to start making queries, you need a bit of preparation to get your local environment up and running.

#### :floppy_disk: Preparing your local environment

1. Clone the repository: `$ git clone git@github.com:paygaphack/mentors-repo.git`
2. Move into the `companies-house-api` directory: `$ cd mentors-repo/companies-house-api`
3. Create a virtual environment with the dependencies listed in `environment.yaml`: `$ conda env create -f environment.yaml`
4. Activate the virtual enviromnent just created: `$ source activate companies-house-api`
5. Obtain a unique API key from [Companies House API: Authorisation](https://developer.companieshouse.gov.uk/api/docs/index/gettingStarted/apikey_authorisation.html)
6. Create a `.env` file :exclamation:within:exclamation: the `companies-house-api` directory
    It won't work otherwise, unless you manually change the path to the `.env` file by modifying the `env_path` variable in `query_companies_house.py`. The file structure should look something like the diagram below.
    
    ```
    mentors-repo  <-- Project root
    │   README.md
    │   LICENSE
    │   .gitignore  <-- Any .env files are ignored here
    │   ...
    │
    └─── companies-house-api
    │        .env  <-- Here!
    │        README.md
    │        query_companies_house.py
    │        query_gpg_data.py
    │        UK_Gender_Pay_Gap_Data_2017_to_2018.csv
    │        Demo Code for querying csv.ipynb
    │        environment.yaml
    │      ...
    │
    └─── another-project
    │        ...
    │        ...
    │   ...
    ```
    
      **:closed_book: N.B.** The `.env` file is ignored in `.gitignore` file in the root of the project. This means that it will not get tracked by `git`, and hence will not be checked into your commits. This is important for security purposes, as you _never_ want to expose your credentials to publically available spaces :no_good:

7. Paste your API key to the `.env` file

    ```bash
    # .env

    API_KEY="YOUR API KEY"
    ```

8. Now you should be all ready to fire up a query :boom: `$ python query_companies_house.py`
    If everything goes well, you should see the response printed out in the console and you should have a file called `00000006.txt` which stores the dictionary of data from the Companies House API.
