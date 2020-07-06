# Portfolio Tracker
A live automatic portfolio tracker in Google Sheets featuring:
- Live portfolio value tracking. 
- Automatic data recording for analysis and graphs.
- Automatic email alerts at portfolio % changes.

**[Download 'Portfolio Tracker (Template)' Here](https://docs.google.com/spreadsheets/d/1qa_QXoe13nbo7LfTOzBdMx3ibzbVT2_czGgw-78hWHI/)** 

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

*To replace the example assets and add new assets in the 'Portfolio' sheet, follow these steps:*

  - Assets currently held are in the 'Stocks', 'Bonds', 'Commodities' and 'Cash' sections. 
  - Manually input data in the cells in the columns 'Ticker', 'Quantity', 'Date of First Holding', 'Purchase Price Per Share', 'Purchase Price (£), 'Interest, Dividends and Distributions', copying the example assets.
      - 'Ticker': Google Finance ticker information can be found by Google searching for the chosen asset's ticker e.g. 'facebook ticker', copy the ticker e.g. 'NASDAQ: FB', and remove the space between the stock exchange and the company so it is formatted 'NASDAQ:FB'.
      - For 'Cash', only data for the 'Date of First Holding' and 'Purchase Price (£)' is required.
      - For 'Interest, Dividends and Distributions' cells, input data when relevant.

*To remove sold assets in the 'Portfolio' sheet follow these steps:*

  - When assets are sold, copy the cells of an asset and paste them in the 'Sold Assets (Realised)' section, copying the example sold asset. Then remove the asset from the 'Stocks' section.
  - Cells in the columns: 'Sold Price Per Share' and 'Sold Price (£)' require manual input of data.

3) Sheets Automation: setting up the 'Current Historical Portfolio' and 'In-Day Portfolio Change' sheets for automation.

*To automate the collection of data for historical records and analysis follow these steps:*

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

*To set up automatic email alerts follow these steps:*

  - On the 'Portfolio' sheet: 
      - Under 'Additional Information' - 'Email Address', replace 'youremailgoeshere@email' with a chosen email address. 
      - Under 'Additional Information' - 'Email Alerts' - 'Alert at (%)', set the % changes, that if breached will trigger alert emails notifying you of the breach.
  
  *Send Test Email:*
  - On the 'Portfolio' sheet, in the 'Day Change (%)' column, cell 'Q8', set the value to a value greater than the set alert level % change e.g. if 'Day Gain Alert Level 1 (%)' is set to 0.5%, set cell 'Q8' to e.g. 10%, this will update the 'Send Count' in the cell next to the 'Alert at (%)' to confirm the email is sent, and the chosen email address will receive an email alert.
  - Once the test email is received, in the 'Portfolio' sheet, click 'Edit' > 'Undo', until cell 'Q8' is returned to it's original formula before the e.g. 10% manually inputted.
   
4) Summary: analysing the data.

  - To analyse your own data, see the formulas in the example cells, copy and apply them for your own data set. The risk free rate can be found at the hyperlink of the cell 'A3'.
  
5) 'Realised Historical Portfolio (Per Asset)': moving realised assets.

  - Once an asset is sold, in the 'Current Historical Portfolio (Per Asset)' sheet, copy the data in the columns for asset name and 'Quantity and paste it in the 'Realisd Historical Portfolio (Per Asset)', adding new columns as requried. Once this is done, follow the instructions in step '2.' on moving an asset into the 'Sold Assets (Realised)' of the 'Portfolio' sheet.

# Additional Information:
**If spaces for more assets are required this can be done by adding to the code in 'Tools' > 'Script editor', and adding rows and columns to the 'Portfolio', 'Current Historical Portfolio (Asset Type)' and 'Current Historical Portfolio (Per Asset)' sheets. Unfortunately, to detail this process with instructions would result in a huge set of instructions, with a lot of detail, and would take a significant amount of time, as such I can only provide instructions on how to use the spreadsheet in its current form and cannot instruct how to code more assets and features. If you need to add more assets I suggest making another copy of the spreadsheet and creating a 'separate' portfolio, or you can learn to edit the code yourself (highly recommend this!). :)*

**The 'Portfolio' sheet is set up for GBP (£), to change this, select the cells that are in GBP (£), go to 'Format' > 'Number' > 'More Formats' > 'More Currencies'.*
         
**Disclaimer: The example assets in this document are only example assets and do not consist of a recommendation to buy or sell example assets. This document is for portfolio tracking and analysis and does not consist of financial advice.*

# Code used in Google Script:


