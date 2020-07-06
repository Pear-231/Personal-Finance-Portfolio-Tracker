# Portfolio Tracker
A live automatic portfolio tracker in Google Sheets featuring:
- Live portfolio value tracking. 
- Automatic data recording for analysis and graphs.
- Automatic email alerts at portfolio % changes.

Download Portfolio Tracker (Template) Here: https://docs.google.com/spreadsheets/d/1qa_QXoe13nbo7LfTOzBdMx3ibzbVT2_czGgw-78hWHI/
  
# What is it?
The spreadsheet presents the live value of your portfolio and records this information and other information such as share price, % changes, and weights every day for historical records, analysis, and producing graphs. The Portfolio Tracker is automated using javascript written in the Google Sheets script editor (similar to Excel's VBA). Portfolio values are automatically recorded and stored in seperate sheets in the document using time-based triggers. These historical values are used in the 'Portfolio' sheet for periodic change values, and in the 'Summary' sheet for analysis of returns and graphs.

- The 'Portfolio' sheet contains all live information about assets in the portfolio. Once data is initially manually inputted cells updated live - the data is used for the 'Portfolio Breakdown' graphs in the 'Summary' sheet. 
- The 'Summary' sheet contains analysis of portfolio returns and graphs - analysis is manually calculated using formalas and data recorded in other sheets.
- The 'Current Historical Portfolio (Asset Type)' sheet contains automatically recorded historical data of the asset types in the portfolio e.g. stocks, bonds etc. - the data is used for the 'Portfolio Wealth (Asset Type)' graph in the 'Summary' sheet. 
- The 'Current Historical Portfolio (Per Asset)' sheet contains automatically recorded historical data of the individual assets in the portfolio e.g. Facebook, Apple etc. - the data is used for the 'Portfolio Wealth (Per Asset)' graph in the 'Summary' sheet. 
- The 'Realised Historical Portfolio (Per Asset)' sheet contains any assets that have previously been automatically recorded in the 'Current Historical Portfolio (Per Asset)' sheet, and are no longer held.
- The 'In-Day Portfolio Change' sheet contains automatically recorded data of the portfolio value throughout the day - the data is used for the 'In-Day Portfolio Change' graph displayed in email alerts.
- Email alerts are automatically sent when alert levels (set in the 'Additional Information' section of the 'Portfolio' sheet) are breached. 

# Instructions:
1) Go to 'File > Make a copy', to save the Portfolio Tracker to your Google Drive.
2) Adding and removing assets:
'Portfolio' Sheet: Current Assets
- The 5 Stocks, 1 Bonds ETF, and 1 Commodities ETF are example assets, these are to be replaced with desired assets.
- Cells in the columns: 'Ticker', 'Quantity', 'Date of First Holding', 'Purchase Price Per Share', 'Purchase Price (£), 'Interest, Dividends and Distributions', and the asset name require manual input of data relevant to desired assets.
    - 'Ticker': Google Finance ticker information can be found by Google searching for the desired asset's ticker e.g. 'facebook ticker', copy the ticker e.g. 'NASDAQ: FB', and remove the space between the stock exchange and the company so it is formatted 'NASDAQ:FB'.
    - Input data for 'Ticker', 'Quantity' etc. into the respective cells by following the examples in the template document, this process is repeated for each asset type. For 'Cash', data inputted is slightly different, follow the example.    
'Portfolio' Sheet: Realised Assets
- When assets are sold, copy the cells of an asset and paste them in the 'Sold' section, remover the asset from the 'Stocks' section.
- Cells in the columns: 'Sold Price Per Share' and 'Sold Price (£)' require manual input of data.

 



    
    
