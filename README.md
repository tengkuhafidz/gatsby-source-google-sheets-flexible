## Description

This is a Gatsby source plugin that has all the options provided by the Google Sheets api. You can also simply use the Google Sheets url instead of the its ID for convenience.

## Install

`npm i gatsby-source-google-sheets-flexible`

## How to use

### Step 1: Prepare your Google API

1. Create a [Google API project](https://console.developers.google.com/projectcreate)
2. Enable [Google Sheets API](https://console.developers.google.com/apis/library/sheets.googleapis.com?project=websheets&folder&organizationId) for that project
   - Click the **ENABLE** button and select the project that you created
3. Create the [Google API key](https://console.developers.google.com/apis/credentials) for that project
   - Click **CREATE CREDENTIALS** button and select **API key**

### Step 2: Configure your Gatsby Project

1. install plugin by running `npm i gatsby-source-google-sheets-flexible`
2. add the plugin in your `gatsby-config.js` file
```
module.exports = {
    plugins: [
        {
            resolve: 'gatsby-source-google-sheets-flexible',
            options: {
                apiKey: <your google api key as in step 1>,
                spreadsheetUrl: <your google sheets url>,
                tabName: <the specific tab name of your google sheets file>,
                cellRange: <the cell range within the google sheets of the data you want to get. eg. 'A1:B1000'>,
                majorDimension: <'COLUMNS' or 'ROWS'>,
            },
        }
    ],
}
```

NOTE: You can add the plugin with different configurations multiple times in your configuration to pull data from different Google Sheets tabs/files

## Step 3: View the results

1. start the project in dev environment by running `gatsby develop`
2. go to http://localhost:8000/___graphql to see the retrieved data. It should have created your Google Sheets data under `all<tabName>SheetsData`