<// Menu for testing script in sheet
function inSheetUse() {
  var menu = [{name: "portfolioDayChangeAlert", functionName: "portfolioDayChangeAlert"}, {name: "inDayPortfolioChange", functionName: "inDayPortfolioChange"}, 
              {name: "currentHistoricalPortfolioAssetType", functionName: "currentHistoricalPortfolioAssetType"}, {name: "currentHistoricalPortfolioPerAsset", functionName: "currentHistoricalPortfolioPerAsset"}, 
              {name: "resetSheetsData", functionName: "resetSheetsData"}]
  SpreadsheetApp.getActiveSpreadsheet().addMenu("Functions", menu);
}


> // function to send email alerts
function portfolioDayChangeAlert() {
  
  // Skip week-end
  // Sunday is day 0, saturday is day 6.
  var day = new Date();
  if (day.getDay() >0 && day.getDay() <6) {

  // Portfolio data
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Portfolio");
  var sheetSummary = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Summary");
  var timeBST = Utilities.formatDate(new Date, "Europe/London", "HH:mm")
  
  // Email send counters
  var sendCountTotalLossAlert1 = sheet.getRange("C33").getValue()
  var sendCountGetLossAlert1 = sheet.getRange("C33");
  var sendCountAddLossAlert1 = sendCountGetLossAlert1.getValue();
  var sendCountTotalLossAlert2 = sheet.getRange("C34").getValue()
  var sendCountGetLossAlert2 = sheet.getRange("C34");
  var sendCountAddLossAlert2 = sendCountGetLossAlert2.getValue();
  var sendCountTotalGainAlert1 = sheet.getRange("C35").getValue()
  var sendCountGetGainAlert1 = sheet.getRange("C35");
  var sendCountAddGainAlert1 = sendCountGetGainAlert1.getValue();
  var sendCountTotalGainAlert2 = sheet.getRange("C36").getValue()
  var sendCountGetGainAlert2 = sheet.getRange("C36");
  var sendCountAddGainAlert2 = sendCountGetGainAlert2.getValue();
  
  // Data for calculations
  var portfolioLossAlert1Pct = sheet.getRange("B33").getValue();
  var portfolioLossAlert2Pct = sheet.getRange("B34").getValue();
  var portfolioGainAlert1Pct = sheet.getRange("B35").getValue();
  var portfolioGainAlert2Pct = sheet.getRange("B36").getValue();
  var portfolioDayChangePct = sheet.getRange("Q8").getValue();

  
  // Display data for emails
  // Portfolio
  var portfolioLossAlert1PctDisplay = sheet.getRange("B33").getDisplayValue();
  var portfolioLossAlert2PctDisplay = sheet.getRange("B34").getDisplayValue();
  var portfolioGainAlert1PctDisplay = sheet.getRange("B35").getDisplayValue();
  var portfolioGainAlert2PctDisplay = sheet.getRange("B36").getDisplayValue();
  var portfolioDayChangePctDisplay = sheet.getRange("Q8").getDisplayValue()
  var portfolioWeekChangePctDisplay = sheet.getRange("S8").getDisplayValue();
  var portfolioMonthChangePctDisplay = sheet.getRange("U8").getDisplayValue();
  var portfolioTotalChangePctDisplay = sheet.getRange("O8").getDisplayValue();
  var portfolioTotalChangeDisplay = sheet.getRange("N8").getDisplayValue();

  // Email montent
  var emailList = sheet.getRange("B37").getDisplayValue();
  var emailSubjectLoss = "Portfolio Day Loss Alert"
  var emailSubjectGain = "Portfolio Day Gain Alert"
  
  // Email message
  var emailMessageIntro = "You are receiving this alert to notify you that your portfolio"
  var emailSendTime = " <i>as of " + timeBST + " (BST)."
  var emailMessageBody = "<br /><br /><strong>Portfolio Key Insights:</strong><li>Total Change (£): <strong>" + portfolioTotalChangeDisplay + "</strong></li>" 
  + "<li>Total Change (%): <strong>" + portfolioTotalChangePctDisplay + "</strong></li>" + "<li>Day Change (%): <strong>" + portfolioDayChangePctDisplay + "</strong></li>" + "<li>Week Change (%): <strong>" 
  + portfolioWeekChangePctDisplay + "</strong></li>" + "<li>Month Change (%): <strong>" + portfolioMonthChangePctDisplay
  var emailImages={};
  var emailSignature = "<br /><br />Regards,<br /><br />Portfolio Alerts<br /><br /> "
  var emailMessageEnding = '<p style = "font-family:arial,garamond,serif;font-size:11px;">' + "*In-Day Portfolio Change graph is displaying from BST perspective; UK markets are open 08:00 - 16:30, US markets are open 14:30 - 21:00."
  
  // Finds the 'In-Day Portfolio Change Graph'
  var charts = sheetSummary.getCharts();
  var chartBlobs=new Array(charts.length); 
  
  // Graph email embed  
  var builder = charts[0].modify();
  builder.setOption('vAxis.format', '#');
  var newchart = builder.build();
  chartBlobs[1] = newchart.getAs('image/png');
  var emailChart = "<br /><br />In-Day Portfolio Change Graph:*</strong> <p align='left'><img src='cid:chart" + 1 + "'"
  emailImages["chart"+1] = chartBlobs[1];
  
  // Email message
  var emailMessageBody = emailMessageBody  + emailChart + "<br />To view your full portfolio <a href=https://docs.google.com/spreadsheets/d/1qa_QXoe13nbo7LfTOzBdMx3ibzbVT2_czGgw-78hWHI >click here</a>."

  
  // Portfolio Loss alert level 1 email
  if (portfolioDayChangePct <= portfolioLossAlert1Pct && sendCountTotalLossAlert1 == 0){
    
    sendCountGetLossAlert1.setValue(sendCountAddLossAlert1+1);
    
    // Adjusts the email message to include the alert level.
    var emailMessageIntro = emailMessageIntro + " has experienced a <strong>" + portfolioDayChangePctDisplay + "</strong> change in value today, breaching its <strong>first loss alert level of " + portfolioLossAlert1PctDisplay + "</strong>,"
    var emailMessageFurtherAlerts = "<br /><br />Further alerts will be provided if the second alert level is breached."
    var emailMessage = emailMessageIntro + emailSendTime + emailMessageBody + emailMessageFurtherAlerts + emailSignature + emailMessageEnding
    

    
    MailApp.sendEmail({
    to: emailList,
    subject: emailSubjectLoss,
    htmlBody: emailMessage,
    name: 'Portfolio Alerts',
    inlineImages:emailImages}); 
  }
  
  // Portfolio Loss alert level 2 email
  if (portfolioDayChangePct <= portfolioLossAlert2Pct && sendCountTotalLossAlert1 == 1 && sendCountTotalLossAlert2 < 1 ){  
    
    sendCountGetLossAlert2.setValue(sendCountAddLossAlert2+1);
    
    // Adjusts the email message to include the alert level.
    var emailMessageIntro = emailMessageIntro + " has experienced a <strong>" + portfolioDayChangePctDisplay + "</strong> change in value today, breaching its <strong>second loss alert level of " + portfolioLossAlert2PctDisplay + "</strong>,"
    
   var emailMessage = emailMessageIntro + emailSendTime + emailMessageBody + emailSignature + emailMessageEnding
   

    
    
    MailApp.sendEmail({
    to: emailList,
    subject: emailSubjectLoss,
    htmlBody: emailMessage,
    name: 'Portfolio Alerts',
    inlineImages:emailImages}); 
  }
  
  // Portfolio Gain alert level 1 email
  if (portfolioDayChangePct >= portfolioGainAlert1Pct && sendCountTotalGainAlert1 == 0){  
    
    sendCountGetGainAlert1.setValue(sendCountAddGainAlert1+1);
    
    // Adjusts the email message to include the alert level.
    var emailMessageIntro = emailMessageIntro + " has experienced a <strong>" + portfolioDayChangePctDisplay + "</strong> change in value today, breaching its <strong>first gain alert level of " + portfolioGainAlert1PctDisplay + "</strong>,"
    var emailMessageFurtherAlerts = "<br /><br />Further alerts will be provided if the second alert level is breached."
    var emailMessage = emailMessageIntro + emailSendTime + emailMessageBody + emailMessageFurtherAlerts + emailSignature + emailMessageEnding
  


    
    MailApp.sendEmail({
    to: emailList,
    subject: emailSubjectGain,
    htmlBody: emailMessage,
    name: 'Portfolio Alerts',
    inlineImages:emailImages}); 
  }
  
  // Portfolio Gain alert level 2 email
  if (portfolioDayChangePct >= portfolioGainAlert2Pct && sendCountTotalGainAlert1 == 1 && sendCountTotalGainAlert2 < 1 ){  
    
    sendCountGetGainAlert2.setValue(sendCountAddGainAlert2+1);
    
    // Adjusts the email message to include the alert level.
    var emailMessageIntro = emailMessageIntro + " has experienced a <strong>" + portfolioDayChangePctDisplay + "</strong> change in value today, breaching its <strong>second gain alert level of " + portfolioGainAlert2PctDisplay + "</strong>,"
    var emailMessage = emailMessageIntro + emailSendTime + emailMessageBody + emailSignature + emailMessageEnding


   
    
    MailApp.sendEmail({
    to: emailList,
    subject: emailSubjectGain,
    htmlBody: emailMessage,
    name: ' Portfolio Alerts',
    inlineImages:emailImages}); 
  }
}
}
  

