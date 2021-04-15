# Vaccine Registration Tool

This project is a free lightweight mobile-friendly web tool for registering, scheduling, notifying, managing, and reporting COVID-19 vaccinations.  It attempts to provide a digital workflow reducing the burden of manual paperwork and processes for small/medium vaccination clinics that may not have the IT infrastructure to build thier own tools. Centralized infrastructure can be challenging to access, use, adapt and may not account for onsite workflows.  As vaccination distribution grows, these tools hope to help smaller clinics operate more efficiently allowing more vacinations per staff.  As technology or transportion limited individuals become a larger percentage of the target population, staff responsiblies will only increase taking time away from administering vaccinations.

It only requires a free Google account to host the project using Google Sheets as the database, Google Drive to store images, and Gmail for messages.  All of the data is stored in (and most of the configuration can be done by editting) a Google Sheet. This means the data is easily edittable and exportable to other EMR systems. It is built using [App Script](https://developers.google.com/apps-script) to automatically create web forms/pages for creating, displaying, and updating data in the spreadsheet. Photos of ID cards can be caputred using the mobile phone camera, stored in Google Drive, and are associated with patient records.

If [Google Cloud Vision Services](https://cloud.google.com/vision) are enabled on your hosting account, it can also perform text recognition on insurance cards and photo IDs for much faster (and less error prone) check-in process.  This service is free for the first 1000 queries/month, with a [modest cost for additional queries/month](https://cloud.google.com/vision/pricing).

You can play with a [early prototype instance of the tool](https://script.google.com/macros/s/AKfycbwM92Cxn9iD-ePMKojsJS0RhWIcCZBfn_h50M8RgHiR2rJxIM6dIUzLEX-ojEIYcAisuQ/exec).  It is under VERY active development.

## Setup your own instance

This section is very much work in progress.

This in an [App Script](https://developers.google.com/apps-script) project that runs on Google Docs.  Hosting an instance requires a free Google Account.   You can reuse an account you have. However, this account will be the administrator with full priveldges to the data and scripts.  Do not share the account creditials to anyone you would not trust to delete or copy the patient information safely.  **Reminder: This project IS NOT HIPAA compliant**.  It is provided in hopes in may be useful where that is not needed.

It also uses a Chrome extension, to help with synching with Github.  So, these instructions will assume you are using the [Chrome Browser](https://www.google.com/chrome).

1. Download and install [Google Chrome Browser](https://www.google.com/chrome)
2. If you don't already have a Google account you want to use as host, you can [create a new Google Account](https://accounts.google.com/signup).
3. (optional) Install the [Google App Script Github Assistant](https://chrome.google.com/webstore/detail/google-apps-script-github/lfjcgcmkmjjlieihflfhjopckgpelofo).  Click add to Chrome.
4. (optional) Github is very useful for saving and managing versions of coding project.  It is recommended, but not required.  If you don't already have a Github account you want to use, create a new [Github account](https://github.com/).  If you are a programmer and want to contribute back to the main project, you can fork this repository rather than copying the AppScript project below.  However, configuring this is beyond the scope of this readme.
5. Create new folder on Google Drive that you want to be the project's main directory.  Look at the URL for a long string of numbers and letters.  'https://drive.google.com/drive/folders/1zOu5qg7VCP4tz1BFyZJDSwGGZmAyflal'. The is your project directory ID: 1zOu5qg7VCP4tz1BFyZJDSwGGZmAyflal.  You will need this later.
6. Create spreadsheet from this template (link TBD - or autocreate the spreadsheet from within appscript?).  Look at the URL for a long string of numbers and letters.  Example 'https://docs.google.com/spreadsheets/d/163XoWSUqz2MjaMewZEi0hxOEpDFdJgfgfR2SL_0NDco/edit#gid=0'. This is your spreadsheet ID: 163XoWSUqz2MjaMewZEi0hxOEpDFdJgfgfR2SL_0NDco.  You will need this later.
7. Open this copy of the [AppScript project](https://script.google.com/d/1O38qwdfY_Pycg1hFUm-Ocm7wKxHrqfuI3feZr-7-ci8cVTEX1tTV6AW7/edit?usp=sharing) for this repository.  Click on the 'i' icon in the left panel to see the project overview.  On the upper right, click on 'Make a copy' to create your own copy of this project.  Then click on the title to rename the project to your own.
8. (optional) If you've installed the Google App Script Github Assistant, you should see 'Repository', 'Branch', and 'Login into SCM' in the menu bar.  Click on 'Login to SCM' and log into Github.  It may ask you for a Github Access Token.  Follow the link to create a new token with the **repo** scope.  Copy and paste the new token in to th login page.  You will directed to approve GasHub to access you account, say Allow. Back in the Google App Script editor, click on 'Repository'.  Select "Create New Repo".  Then press the up arrow in the menu to upload your copy of the you AppScript project to your Github account.  It will show you a window called "Diff" showing you the differences in the files.  Scroll to the bottom and add a description like "initial commit" and press "Push".  In a moment, it copy all the files in your project to Github for safe keeping and version control, allowing your to recover old versions if needed.
9. Open config.gs, and you will need to modify 'YOUR_SPREADSHEET_ID' and 'YOUR_PROJECT_FOLDER_ID' to be the long string of characters from the previous steps to tell this project what files/directory to use for the project.
10. Click on the file Code.gs, and press run.  In a moment, it will say "Authorization Required".  Click "review permissions".  Select your host account. It will warn you that "Google hasn't verified this app."  Since this is a custom app of which you are now the developer, this is correct.  You are approving this to make modifications to files in your Google Drive.  Click "Advanced" and "Go to name of your app".  It will list the edit rights that the application needs to your files (Google Drive, Google Sheets, Gmail, external Vision service) then hit "Allow".
11. In a moment it should say "run from editor complete" in the Execution Log.  This means everything went correctly.
12. Open config.gs, and you will need to modify 'YOUR_SPREADSHEET_ID' and 'YOUR_PROJECT_FOLDER_ID' to be the long string of characters from the previous steps to tell this project what files/directory to use for the project.
13.  Now click on "Deploy".  Select "New Deployment", which will create a live instance of the website.  Select Type > Web app.  Add a decription like "Inital Test".  Under configuration > Web app, set "Execute as" Me to enable access your account data.  Set "Who has access" to be "Only myself" while you are testing.  Then hit "Deploy".
14.  Under Web app, you should now see a URL that you can click on, which will open a new tab to the live running Web app.
15.  When doing rapid edits, you can use Deploy > Test Deployments to create a web app instance that will refresh everytime you save your changes in the editor.  This avoids having to create a new deployment for each small change you make.
16. (optional) If you have the Github assistant installed, you can puload/push your code changes to Github for safe keeping allowing you to roll back code changes in case something happens.  This is particularly valuable if you are using multiple computers to edit the project.  The App Script IDE does not sync changes between browsers. So old browser state, can overwrite new edits. 
17.  Once you are ready anyone on the internet to use your Web app, create a New Deployment and set "Who has access" to "Anyone".  You will get a new URL, that you can now share with others.  You should see data appear in the your Google sheet.
