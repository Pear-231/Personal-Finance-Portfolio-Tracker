# Portfolio Tracker
A live automatic portfolio tracker in Google Sheets featuring:
- Live portfolio value tracking. 
- Automatic data recording for analysis and graphs.
- Automatic email alerts at portfolio % changes.

**Download 'Portfolio Tracker (Template)' Here:** https://docs.google.com/spreadsheets/d/1qa_QXoe13nbo7LfTOzBdMx3ibzbVT2_czGgw-78hWHI/

**To use all the features of this document a google account is required.*
  
# What is it?
The spreadsheet presents the live value of your portfolio and records this information and other information such as share price, % changes, and weights every day for historical records, analysis, and producing graphs. The Portfolio Tracker is automated using javascript written in the Google Sheets script editor (similar to Excel's VBA). Portfolio values are automatically recorded and stored in seperate sheets in the document using time-based triggers. These historical values are used in the 'Portfolio' sheet for periodic change values, and in the 'Summary' sheet for analysis of returns and graphs. 

*The Portfolio Tracker is set up to automatically record values for 8 assets (5 Stocks, 1 Bonds ETF, 1 Commodities ETF, 1 Cash) which can be adjusted to any chosen assets available on Google Finance, to add more assets see below.**

- The 'Portfolio' sheet contains all live information about assets in the portfolio. Once data is initially manually inputted, cells update live - the data is used for the 'Portfolio Breakdown' graphs in the 'Summary' sheet. 
- The 'Summary' sheet contains analysis of portfolio returns and graphs - analysis is manually calculated using formalas and data recorded in other sheets.
- The 'Current Historical Portfolio (Asset Type)' sheet contains automatically recorded historical data of the asset types in the portfolio e.g. stocks, bonds etc. - the data is used for the 'Portfolio Wealth (Asset Type)' graph in the 'Summary' sheet. 
- The 'Current Historical Portfolio (Per Asset)' sheet contains automatically recorded historical data of the individual assets in the portfolio e.g. Facebook, Apple etc. - the data is used for the 'Portfolio Wealth (Per Asset)' graph in the 'Summary' sheet. 
- The 'Realised Historical Portfolio (Per Asset)' sheet contains any assets that have previously been automatically recorded in the 'Current Historical Portfolio (Per Asset)' sheet, and are no longer held.
- The 'In-Day Portfolio Change' sheet contains automatically recorded data of the portfolio value throughout the day - the data is used for the 'In-Day Portfolio Change' graph displayed in email alerts.
- Email alerts are automatically sent when alert levels (set in the 'Additional Information' section of the 'Portfolio' sheet) are breached e.g. if % day change is greater than 'Day Gain Alert Level 1', an email alert is sent. There are 2 types of email alerts, 'Loss Alerts' and 'Gain Alerts'; email alerts feature information about 'Day Change (%)' and key insights on portfolio changes over week, month and total periods.

# Instructions:
1) Go to 'File' > 'Make a copy', to save the Portfolio Tracker to your Google Drive.
2) Using the 'Portfolio' Sheet: adding and removing assets.

  *'Portfolio' Sheet: Adding New Assets*

  - Assets currently held are in the 'Stocks', 'Bonds', 'Commodities' and 'Cash' sections. To replace the example assets and add new assets, follow these steps:
  - Cells in the columns 'Ticker', 'Quantity', 'Date of First Holding', 'Purchase Price Per Share', 'Purchase Price (£), 'Interest, Dividends and Distributions', and the asset name require manual input of data relevant to chosen assets. The 5 Stocks, 1 Bonds ETF, 1 Commodities ETF and 1 Cash are example assets*, these are to be replaced with chosen assets.
      - 'Ticker': Google Finance ticker information can be found by Google searching for the chosen asset's ticker e.g. 'facebook ticker', copy the ticker e.g. 'NASDAQ: FB', and remove the space between the stock exchange and the company so it is formatted 'NASDAQ:FB'.
      - Input data for 'Ticker', 'Quantity' etc. into the respective cells by following the examples in the template document, this process is repeated for each asset type Stocks, Bonds etc.. For 'Cash', only data for the 'Date of First Holding' and 'Purchase Price (£)' is required.
      - For 'Interest, Dividends and Distributions' cells, input data when relevant.

  *'Portfolio' Sheet: Removing Sold Assets*

  - When assets are sold, copy the cells of an asset and paste them in the 'Sold Assets (Realised)' section, copying the example sold asset. Then remove the asset from the 'Stocks' section.
  - Cells in the columns: 'Sold Price Per Share' and 'Sold Price (£)' require manual input of data.