// function to record in-day portfolio change
function inDayPortfolioChange() { 
    
  // Skip week-end
  // Sunday is day 0, saturday is day 6.
  var day = new Date();
  if (day.getDay() >0 && day.getDay() <6) {
  
  // creates the table of data
  var portfoliosheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Portfolio");
  var historicalsheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("In-Day Portfolio Change");
  var date = Utilities.formatDate(new Date, "Europe/London", "dd/MM/yyyy");
  var time = Utilities.formatDate(new Date, "Europe/London", "HH:mm");
  var total =portfoliosheet.getRange("M8").getValue();
  historicalsheet.appendRow([date, time, total]);
  }
}


// function to record portfolio data for asset types
function currentHistoricalPortfolioAssetType(parameters) {

  // Skip week-end
  // Sunday is day 0, saturday is day 6.
  var day = new Date();
  if (day.getDay() >0 && day.getDay() <6) {
  
  var portfoliosheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Portfolio");
  var historicalsheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Current Historical Portfolio (Asset Type)");
  var date = Utilities.formatDate(new Date, SpreadsheetApp.getActive().getSpreadsheetTimeZone(), "dd/MM/yyyy");
  var stocks = portfoliosheet.getRange("M3").getValue();
  var bonds = portfoliosheet.getRange("M4").getValue(); 
  var commodities =portfoliosheet.getRange("M5").getValue();
  var cash = portfoliosheet.getRange("M7").getValue();
  var total = portfoliosheet.getRange("M8").getValue();
  
 
  historicalsheet.appendRow([date, stocks, bonds, commodities, cash, total]);
 }
}

