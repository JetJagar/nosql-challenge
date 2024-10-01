# nosql-challenge
# UK Food Hygiene Ratings Analysis

## Overview
This project analyzes food hygiene ratings data provided by the UK Food Standards Agency. The aim is to assist the food magazine **Eat Safe, Love** in evaluating restaurants and establishments for their articles and reviews. The project involves setting up a NoSQL database, modifying the data, and performing exploratory analysis.

## Table of Contents
- [Part 1: Database and Jupyter Notebook Setup](#part-1-database-and-jupyter-notebook-setup)
- [Part 2: Update the Database](#part-2-update-the-database)
- [Part 3: Exploratory Analysis](#part-3-exploratory-analysis)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Part 1: Database and Jupyter Notebook Setup
1. **Import Data**: Import the data from `establishments.json` into a MongoDB database named `uk_food` and collection `establishments`.
   - Terminal Command:
     ```bash
     mongoimport --db uk_food --collection establishments --file establishments.json --jsonArray
     ```
   - Include this command in a markdown cell in your Jupyter Notebook.

2. **Libraries**: Import the necessary libraries:
   ```python
   from pymongo import MongoClient
   from pprint import pprint
   ```

3. **Mongo Client**: Create an instance of the Mongo Client and confirm the database and collection setup.
   ```python
   client = MongoClient()
   db = client.uk_food
   establishments = db.establishments
   ```

4. **Validation**:
   - List databases to confirm `uk_food` exists.
   - List collections to confirm `establishments` is present.
   - Retrieve and display one document from `establishments` using `find_one`.

## Part 2: Update the Database
1. **Add New Restaurant**: Insert a new halal restaurant record into the `establishments` collection:
   ```python
   new_restaurant = {
       "BusinessName": "Penang Flavours",
       "BusinessType": "Restaurant/Cafe/Canteen",
       "BusinessTypeID": "",
       "AddressLine1": "Penang Flavours",
       "AddressLine2": "146A Plumstead Rd",
       "AddressLine3": "London",
       "PostCode": "SE18 7DY",
       "LocalAuthorityCode": "511",
       "LocalAuthorityName": "Greenwich",
       "scores": {
           "Hygiene": "",
           "Structural": "",
           "ConfidenceInManagement": ""
       },
       "SchemeType": "FHRS",
       "geocode": {
           "longitude": "0.08384000",
           "latitude": "51.49014200"
       },
       "NewRatingPending": True
   }
   establishments.insert_one(new_restaurant)
   ```

2. **Find BusinessTypeID**: Query to find `BusinessTypeID` for "Restaurant/Cafe/Canteen" and update the new restaurant's record.

3. **Remove Dover Establishments**: Count and remove all establishments with the Local Authority of Dover, then confirm deletions.

4. **Data Type Corrections**: Use `update_many` to convert latitude, longitude, and `RatingValue` to their correct numeric types.

## Part 3: Exploratory Analysis
Perform analysis to answer specific queries from the magazine:
1. **Hygiene Score of 20**: Identify establishments with a hygiene score of 20.
2. **High Rating Establishments in London**: Find establishments in London with a `RatingValue` >= 4, using regex for the Local Authority name.
3. **Top Rated Establishments**: Get the top 5 establishments with a `RatingValue` of 5, sorted by the lowest hygiene score, near "Penang Flavours."
4. **Hygiene Score Count by Local Authority**: Count establishments with a hygiene score of 0, sorted from highest to lowest, and display the top ten.

## Installation
To get started, clone the repository and ensure you have the required libraries:
```bash
git clone <repository-url>
pip install pymongo pandas
```

## Usage
1. Open `NoSQL_setup_starter.ipynb` for setting up the database and updating it.
2. Use `NoSQL_analysis_starter.ipynb` for performing the exploratory analysis.
