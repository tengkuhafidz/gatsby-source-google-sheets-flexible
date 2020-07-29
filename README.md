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

**Available Options**
- **apiKey:** Your google api key as in step 1.
- **spreadsheetId:** The ID of the Google Sheets document to retrieve data from. *Not required if you use the `spreadsheetUrl` option (next line)*.
- **spreadsheetUrl:** The url of Google Sheets document to retrieve data from. *Not required if you use the `spreadsheetId` option (previous line)*.
- **tabName:** the tab name of the spreadsheet that you want to retrieve from the Google Sheets document.
- **cellRange (OPTIONAL):** the range within the Google Sheets document of the cells you want to retrieve data from. Defaults to "A1:Z1000".
- **majorDimension (OPTIONAL):** The major dimension that results should use. 2 Possible values: "ROWS" (default), "COLUMNS". Check out the majorDimension parameter [here](https://developers.google.com/sheets/api/reference/rest/v4/spreadsheets.values/get) for more information.
- **valueRenderOption (OPTIONAL):** Determines how values should be rendered in the output. 3 possible values: "FORMATTED_VALUE" (default), "UNFORMATTED_VALUE", "FORMULA". Check out [here](https://developers.google.com/sheets/api/reference/rest/v4/ValueRenderOption) for more information.
- **dateTimeRenderOption (OPTIONAL):** Determines how dates should be rendered in the output. 2 possible values: "SERIAL_NUMBER", "FORMATTED_STRING". Check out [here](https://developers.google.com/sheets/api/reference/rest/v4/DateTimeRenderOption) for more information.


**Additional Notes:** 
- All of the values should be of string type, within quotation marks.
- You can add the plugin with different configurations multiple times to pull data from different Google Sheets tabs/files


**Example of using the plugin to retrieve data from 2 tabs in the same sheets, using `spreadsheetUrl` for one, and `spreadsheetId` for the other:** 
(in `gatsby-config.js`)
```
module.exports = {
    plugins: [
        {
            resolve: "gatsby-source-google-sheets-flexible",
            options: {
                apiKey: "AIzaSyCQQlbvNPEp21LLRsA_S0-R3r2TdxyUE-k",
                spreadsheetUrl: "https://docs.google.com/spreadsheets/d/16x6gtYQl7TAhehSqcaf_SAMDKNpEgoMxAGgMpQ7NUMs/edit#gid=72026853",
                tabName: "site",
                cellRange: "A1:B23",
                majorDimension: "COLUMNS",
            },
        },
        {
        resolve: 'gatsby-source-google-sheets-flexible',
            options: {
                apiKey: "AIzaSyCQQlbvNPEp21LLRsA_S0-R3r2TdxyUE-k",
                spreadsheetId: "16x6gtYQl7TAhehSqcaf_SAMDKNpEgoMxAGgMpQ7NUMs",
                tabName: "listing",
                cellRange: "A1:H1000",
                majorDimension: "ROWS",
            }
        }   
    ],
}
```

## Step 3: View the results

1. start the project in dev environment by running `gatsby develop`
2. go to http://localhost:8000/___graphql to see the retrieved data. It should have created your Google Sheets data under `all<tabName>SheetsData`