3) Sheets Automation: setting up the 'Current Historical Portfolio' and 'In-Day Portfolio Change' sheets for automation.

  - Go to 'Tools' > 'Script editor'. This is where the code for the automation is stored.
  - Click the clock icon on the top bar or go to 'Edit > Current Project Triggers'.
  - Click 'Add Trigger': Under 'Choose which function to run' select 'portfolioDayChangeAlert', under 'Select event source' select 'Time-driven', under 'Select type of time based trigger' select 'Minutes timer', click save. If a screen appears that reads 'This app isn't verified', click 'Advanced' > 'Go to portfolio Scripts (unsafe)' > 'Allow'.
  - Click 'Add Trigger': Under 'Choose which function to run' select 'inDayportfolioChange' and repeat the previous bullet point for 'Time-driven - Minutes timer' etc.
  - Click 'Add Trigger': Under 'Choose which function to run' select 'currentHistoricalPortfolioAssetType', under 'Select event source' select 'Time-driven', under 'Select type of time based trigger' select 'Day timer', under 'Select time of day' select '10pm to 11pm' (*This time is optimised for British summer time to carry out the automated function after UK and US markets have closed. The time should be changed according to the timezone of the user and the markets of assets)*, click save.
  - Click 'Add Trigger': Under 'Choose which function to run' select 'currentHistoricalPortfolioPerAsset' and repeat the previous bullet point for 'Time-driven - Day timer' etc.
  - Click 'Add Trigger': Under 'Choose which function to run' select 'resetSheetsData', under 'Select event source' select 'Day timer', under 'Select time of day' select 'Midnight to 1am' (*This time is optimised for British summer time to carry out the automated function after UK and US markets have closed. The time should be changed according to the timezone of the user and the markets of assets)*, click save.
  - The triggers have all been loaded, this page can be closed.
  - To test these functions, in the Portfolio Tracker document go to the 'Current Historical Portfolio (Asset Type) sheet, on the top bar click 'Functions' > click currentHistoricalPortfolioAssetType and a new row will will be added for today's data. This row can be deleted after the test is completed.
  
3) Email Automation: adding the user's email address, setting alert levels and receiving a test email.

  - On the 'Portfolio' sheet: 
      - Under 'Additional Information' - 'Email Address', replace 'youremailgoeshere@email' with a chosen email address. 
      - Under 'Additional Information' - 'Email Alerts' - 'Alert at (%)', set the % changes, that if breached will trigger alert emails notifying you of the breach.
  
  *Send Test Email:*
  - On the 'Portfolio' sheet, in the 'Day Change (%)' column, cell 'Q8', set the value to a value greater than the set alert level % change e.g. if 'Day Gain Alert Level 1 (%)' is set to 0.5%, set cell 'Q8' to e.g. 10%, this will update the 'Send Count' in the cell next to the 'Alert at (%)' to confirm the email is sent, and the chosen email address will receive an email alert.
  - Once the test email is received, in the 'Portfolio' sheet, click 'Edit' > 'Undo', until cell 'Q8' is returned to it's original formula before the e.g. 10% manually inputted.
   
4) Summary: analysing the data.

  - To analyse your own data, see the formulas in the example cells and replicate for your own data set. The risk free rate can be found at the hyperlink of the cell 'A3'.
  
5) 'Realised Historical Portfolio (Per Asset)': moving realised assets.

  - Once an asset is sold, in the 'Current Historical Portfolio (Per Asset)' sheet, copy the data in the columns for asset name and 'Quantity and paste it in the 'Realisd Historical Portfolio (Per Asset)', adding new columns as requried. Once this is done, follow the instructions in step '2.' on moving an asset into the 'Sold Assets (Realised)' of the 'Portfolio' sheet.

# Additional Information:
**If spaces for more assets are required this can be done by adding to the code in 'Tools' > 'Script editor', and adding rows and columns to the 'Portfolio', 'Current Historical Portfolio (Asset Type)' and 'Current Historical Portfolio (Per Asset)' sheets. Unfortunately, to detail this process with instructions would result in a huge set of instructions, with a lot of detail, and would take a significant amount of time, as such I can only provide instructions on how to use the spreadsheet in its current form and cannot instruct how to code more assets and features. If you need to add more assets I suggest making another copy of the spreadsheet and creating a 'separate' portfolio, or you can learn to edit the code yourself (highly recommend this!). :)*

**The 'Portfolio' sheet is set up for GBP (£), to change this, select the cells that are in GBP (£), go to 'Format' > 'Number' > 'More Formats' > 'More Currencies'.*
         
**Disclaimer: The example assets in this document are only example assets and do not consist of a recommendation to buy or sell example assets. This document is for portfolio tracking and analysis and does not consist of financial advice.*

Code used in Google Script:
