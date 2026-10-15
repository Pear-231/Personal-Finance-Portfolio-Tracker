# Google Apps Script development

This directory contains the Google Apps Script code. We use [Clasp](https://developers.google.com/apps-script/guides/clasp) to develop into Google Apps Script.

## Requirements

- Node.js
- The Google Apps Script API enabled for your Google account at https://script.google.com/home/usersettings.

## Setup

1. Install Clasp if you don't already have it:
   ```
   npm install @google/clasp -g
   ```

2. Authenticate Clasp:
   ```
   clasp login
   ```

3. Copy `.clasp.json.example`, remove the `.example` suffix, and then in the spreadsheet go to `Extensions > Apps Script`, open `Project Settings`, copy the `Script ID` and paste it the scriptId value in your .clasp.json.

4. To start automatic synchronisation to Apps Script run:
   ```
   clasp --project (Resolve-Path apps-script/.clasp.json) push --watch
   ```