# Movie-Stats

# Installation and configuration
### Dependencies

- By default, Excel blocks any programmatic access to the application unless the user permits it. Follow this guide to enable VBA trust settings. https://www.surfandperf.com/2019/01/uipath-error-programmatic-access-to.html
- The Excel activities package is required and will automatically install if connected to the internet.
- Edge requires the UIPath Studio extension to be installed https://docs.uipath.com/studio/docs/extension-for-edge-chromium#install-from-uipath-studio

### Configuration
Default configuration:
- ``Top 25``
- ``Action``
- ``Over 50,000 votes``
- ``Rating over 7.5``
- ``Within the last 20 years``

Configuration can be managed at the first prompt when starting the script.

# Detailed implementation
#### Module 1
- Step 1: Load configuration
  - Loads default configuration, or prompts user with optional changes
- Step 2: Scrape IMDb
  - Creates a url based on the selected configurations and loads each title into a datatable

#### Module 2
- Step 1: Find movie on boxofficemojo
  - With the IMDb id from earlier, go to the movie page and scrape the data while handling any errors.

#### Module 3
- Step 1: Save to an Excel file
  - Store the scraped data in an Excel file
- Step 2: Plot the data
  - Use the stored data and leverage the UIPath Excel activities plugin to automatically plot a chart from the data.

   
# Outcome and document outgress
<img src="https://i.imgur.com/JhSRyDw.png" width="70%">

The outcome will be a single Excel file named ``Movies.xlsx`` with a list of data scraped, and the plotted graph.

# General caveats
- Desired data points such as budget may not be available due to the information not being publicly disclosed. 
- Any currently running Edge instances will be forcefully closed as UIPath tries to open its own instance.
- If UIPath is stuck on "restoring dependencies", backup and delete ``project.json`` and try again


