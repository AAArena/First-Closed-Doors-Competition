**[<< Previous: Exchange API](./1b-Exchange-API.md)**



# Starting out Your Own T-Bot

## Step 1: Using an Existing T-Bot as a Starting Point

Now is a good time to sit and think about your trading strategy. Do you have one?

If you do have a strategy you wish to automate, then we are going to offer you a trading algobot template to start from: it's called [Mariam]( https://github.com/AAMasters/AAMariam-Trading-Bot). As her [README]( https://github.com/AAMasters/AAMariam-Trading-Bot/blob/master/README.md) file goes, Mariam is ideal as a "starting point laying out the proper ways to interact with the AACloud". However, her actual trading strategy is quite unusable. Start with Mariam if you are bringing your own logic.

If you don't have a strategy or are not sure about starting out from scratch, we have a friend you might want to meet: this is [Artudito]( https://github.com/AAMasters/AAArtudito-Trading-Bot). Artudito is an accomplished trader. He uses linear regression channels to determine when to buy or sell. Check his [README]( https://github.com/AAMasters/AAArtudito-Trading-Bot/blob/master/README.md) file for more details.

Starting out with an accomplished trading algobot is all about making incremental improvements on how the algobot does what he does. You might want to introduce new complementary logic to make him smarter, or simply polish his decision-making by studying his actual performance and ironing out the flaws you may see when taking a closer look.

Now that we've cleared that up, it's time to move on and set you up with your template. For simplicity's sake we are going to describe how to proceed with Mariam, but the exact same explanation should work if you choose to clone Artudito instead.

### A: Clone and Rename Algobot

We will use Mariam, a trading algobot within the AAMasters organization as a starting point for creating your own algobot. 

But let's first remember the kind of folder structure you wish to develop. You have already cloned AACloud and placed it somewhere in your hard drive. Now its a good time to create a folder at the same level of AACloud with the name of your Algobot Team GitHub organization.

```
.					# Top level directory located at your choice
├── AACloud				# Already cloned from git repository
└── AAYourTeam				# Directory named after your Algobot Team GitHub organization
    └── AAYourAlgobot-Trading-Bot	# The location where you should clone Mariam 
    					# only to rename the folder afterwards    
```