// function to record portfolio data for individual assets
function currentHistoricalPortfolioPerAsset(parameters) {

  // Skip week-end
  //Sunday is day 0, saturday is day 6.
  var day = new Date();
  if (day.getDay() >0 && day.getDay() <6) {
  
  var portfoliosheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Portfolio");
  var historicalsheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Current Historical Portfolio (Per Asset)");
  var date = Utilities.formatDate(new Date, SpreadsheetApp.getActive().getSpreadsheetTimeZone(), "dd/MM/yyyy");
  var asset1Total =portfoliosheet.getRange("M12").getValue();
  var asset1Quantity =portfoliosheet.getRange("D12").getValue();
  var asset2Total =portfoliosheet.getRange("M13").getValue();
  var asset2Quantity =portfoliosheet.getRange("D13").getValue();
  var asset3Total =portfoliosheet.getRange("M14").getValue();
  var asset3Quantity =portfoliosheet.getRange("D14").getValue();
  var asset4Total =portfoliosheet.getRange("M15").getValue();
  var asset4Quantity =portfoliosheet.getRange("D15").getValue();
  var asset5Total =portfoliosheet.getRange("M16").getValue();
  var asset5Quantity =portfoliosheet.getRange("D16").getValue();
  var asset6Total =portfoliosheet.getRange("M18").getValue();
  var asset6Quantity =portfoliosheet.getRange("D18").getValue();
  var asset7Total =portfoliosheet.getRange("M20").getValue();
  var asset7Quantity =portfoliosheet.getRange("D20").getValue();
  var asset8Total =portfoliosheet.getRange("M22").getValue();
  var total =portfoliosheet.getRange("M8").getValue();
  historicalsheet.appendRow([date, asset1Total, asset1Quantity, asset2Total, asset2Quantity, asset3Total, asset2Quantity, asset4Total, asset4Quantity, asset5Total, asset5Quantity, asset6Total, asset6Quantity, asset7Total, asset7Quantity, asset8Total, total]);
  }
}

// function to clear the in-day data
function resetSheetsData() {

  var sheetInDayPortfolioChange = SpreadsheetApp.getActive().getSheetByName("In-Day Portfolio Change");
  var sheetPortfolio = SpreadsheetApp.getActive().getSheetByName("Portfolio");
  var start, end;

  // Resets the sheet in preparation for next day.
  start = 4;
  end = 3000 - start; // Number of last row you want to delete
  sheetInDayPortfolioChange.deleteRows(start, end); 
  sheetInDayPortfolioChange.insertRows(4, 2996); // Shifts all rows down by three
  
  // Resets send count values in Portfolio sheet
  sheetPortfolio.getRange('C33').setValue("0");
  sheetPortfolio.getRange('C34').setValue("0");
  sheetPortfolio.getRange('C35').setValue("0");
  sheetPortfolio.getRange('C36').setValue("0");
}
