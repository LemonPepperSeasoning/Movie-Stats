# Movie-Stats

Welcome to the Movie-Stats project, created by INFOSYS 300 / SOFTENG 762 Team 4 students from The University of Auckland.

## Introduction

Movie-stats is a UI-path program that extracts movie statistics from IMBd and displays it using excel.
The movies can be filtered by Genre, Rating, and Year of production.

## Installation and configuration

### Run

- Open UiPath studio
- Select "Open a Local Project"
- Select project.json file in the root folder
- Click "Run" from the top action ribbon

If the above run instruction does not work, please refer to "General caveats" section and try the below instruction:

- Open Main.xaml file using UiPath Studio
- Click "Run" from the top action ribbon

### Deployment

This program can be published to UIPath assistant for easier deployment. Follow this step by step guide: https://docs.uipath.com/studio/docs/about-publishing-automation-projects

### Dependencies

- By default, Excel blocks any programmatic access to the application unless the user permits it. Follow this guide to enable VBA trust settings. https://www.surfandperf.com/2019/01/uipath-error-programmatic-access-to.html
- The Excel activities package is required and will automatically install if connected to the internet.
- Edge requires the UIPath Studio extension to be installed https://docs.uipath.com/studio/docs/extension-for-edge-chromium#install-from-uipath-studio

### Configuration

Configuration can be managed at the first prompt when starting the script.

Default configuration:

- `Top 25`
- `Action`
- `Over 50,000 votes`
- `Rating over 7.5`
- `Within the last 20 years`

## Detailed implementation

#### FetchMovieData Module

- Step 1: Load configuration
  - Loads default configuration, or calls GetUserConfig module
- Step 2: Scrape IMDb
  - Creates a url based on the selected configurations and loads each title into a datatable

#### GetUserConfig Module

- Step 1: Configuration Inputs
  - Gets user input
- Step 2: Configuration Inputs
  - Run's DateChecker module to check the user date input is valid

#### DateChecker Module

- Checks Date
  - Checks date format is correct
  - Checks year is valid
  - Checks month is valid if year is valid
  - Checks day is valid if year and month are valid

#### FetchBoxOfficeInformation Module

- Step 1: Find movie on boxofficemojo
  - With the IMDb id from earlier, go to the movie page and scrape the data while handling any errors.

#### ExcelExport Module

- Step 1: Save to an Excel file
  - Store the scraped data in an Excel file
- Step 2: Plot the data
  - Use the stored data and leverage the UIPath Excel activities plugin to automatically plot a chart from the data.

## Outcome and document outgress

<img src="https://i.imgur.com/JhSRyDw.png" width="70%">

The outcome will be a single Excel file named `Movies.xlsx` with a list of data scraped, and the plotted graph.

## General caveats

- Desired data points such as budget may not be available due to the information not being publicly disclosed.
- Any currently running Edge instances will be forcefully closed as UIPath tries to open its own instance.
- If UiPath is stuck on "restoring dependencies", backup and delete `project.json` and try again