Clone [Mariam's repository](https://github.com/AAMasters/AAMariam-Trading-Bot) and –once in your local machine– rename the root folder with the name of your new algobot.

```
$ git clone https://github.com/AAMasters/AAMariam-Trading-Bot _AAYourBotName-Trading-Bot_
$ cd _AAYourAlgobotName-Trading-Bot_
```

Make sure you follow the naming convention using the following string:

"**AA**"+"**AlgobotName**"+"**-Indicator-Bot**" _or_ "**-Trading-Bot**"

e.g.: _AAMariam-Trading-Bot_

> NOTE: Make sure the algobot name is unique. That is, no other algobot by any other Algobot Team can have the same name. You can find the current list of algobots in the _[AAPlatform ecosystem.json file](https://github.com/AdvancedAlgos/AAPlatform/blob/master/ecosystem.json)_.

### B: Rename Solution

Now rename the solution using the following syntax: "**AA**"+"**AlgobotName**"+"**-TypeOfAlgobot-**"+"**Bot**"+"**.sln**"

e.g.: _AAMariam-Trading-Bot.sln_

```
$ mv  AAMariam-Trading-Bot.sln _AAYourAlgobot-Trading-Bot.sln_
```

### C: Remove .git Folder

Next, delete the hidden _.git_ folder to eliminate the relationship with the original GitHub repository.

```
$ rm -rf .git
```

### D: Create New Repository

Now you are going to use GitHub Desktop to turn the recently renamed folder back into a GitHub repository, this time with the name of your own bot. This is what you need to do:

1. Go to GitHub Desktop, click _File > New Repository...

![GitHub Desktop](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/GitHub-Desktop-03.png)

2. In the _Name_ field, type the exact same name you gave to the folder (better to copy and paste it). The name should look somewhat like _AAYourAlgobot-Trading-Bot_.

3. In the _Description_ field, type a short description about the kind of strategy your t-bot will feature.

4. In the _Local path_ field, choose the path to the folder containing the t-bot's folder (if you followed our recommendations that should be somewhat in the lines of _AAYourTeam_).

5. Leave the rest of the fields in their default state and click _Create Repository_.

![GitHub Desktop](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/GitHub-Desktop-04.png)

6. Now GitHub Desktop will show the newly created repository as the current repository and will offer a _Publish Repository_ button in the top / center of the app. Click the _Publish Repository_ button...

![GitHub Desktop](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/GitHub-Desktop-05.png)

7. Uncheck _Keep this code private_, select your organization from the drop down menu and click _Publish repository_.

This last step published your algobot's code, effectively creating a repository in your organization at github.com. You may go and check yourself if you wish.

### E: Request a Storage Container

Bots store data in the cloud. For the time being, the process for setting up a storage container for your Algobot Team is manual. Please send us a request to set up a storage container over Telegram; include your Github Organization and algobot's name, please. When the request is processed, you will get the three following items:

#### 1. Your Algobot Team Connection String

A text string similar to the following one:

```
DefaultEndpointsProtocol=https;AccountName=aayourteam;AccountKey=o1+ImM1zafasYOgf6Npmza+oGDjf7R2dRFEfXv7zF9krgIlgXtUCrNQE+UjAq3DR9u7JdFi684Wl/DWJlLvnwyWT9Q==;EndpointSuffix=core.windows.net
```

Create a folder named _Connection-Strings_ at the same level of the platform's repository (out of the folder AACloud). Inside it, create a subfolder named _Testnet_.

Open Notepad or any other basic text editor and create a file with the following content, making sure you place the supplied connection string in the appropriate place:

```
{
"useDevelopmentStorage": false,
"connectionString": "PLACE_YOUR_CONNECTION_STRING_HERE",
"accountName": "",
"accountKey": "",
"sas": ""
}
```

Save the file inside _Connection-Strings > Testnet_ naming it as follows:

"**AA**" + **YourTeam** + "**.azure.storage**" + **.connstring**"

e.g.: AAYourTeam.azure.storage.connstring

#### 2. Other Algobot's Connection Strings

The t-bot you cloned –Mariam– uses datasets that other algobots produce, thus, your t-bot will need connection strings for those other algobots. You will get these connection strings in files that you will need to place inside _Connection-Strings > Testnet_ folders.

#### 3. SAS Token

```
?sv=2017-07-29&ss=f&srt=sco&sp=rl&se=2018-12-31T04:47:12Z&st=2018-03-01T20:47:12Z&spr=https&sig=VFMzqZUyr%2aTEyu53dHV60Zib0hb1PTqzcqEKAl97aLvA%3D
```

You will use the SAS token in the next step.

### F: Configure Your Algobot

Open _this.bot.config.json_, a file within your algobot's repository. Let's review and modify the config file segment by segment:

```
{
  "displayName": "Mariam",
  "codeName": "AAMariam",
  "type": "Trading",
  "version": {
    "major": 1,
    "minor": 0,
    "patch": 0
  },
```
You need to update that segment of the config with the following things in mind:

 - *displayName* (your algobot's name without the AA prefix; e.g. Mariam)
 - *codeName* (name with the AA prefix; e.g. AAMariam)
 - *version* (start with major:0, minor:1, patch:0 – increase minor until you release your algobot; once you do, change to major:1, minor: 0)

```
  "devTeam": "AAMasters",
  "profilePicture": "Mariam.png",
  "dataSetVersion": "dataSet.V1",
```

 - *devTeam* (your organization's name including the AA prefix)
 - *profilePicture* (your algobot's picture - change Mariam's picture with one appropriate for your t-bot)
 - *dataSetVersion* (different versions of algobots may use different versions of datasets)

```
  "processes": [
    {
      "name": "Trading-Process",
      "description": "Simple trading strategy to be used as a template.",
      "startMode": {
        "live": {
          "run": "true",
          "resumeExecution": "false"
        },
        "backtest": {
          "run": "false",
          "beginDatetime": "2018-04-12T16:00:00.000Z",
          "endDatetime": "2018-04-12T16:15:00.000Z",
          "waitTime": 1000
        },
        "competition": {
          "run": "false",
          "beginDatetime": "2018-04-27T16:00:00.000Z",
          "endDatetime": "2018-04-28T16:05:00.000Z",
          "resumeExecution": "false"
        }
      },
```

 - *description* (briefly describe your algobot's strategy)
 - *startMode* There are three ways in which your t-bot can be run and only one of them should be set to _true_:
   - _live_ means real live trading,
   - _backtest_ allows testing your strategy against historical data,
   - _competition_ means real trading within a competition

```
      "normalWaitTime": 60000,
      "retryWaitTime": 10000,
      "sleepWaitTime": 3600000,
      "comaWaitTime": 86400000,
```
These parameters affect the frequency with which the algobot is run and wait periods in case of certain events. Leave them at the default value for the time being.

```
      "statusDependencies": [
        {
          "devTeam": "AAMasters",
          "bot": "AAMariam",
          "botVersion": {
            "major": 1,
            "minor": 0
          },
          "process": "Trading-Process",
          "dataSetVersion": "dataSet.V1"
        }
      ],
```

This is a declaration of Status Dependencies, meaning the status reports the t-bot consumes. If your t-bot needs status reports from other algobots, this is where you need to configure those dependencies. In the meantime, replace the _devTeam_ with your own team and _bot_ with the name of your bot. Make sure you use the same values for _major_ and _minor_ you used before.

```
      "dataDependencies": [
        {
          "devTeam": "AAMasters",
          "bot": "AAOlivia",
          "botVersion": {
            "major": 1,
            "minor": 0
          },
          "product": "Candles",
          "dataSet": "Multi-Period-Market",
          "dataSetVersion": "dataSet.V1"
        },
        {
          "devTeam": "AAMasters",
          "bot": "AAOlivia",
          "botVersion": {
            "major": 1,
            "minor": 0
          },
          "product": "Candles",
          "dataSet": "Multi-Period-Daily",
          "dataSetVersion": "dataSet.V1"
        },
        {
          "devTeam": "AAMasters",
          "bot": "AABruce",
          "botVersion": {
            "major": 1,
            "minor": 0
          },
          "product": "Candles",
          "dataSet": "One-Min",
          "dataSetVersion": "dataSet.V1"
        }
      ]
    }
  ],
```

These are declarations of Data Dependencies, that is, data from other algobots that Mariam consumes. If your algobot consumes data from other algobots, this is where you need to declare those dependencies.

```
  "products": [
    {
      "codeName": "Live Trading History",
      "displayName": "Live Trading History",
      "shortDisplayName": "Live",
      "description": "General information about Mariam live trading history.",
      "storageAccount": "aamariam",
      "dataSets": [
        {
          "codeName": "Backtest History",
          "type": "File Sequence",
          "validPeriods": [ "24-hs", "12-hs", "08-hs", "06-hs", "04-hs", "03-hs", "02-hs", "01-hs", "45-min", "40-min", "30-min", "20-min", "15-min", "10-min", "05-min", "04-min", "03-min", "02-min", "01-min" ],
          "filePath": "@DevTeam/@Bot.1.0/AACloud.1.1/Poloniex/dataSet.V1/Output/Trading-Process",
          "fileName": "Execution.History.Live.@Sequence.json"
        }
      ],
      "exchangeList": [
        {
          "name": "Poloniex"
        }
      ],
      "plotter": {
        "devTeam": "AAMasters",
        "codeName": "PlottersTrading",
        "moduleName": "History"
      }
    },
  ```

Bots output certain products. AACloud keeps track of algobots activities in different running modes and makes it publicly available, for transparency purposes.

The config segment above shows the configuration of the first and most important product all trading algobots output: the Live Trading History.

**DO NOT FORGET:**
 **- *storageAccount* (replace with the one assigned to you)**

```
    {
      "codeName": "Backtest Trading History",
      "displayName": "Backtest Trading History",
      "shortDisplayName": "Backtest",
      "description": "General information about Mariam backtest trading history.",
      "storageAccount": "aamariam",
      "dataSets": [
        {
          "codeName": "Backtest History",
          "type": "File Sequence",
          "validPeriods": [ "24-hs", "12-hs", "08-hs", "06-hs", "04-hs", "03-hs", "02-hs", "01-hs", "45-min", "40-min", "30-min", "20-min", "15-min", "10-min", "05-min", "04-min", "03-min", "02-min", "01-min" ],
          "filePath": "@DevTeam/@Bot.1.0/AACloud.1.1/Poloniex/dataSet.V1/Output/Trading-Process",
          "fileName": "Execution.History.Backtest.@Sequence.json"
        }
      ],
      "exchangeList": [
        {
          "name": "Poloniex"
        }
      ],
      "plotter": {
        "devTeam": "AAMasters",
        "codeName": "PlottersTrading",
        "moduleName": "History"
      }
    },

```
The above segment shows the configuration of the Backtest History product.

**DO NOT FORGET:**
 **- *storageAccount* (replace with the one assigned to you)**

```
    {
      "codeName": "Competition Trading History",
      "displayName": "Competition Trading History",
      "shortDisplayName": "Competition",
      "description": "General information about Mariam competition trading history.",
      "storageAccount": "aamariam",
      "dataSets": [
        {
          "codeName": "Backtest History",
          "type": "File Sequence",
          "validPeriods": [ "24-hs", "12-hs", "08-hs", "06-hs", "04-hs", "03-hs", "02-hs", "01-hs", "45-min", "40-min", "30-min", "20-min", "15-min", "10-min", "05-min", "04-min", "03-min", "02-min", "01-min" ],
          "filePath": "@DevTeam/@Bot.1.0/AACloud.1.1/Poloniex/dataSet.V1/Output/Trading-Process",
          "fileName": "Execution.History.Competition.@Sequence.json"
        }
      ],
      "exchangeList": [
        {
          "name": "Poloniex"
        }
      ],
      "plotter": {
        "devTeam": "AAMasters",
        "codeName": "PlottersTrading",
        "moduleName": "History"
      }
    }
  ]
}
```

Finally, the last product configured is the Competition Trading History.

**DO NOT FORGET:**
**- *storageAccount* (replace with the one assigned to you)**

## Step 2: Configure the AACloud

In the AACloud folder, open _this.config.json_, make the changes as explained below and save.

```
{
  "codeName": "AACloud",
  "version": {
    "major": 1,
    "minor": 1,
    "patch": 0
  },
  "executionList": [
    {
      "enabled": "false",
      "botPath": "../Bots/AAMasters/AAMariam-Trading-Bot",	# Enter the path to your t-bot's project folder
      "process": "Trading-Process"				# up to the last folder only.
    },
    {								# AACloud is prepared to run multiple algobots
      "enabled": "false",					# each with it's own processes.
      "botPath": "../Bots/AAMasters/AAOlivia-Indicator-Bot",	#
      "process": "Multi-Period-Market"				# When you clone AACloud
    },								# you may find different algobots
    {								# showing up in the configuration file,
      "enabled": "false",					# just like the ones here.
      "botPath": "../Bots/AAMasters/AACharly-Extraction-Bot",	#
      "process": "Poloniex-Hole-Fixing"				# Delete the entries you are not using,
    },								# making sure you delete the comma
    {								# after your algobot.
      "enabled": "true",					
      "botPath": "../Bots/AAMasters/AABruce-Indicator-Bot",	
      "process": "One-Min-Daily-Candles-Volumes"		
    }								
  ],
  "stopGracefully": "true",		# 'false' for continuous run, 'true' for one run only.
  "storageConnStringFolder": "Mixed",	# 'Testnet', 'Mixed' or 'Production' indicate which folders to look in for conn strings
  "maxLogLoops": 10			# The number of loops you wish to log.
  "marketRateProvider": {
    "devTeam": "AAMasters",
    "bot": "AABruce",
    "botVersion": {
      "major": 1,
      "minor": 0
    },
    "product": "Candles",
    "dataSet": "One-Min",
    "dataSetVersion": "dataSet.V1"
  }
}
```

### Path

Change the path to the proper one pointing to your algobot in your local machine. Bear in mind the path is relative to where the _AACloud.sln_ is located. Do not include the actual _.sln_ file in the path; only the containing folder is expected.

Make sure you delete the entries corresponding to bots you are not running, making sure the json file remains valid (you need to delete the comma after your algobot's declaration).

### Stop Gracefully

When you run a trading algobot in your local environment you can configure the AACloud to run it either continuously or only once. This is to avoid the consequences of stopping a trading algobot forcefully, which may cause the t-bot to loose sync with the exchange (open positions may not be taken into account in subsequent runs).

This is where the _stopGracefully_ parameter comes into play. When the value is _false_ the platform will run the t-bot continuously. When the value is _true_ the platform runs the t-bot once and stops it afterwards.

If you ran the t-bot with _"stopGracefully": "false"_ and need to stop the execution, then simply go back to the config, change the parameter to _true_, save the file and wait. Upon the next run, the algobot will be stopped.

### Connection String Folders

In addition, the file Run.js allows you to tell the AACloud whether you wish to run your t-bot againt testnet or production data (or both). However, your connection credentials only work in the development environment, so stick with Testnet.

### Configure Which Process to Run

Now we need to tell the platform which process to run. Click on the AACloud node and make sure the value for the Script arguments field is "_Trading-Process_":

![VS](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Visual-Studio-02-TB.png)

## Step 3: Test Run

### Execute

Once running, the process should call the command prompt and start showing some activity:

![VS](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Command-Prompt-01.png)

## Step 4: What to Expect After Execution

Once you run the AACloud and the platform calls the t-bot and process you just configured, you will not _see_ much more than the command prompt popping up, as described earlier. Do not expect any graphics, browser windows or candlestick charts to pop up.

The visualization of algobots activity over a candlestick chart happens at AAWeb, discussed in the [Watching Algobots in Action](../Algobots-in-action.md) section. We will review that later on but feel free to take a peek if you wish.

In the meantime, what you can review the dataset generated by the t-bot in the form of _.json_ files stored in the cloud, the logs stored locally and the orders that may have been placed in your account at the exchange.

### Output

You should be able to browse the output of the t-bot using the Azure Storage Explorer with the connection string we provided for your algobot earlier.

T-bots have two main outputs: the execution context and the execution history; the former can be of three different types depending on what mode the t-bot is running (backtest, live and competition).

#### Execution Context

It stores one blob per execution, thus one blob per minute, with information regarding the t-bot's business, including values of each variable such as balances, profit, positions and so on.

#### Execution History

Its a registry that keeps track of each execution, and is stored in a sequence of blobs. It is mostly used to plot t-bot's activity in AAWeb's timeline.

### Logs

Upon execution, the platform creates a folder named _Logs_ right outside the platform's repository. Thus, you will find the Logs folder in the same directory as the AACloud folder. Each algobot stores logs in its own sub-folders.

### Debugging

By now you should be able to run the t-bot in your local environment and use typical debugging tools and procedures should anything go wrong.

In case you were not able to successfully run the t-bot, the logs files are the first place to go.

### Quick Logs Overview

Logs are segregated per each execution so that it is easy to locate log files corresponding to different executions. The separation is accomplished by the folder structure itself.

```
.
├── AACloud              
├── Logs > [year] > [month] > [day] > [hour] > [minute ]	# Folder structure showing execution datetime

		└── _Your_Team_ 				# Directory named after your team
	  		 └── Trading 				# Named after type of algobot (e.g. Trading, Indicator, etc)
		 	  	└── _YourBot_ver_    		# Named after your algobot and Version
		 	  		└── _Process_    	# Named after the specific process			
			   			└── ...logs 	# See below for details			   
```
**Log name format:** _Date(Yr-Mo-Day-Hr-Min)–RandId–SourceFile.log_
\* _SourceFile_ is the name of the AACloud file to check for associated error or output.

**Selected Log Guide:\***
1.  _~.This.Bot.log:_ Errors and outputs specific to your algobot in its repository. All other logs point to CloudPlatform files.
2.  _~.Exchange Api.log:_ Output from exchange API
3.  _~.Assistant.log:_ Trading actions between t-bot and exchange
4.  _~.Datasource.log:_ Data accessed from storage by your algbots
5.  _~File Storage.\_Bot\_.log:_ Data access from storage by listed algobot
6. _~.trading algobot Main Loop.log:_ Best log to narrow down general cloud platform issues

\*_By closest relationship to your algobot. Read source code for more detailed comments and to view other files associated with the cloud platform_

If you wish to debug the platform and your algobot, open the _IntervalExecutor.js_ module and place a breakpoint in the following line:

```
fileProcessingInterval.start(loopControl);
```

Now, run the IDE. When execution halts, press F11 to step into the module _User.Bot.js_ that will be loaded from the configured algobot process folder. Once there you can set more breakpoints or debug the module step by step.

## Step 5: Start Coding

Once you have managed to run the t-bot successfully, you are good to go. We've found the following workflow is quite practical:

* The main business logic/solution to edit is in  (_Your-Bot-Repo > Trading-Process > User.Bot.js_). Other types of algobots (e.g. indicator or extraction) have different process folder types.

* Your t-bot will not fully successfully run until there is a balance in your Poloniex account and your t-bot can make an actual trade. The t-bot status report will also not be written to your storage account until then. You can use the simulation mode described above (_exchangeSimulationMode_ in the AACloud config) for a temporary workaround until you fund your account.

* Code directly in the t-bot's solution until the code is fully implemented.

* Close the t-bot's module and go to the cloud platform solution to debug (as explained above). While debugging, the t-bot's files will pop up in separate tabs, so that you can edit the code in the process.

<hr />

**[Next: Launching Your Algobot >>](./3-LaunchingYourAlgobot.md)**

[Terms of Service](../Terms.md)  &bull;  [Disclaimer](../Disclaimer.md)

<hr />

**Table of Contents:** [Basic Definitions](../README.md/#basic-definitions) | [About The Competition](../TheCompetition.md) | [The AAPlatform](../AAPlatform.md) | [About Algobots](../Algobots.md) | [Setting Up Your Development Environment](./0-Setup.md) | [Trading Algobots](./1-TradingAlgobots.md) | [Exchange API](./1b-Exchange-API.md) | [Starting Out Your Own Algobot](./2-YourOwnAlgobot.md) | [Launching Your Algobot](./3-LaunchingYourAlgobot.md) | [Watching Algobots in Action](../Algobots-in-action.md) 

