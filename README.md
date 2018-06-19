# U.S. Prosecutor Database
> Last Updated: June 19th 2018 (Juneteenth)

**If you are interested in contributing data, see [3. Data Collection](#4-data-collection) for detailed instructions.**

## Table of Contents
1. Introduction
2. The USPD App
3. The USPD Data
4. Data Collection
5. Post-Carceral: Stay Updated, Volunteer
6. Acknowledgements

## 1. Introduction

The U.S. Prosecutor Database is a collection of .csv and .json data for currently elected and appointed government attorneys at the local, state, and federal level. This includes Attorney Generals, U.S. Attorneys, District/State Attorneys, and Municipal/County/City Attorneys.

Our goal is to showcase prosecutorial demographics, culture, and history. This goal is in service to the Post-Carceral vision:

* Cultivate a community of holding prosecutors accountable as a voting public
* Change the political and cultural landscape of this nation's real lawmakers
* Assisting prosecutors who aim to end mass incarceration and commit to decarceration

Unfortunately, this data does not already exist. It is our mission to collect this information so that we can not only showcase reality, but contribute to radically changing this political picture for future generations to come.

## 2. The USPD App

Our online community, Post-Carceral, has created a web app which renders this data for easy access.

Please contact [Billimarie](https://www.github.com/billimarie) if you are interested in contributing as a web developer or web designer.

## 3. The USPD Data

This repository houses the data we are aiming to collect.

The **Basic Prosecutor Profile** consists of 7 fields:
* Name
* Location (State, County)
* Role
* Website
* Office Info (Address)
* Contact Info (Phone, Fax, Email)
* Optional: headshot / profile image

The **Full Prosecutor Profile** has several additional fields, including Demographics (Age, Race, Gender, Party). Feel free to collect this data in your pull request.

## 4. Data Collection

Here are detailed instructions on how you can contribute to the repo as a data collector.

### Setting Up Locally

1. Clone this repo to your local environment
`git clone git@github.com:billimarie/prosecutor-database.git`

2. Create a new branch for your work (ex: `ny-da`)
`git checkout -b [state]-[role]`

3. Install Node modules
`npm install`

4. Install the `csvtojson` module globally
`npm install -g csvtojson`

### Gathering Data

As noted, a dataset of all U.S. Prosecutors does not exist. Therefore, in order to create it, we work in a scope of location (state, county) and role. You will see this component echoed as State-Role. **Your branch should only consist of data from one state, one role.** It is okay to submit multiple pull requests, as long as you keep your work isolated in this manner.

There are one of two options you can choose for cultivating your dataset:

#### 1. Manually Collecting Prosecutor Names By Hand

1. Create a new .csv file as `[state]-[role].csv`. Add the **Basic Prosecutor Profile** columns:

* Name
* Location (State, County)
* Role
* Website
* Office Info (Address)
* Contact Info (Phone, Fax, Email)
* Optional: headshot / profile image

*Note: You can always add additional columns, as long as it conforms to the Full Prosecutor Profile (Demographics: Age, Race, Gender, Party).*

2. Google your chosen state's prosecutor association.

3. Collect the data in your .csv file.

4. Run the csvtojson Node module (ex: `ny-da.csv > ny-da.json`).
`csvtojson [state-role].csv > [state-role].json`

5. Be mindful of isolating your work. **One state, one role, one branch.**

6. Add, Commit, and Submit a Pull Request.

```
git add .
git commit -m "Added [state] [role] as .csv and .json"
git push origin [branch]
```

#### 2. Creating A Python Script To Scrape The Data

The second option (data scraping via Python script) is often not ideal as each state's method for collecting and rendering basic prosecutor data (name, role, office, website) is wildly non-uniform. It will most likely require more work to tweak the following script to the state's prosecutor association website,. versus simply collecting the data by hand. However, this is a good avenue to try if you come across some semblance of uniformity and/or want to see how scraping works.

Here is the Python script I've been tweaking for each state:

```
#!/usr/bin/python3

from pyquery import PyQuery as pq
import requests as req

urls = [
    'https://www.nypti.org/DA Htmls/stlawrence.html',
    'https://www.nypti.org/DA Htmls/franklin.html',
    'https://www.nypti.org/DA Htmls/clinton.html',
    ...
    'https://www.nypti.org/DA Htmls/orleans.html',
    'https://www.nypti.org/DA Htmls/niagara.html',
    'https://www.nypti.org/DA Htmls/chautauqua.html'
]

for url in urls:
    page = req.get(url)
    doc = pq(page.text)
    link = doc('a')
    website = pq(link).attr('href')
    da = doc('div').text()
    print(da)
    print(website)
```

Please feel free to submit a pull request if you can enhance this script (or provide a newer, better, faster version).

Once you scrape from a website, continue with the following:

1. Make sure the data you scraped is organized in an .csv file (`[state]-[role].csv`). Add the **Basic Prosecutor Profile** columns:

* Name
* Location (State, County)
* Role
* Website
* Office Info (Address)
* Contact Info (Phone, Fax, Email)
* Optional: headshot / profile image

*Note: You can always add additional columns, as long as it conforms to the Full Prosecutor Profile (Demographics: Age, Race, Gender, Party).*

2. Run the csvtojson Node module (ex: ny-da.csv > ny-da.json).
`csvtojson [state-role].csv > [state-role].json`

3. Be mindful of isolating your work. **One state, one role, one branch.**

4. Add, Commit, and Submit a Pull Request.

```
git add .
git commit -m "Added [state] [role] as .csv and .json"
git push origin [branch]
```

#### Brainstorming Other Means Of Data Collection

If a new method for collecting this data is discovered, please create a new issue where we can discuss it as a community.

## 5. Post-Carceral

### Stay Updated

**[Sign up for our weekly mailing list](https://t.co/bvfPitdu2g).** I send emails to everyone every Monday, after our remote Sunday sessions.

You can also find USPD updates on our Twitter: [@USProsecutorDB](https://twitter.com/USProsecutorDB).

To get involved in a remote Sunday session, follow [@postcarceral](https://twitter.com/postcarceral) (this is our general prisoners' rights group responsible for housing the USPD project).

### Volunteer

Every Sunday, we meet via Skype to:
* Discuss recent prosecutor news, primary results, and campaigns
* Brainstorm ways to hold prosecutors accountable
* Manually search Google by hand for prosecutor data
* Use Python to scrape data from district attorney association websites

**You don't have to be a developer or a prisoners' rights activist to join.** We're looking for all types of people with all types of expertise to collaborate with.

If you'd like to volunteer and help with the US Prosecutor Database, or if you're curious about attending a Datathon session, send an email to [Billimarie](https://www.github.com/billimarie) and follow [@USProsecutorDB on Twitter](https://twitter.com/USProsecutorDB).

## 6. Acknowledgements

This project would not be possible without the support of many individuals and organizations, including, but not limited to:

<img src="https://user-images.githubusercontent.com/6895471/35476336-29f78180-037c-11e8-800d-6fc8501a09b7.jpg" width="250px" border="0" />
