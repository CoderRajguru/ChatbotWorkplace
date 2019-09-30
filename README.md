# Help@ Bot
A sample help bot for Workplace which can act as an online admin answering questions it is asked by simply querying from a google or office 365 Spread sheet. 


What can the bot be used for ? 

* FAQ Bot : Bot that answers frequently asked questions for any product/feature/process
* Admin Bot : Common asked questions about organisation/company for employees 
* Acronym Bot : Can be used as a simple acronym bot used by noobs to help understand the meanings for multiple acronyms or terms used in the company
* Company quick links : There are multiple portals and docs in a company. Instead of maintaining bookmarks 

How does it work ? 

![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/helpbut_setup.png)


* Workplace Admin updates the google sheet with all the necessary information. The sheet can be accessed and updated by anyone (irrespective of their work background)
* Workplace user queries the bot(@Help) for information about any specific topic
* @Help Bot  queries the sheets and replies back to the user
* In case a query made to the bot is absent in the sheets then the @help bot pings the admin with the unavailable query to update the sheet

HelpBot Demo.mov (https://quip.com/2/blob/VfHAAAaErCb/rGqU48PHn17c-Q7fZ54e0Q?name=HelpBot%20Demo.mov) 


How to deploy @Help Bot to your workplace?

We can split the process to three major steps

* Google Sheet Setup
* Development/Deployment of Code
* Workplace Admin Setup



 Google Sheets API Setup 

As the bot refers to the spreadsheet to get the answers for the queries it gets , it is very important to configure the google spreadsheet (https://www.google.com/sheets/about/)
To programmatically access(which the Bot will do) your spreadsheet, you’ll need to create a service account and OAuth2 credentials from the Google API Console (https://console.developers.google.com/)

* *Go to the Google APIs Console (https://console.developers.google.com/)*
* *Create a new project*

![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/create_project.png)



* *Click Enable API. Search for and enable the Google Drive API.*

![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/enable_API.png)

![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/enable_API_2.png)


* *Create credentials for a Web Server to access Application Data.*

![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/choose_webserver.png)

* *Name the service account and grant it a Project Role of Editor.*

![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/account_key_setup.png)

* *Download the JSON file.*


![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/save_key.png)

* *Copy the JSON file to your code directory and rename it to client_secret.json*
* *Create a new google sheet and enter the queries/answers*


![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/setup_googlesheet.png)

*Index* - # of items in the sheet 
*Tag - *Quick/easy look up for the user queries 
*FAQ Question - * User queries for Bot
*meaning/def/more - *Detailed answer for each query received 

* *Find the client_email inside client_secret.json. Back in your spreadsheet, click the Share button in the top right, and paste the client email into the People field to give it edit rights. Hit Send.*

![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/share_sheet.png)


Deployment/Code setup

* The code can be found here : https://github.com/Bikashforworkplacenew/HelpBot-Workplace

* The project has 3 files which we needs to be modified/changed according to your needs [You can always deploy the project as it is without changing too]
    * *client_secret.json(HelpBot-Workplace/utilities/client_secret.json)[*Mandatory*]*
        * You need to replace the client_secret.json in the project with the one that you saved in the previous step
    * *.env(HelpBot-Workplace/.env)[*Mandatory*]* 
        * Please modify/add the necessary details to this file
        * This is your config file which can be edited at any point of time 
        * It contains the google sheet ID/ google sheet links and Workplace_Admin_ID
        
        ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/environment_variable.png)
        
    * *messages.js (HelpBot-Workplace/utilities/messages.js)[*OPTIONAL*]*
        * Most Important : Make sure to get the columns names right from the spreadsheet set up 

e.g. in here the column names (“meaning”,“def”) is same as the ones being extracted in the code

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/botqueries_column.png)
 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/column_code.png)
        
        * You can add your own welcome message 

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/intro_mesage.png)

        * Add the necessary aesthetics checks 


 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/aesthetic_check.png)

        * Add your own custom admin message in case any query from the sender is not found 
* After making the changes you can deploy the code in any web server 
* In this example I have used Heroku to deploy my code and make all the configuration 
    * You can create a new app in Heroku
    

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/heroku_newapp.png)


* As my code is pushed to Github, i am choosing github account project 

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/connect_github.png)


* Make sure you “Enable Automatic Deploys” after deploying branch

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/auto_deploy.png)

* There is one final step that you need to do which we will complete after the Workplace Setup 

Workplace Admin Setup

* Admin needs to create a custom integration in the Admin Panel of workplace account

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/admin_panel.png)

*   Click on the “Create custom integration” button

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/create_custom_integration.png)

*  Enter a name for the integration, which will be the name of your chat bot, and click on the “Create” button. You will now be able to configure the permissions of the integration. Enable the “Message any member” permission and click on the “Create access token” button.

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/integration_setup.png)

*  Copy the access token, enable the “I understand” checkbox and click on the “Done” button

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/access_token.png)

Configuring Values for Workplace and Heroku

 ![alt text](https://github.com/Bikashforworkplacenew/HelpBot-Workplace/blob/master/images/heroku_config_values.png)

*  Return to the settings page of the Heroku application and paste the access token that you've just copied in the ACCESS_TOKEN value.
* Copy the App ID and App Secret of the Workplace integration and paste it in the APP_ID and APP_SECRET values
     Return to the integration configuration in Workplace and scroll all the way down until you see the configure webhooks section. Enable the “messages” checkbox and specify the following fields:
    
* Callback URL: https://[name of your Heroku application].herokuapp.com/webhook (https://herokuapplicationname.herokuapp.com/webhook)
    * The name of the Heroku application can be found by clicking on the “Open app” button in the Heroku application. This will then open a new tab where the name of the application will be the first part of the url (e.g. https://wp-helpbot.herokuapp.com/ (https://wpsamples-hellobot.herokuapp.com/) will become https://wp-helpbot.herokuapp.com/webhook)
    * Verify Token: workplacesample
    *  Return to the Heroku settings page and fill out the remaining values as followed
        
    * SERVER_URL: https://[name of your Heroku application].herokuapp.com/ (https://herokuapplicationname.herokuapp.com/webhook)
    * VERIFY_TOKEN: workplacesample



*  Return to the integration configuration in Workplace, scroll all the way down and click on the “Save” button.
     When you click on the “Save” button, you should return to the main custom integrations page
    
* Verify that the Workplace Chat bot is working

