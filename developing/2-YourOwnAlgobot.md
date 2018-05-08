**[<< Previous: Trading Algobots >>](./1-TradingAlgobots.md)**



# Starting out Your Own t-Bot

## Step 1: Using an Existing t-Bot as a Starting Point

Now is a good time to sit and think about your trading strategy. Do you have one?

If you do have a strategy you wish to automate, then we are going to offer you a trading algobot template to start from: it's called [Mariam]( https://github.com/AAMasters/AAMariam-Trading-Bot). As her [README]( https://github.com/AAMasters/AAMariam-Trading-Bot/blob/master/README.md) file goes, Mariam is ideal as a "starting point laying out the proper ways to interact with the AACloud". However, her actual trading strategy is quite unusable. Start with Mariam if you are bringing your own logic.

If you don't have a strategy or are not sure about starting out from scratch, we have a friend you might want to meet: this is [Artudito]( https://github.com/AAMasters/AAArtudito-Trading-Bot). Artudito is an accomplished trader. He uses linear regression channels to determine when to buy or sell. Check his [README]( https://github.com/AAMasters/AAArtudito-Trading-Bot/blob/master/README.md) file for more details.

Starting out with an accomplished trading algobot is all about making incremental improvements on how the bot does what he does. You might want to introduce new complementary logic to make him smarter, or simply polish his decision-making by studying his actual performance and ironing out the flaws you may see when taking a closer look.

Now that we've cleared that up, it's time to move on and set you up with your template. For simplicity's sake we are going to describe how to proceed with Mariam, but the exact same explanation should work if you choose to clone Artudito instead.

### A: Clone and Rename Bot

We will use Mariam, a trading algobot within the AAMasters organization as a starting point for creating your own bot. Clone [Mariam's repository](https://github.com/AAMasters/AAMariam-Trading-Bot) and –once in your local machine– copy and paste the repository's root folder, renaming it with the name of your new bot.

```
$ git clone https://github.com/AAMasters/AAMariam-Trading-Bot _AAYourBotName-Trading-Bot_
$ cd _AAYourBotName-Trading-Bot_
```

Make sure you follow the naming convention using the following string:

"**AA**"+"**BotName**"+"**-Indicator-Bot**" _or_ "**-Trading-Bot**"

e.g.: _AAMariam-Trading-Bot_

> NOTE: Make sure the bot name is unique. That is, no other bot by any other Algobot Team can have the same name. You can find the current list of bots in the _[AAPlatform ecosystem.json file](https://github.com/AdvancedAlgos/AAPlatform/blob/master/ecosystem.json)_.

> NOTE: Having fun is essential; naming your bot offers a good chance to do just that. Feel free to name your bot after a good friend or go crazy with whatever character makes you laugh.

### B: Rename Solution (Optional: VS IDE only)

Now rename the solution using the following syntax: "**AA**"+"**BotName**"+"**-TypeOfBot-**"+"**Bot**"+"**.sln**"

e.g.: _AAMariam-Trading-Bot.sln_

```
$ mv  AAMariam-Trading-Bot.sln _AAYourBotName-Trading-Bot.sln_
```

### C: Remove .git Folder

Next, delete the hidden _.git_ folder to eliminate the relation to the original GitHub repository.

```
$ rm -rf .git
```

### D: Add GitHub Repository

Now is a good time to go to GitHub and add a new local repository within your own organization. Name the repository after your bot (use the exact same name as the root folder). Make sure you include a concise description of what the bot does. Upload the files in your local repository to the GitHub repository so that GitHub takes control of the association between your local files and the ones at GitHub.

#### Using Git CLI:
After creating new empty repository in Github without creating README or other files
```
$ git init
# initialize local repository
$ git add .
# Track all local files
$ git commit -m "Clone bot"
# Make first commit
$ git remote add origin _YourRemoteRepositoryURL
# e.g. https://github.com/YourTeam/AAYourBot-Trading-Bot.git
$ git remote -v
# Verifies the new remote URL
$ git push -u origin master
# Pushes the changes in your local repository up to the remote repository you specified as the origin
```

### E: Request a Storage Account

Bots store data in the cloud. For the time being, the process for opening a storage account for your bot is manual. Please send us a request to open a storage account over Telegram; include your Github Organization and bot's name, please. When the request is processed, you will get the following:

#### Your Algobot Team Connection String

A text string similar to the following one:

```
DefaultEndpointsProtocol=https;AccountName=aayourbot;AccountKey=o1+ImM1zafasYOgf6Npmza+oGDjf7R2dRFEfXv7zF9krgIlgXtUCrNQE+UjAq3DR9u7JdFi684Wl/DWJlLvnwyWT9Q==;EndpointSuffix=core.windows.net
```

Create a folder named _Connection-Strings_ at the same level of the platform's repository (out of the folder AACloud). Inside it, create a subfolder named _Production_.

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

Save the file inside _Connection-Strings > Production_ naming it as follows:

"**AA**" + **BotName** + "**.azure.storage**" + **.connstring**"

e.g.: AAMariam.azure.storage.connstring

#### Other Bot's Connection Strings

The bot you cloned –Mariam– uses datasets that other bots produce, thus, your bot will need connection strings for those other bots. You will get these connection strings in files that you will need to place inside _Connection-Strings > Production_ folders.

#### SAS Token

```
?sv=2017-07-29&ss=f&srt=sco&sp=rl&se=2018-12-31T04:47:12Z&st=2018-03-01T20:47:12Z&spr=https&sig=VFMzqZUyr%2aTEyu53dHV60Zib0hb1PTqzcqEKAl97aLvA%3D
```

You will use the SAS token in the next step.

### F: Configure Your Bot

Open _this.bot.config.json_, a file within your bot's repository. Let's review and modify the config file segment by segment:

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

 - *displayName* (your bot's name without the AA prefix; e.g. Mariam)
 - *codeName* (name with the AA prefix; e.g. AAMariam)
 - *version* (start with major:0, minor:1, patch:0 – increase minor until you release your bot; once you do, change to major:1, minor: 0)

```
  "devTeam": "AAMasters",
  "profilePicture": "Mariam.png",
  "dataSetVersion": "dataSet.V1",
```

 - *devTeam* (your organization's name including the AA prefix)
 - *profilePicture* (your bot's picture)
 - *dataSetVersion* (different versions of bots may use different versions of datasets)

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

 - *description* (briefly describe your bot's strategy)
 - *startMode* There are three ways in which your bot can be run and only one of them should be set to _true_:
   - _live_ means real live trading,
   - _backtest_ allows testing your strategy against historical data,
   - _competition_ means real trading within a competition

```
      "normalWaitTime": 60000,
      "retryWaitTime": 10000,
      "sleepWaitTime": 3600000,
      "comaWaitTime": 86400000,
```
These parameters affect the frequency with which the bot is run and wait periods in case of certain events. Leave them at the default value for the time being.

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

This is a declaration of Status Dependencies, meaning the status reports the bot consumes. If your bot needs status reports from other bots, this is where you need to configure those dependencies.

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

These are declarations of Data Dependencies, that is, data from other bots that Mariam consumes. If you bot consumes data from other bots, this is where you need to declare those dependencies.

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

Bots output certain products. AACloud keeps track of bots activities in different running modes and makes it publicly available, for transparency purposes.

The config segment above shows the configuration of the first and most important product all trading algobots output: the Live Trading History.

 - *storageAccount* (replace with the one assigned to you)

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

 - *storageAccount* (replace with the one assigned to you)

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
  ],

```

Finally, the last product configured is the Competition Trading History.

 - *storageAccount* (replace with the one assigned to you)

  ```
    "storage": {
    "sas": "?sv=2017-07-29&ss=f&srt=sco&sp=rl&se=2018-12-31T01:49:13Z&st=2018-03-01T17:49:13Z&spr=https&sig=BGdV3DlytkD6vGr%2FxfXcinqF3xSLFxfIz18lfzFzI6g%3D",
    "fileUri": "https://aayourorganization.file.core.windows.net"
  }
}
```

   - *sas* (replace the value with the SAS token we gave you in the [previous step](#sas-token)
   - *fileUri* (replace "_yourorganization_" with the actual name of your Github Organization)

Save the file when you are done.

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
      "botPath": "../Bots/AAMasters/AAMariam-Trading-Bot",	# Enter the path to your bot's project folder
      "process": "Trading-Process"				# up to the last folder only.
    },
    {								# AACloud is prepared to run multiple bots
      "enabled": "false",					# each with it's own processes.
      "botPath": "../Bots/AAMasters/AAOlivia-Indicator-Bot",	#
      "process": "Multi-Period-Market"				# When you clone AACloud
    },								# you may find different bots
    {								# showing up in the configuration file,
      "enabled": "false",					# just like the ones here.
      "botPath": "../Bots/AAMasters/AACharly-Extraction-Bot",	#
      "process": "Poloniex-Hole-Fixing"				# You can choose to set "enabled"
    },								# to "false" or simply delete
    {								# the entries you are not using,
      "enabled": "true",					# in which case you will need to
      "botPath": "../Bots/AAMasters/AABruce-Indicator-Bot",	# delete the comma
      "process": "One-Min-Daily-Candles-Volumes"		# after the first bot.
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

Change the path to the proper one pointing to your bot in your local machine. Bear in mind the path is relative to where the _AACloud.sln_ is located. Do not include the actual _.sln_ file in the path; only the containing folder is expected.

### Stop Gracefully

When you run a trading algobot in your local environment you can configure the AACloud to run it either continuously or only once. This is to avoid the consequences of stopping a trading algobot forcefully, which may cause the bot to loose sync with the exchange (open positions may not be taken into account in subsequent runs).

This is where the _stopGracefully_ parameter comes into play. When the value is _false_ the platform will run the bot continuously. When the value is _true_ the platform runs the bot once and stops it afterwards.

If you ran the bot with _"stopGracefully": "false"_ and need to stop the bot, then simply go back to the config, change the parameter to _true_, save the file and wait. Upon the next run, the bot will be stopped.

### Connection String Folders

In addition, the file Run.js allows you to tell the AACloud whether you wish to run your bot againt testnet or production data (or both).

### Configure Which Process to Run

Now we need to tell the platform which process to run. Click on the AACloud node and make sure the value for the Script arguments field is "_Trading-Process_":

![VS](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Visual-Studio-02-TB.png)

## Step 3: Test Run

### Execute

Once running, the process should call the command prompt and start showing some activity:

![VS](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Command-Prompt-01.png)

## Step 4: What to Expect After Execution

Once you run the AACloud and the platform calls the bot and process you just configured, you will not "see" much more than the command prompt popping up, as described earlier. Do not expect any graphics, browser windows or candlestick charts to pop up. The visualization of bots activity over a candlestick chart happens at a different moment. We will get there later. In the meantime, what you can actually see is the dataset generated by the bot in the form of _.json_ files stored in the cloud, the logs stored locally and the orders that may have been placed in your account at the exchange.

### Check Output

As stated above, you should be able to browse the output of the bot using the Azure Storage Explorer with the connection string we provided for your bot earlier (_File Shares > data_).

### Logs

Upon execution, the platform creates a folder named _Logs_ right outside the platform's repository. Thus, you will find the Logs folder in the same directory as the AACloud folder. Each bot stores logs in its own sub-folders.

### Debugging

By now you should be able to run the bot in your local environment and use typical debugging tools and procedures should anything go wrong.

In case you were not able to successfully run the bot, the logs files are the first place to go.

#### A Quick Logs Overview

Logs are segregated per each execution so that it is easy to locate log files corresponding to different executions. The separation is accomplished by the folder structure itself.

```
.
├── AACloud              
├── Logs > [year] > [month] > [day] > [hour] > [minute ]	# Folder structure showing execution datetime

		└── _Your_Team_ 				# Directory named after your team
	  		 └── Trading 				# Named after type of bot (e.g. Trading, Indicator, etc)
		 	  	└── _YourBot_ver_    		# Named after your Bot and Version
		 	  		└── _Process_    	# Named after the specific process			
			   			└── ...logs 	# See below for details			   
```
**Log name format:** _Date(Yr-Mo-Day-Hr-Min)–RandId–SourceFile.log_
\* _SourceFile_ is the name of the AACloud file to check for associated error or output.

**Selected Log Guide:\***
1.  _~.This.Bot.log:_ Errors and outputs specific to your bot in its repository. All other logs point to CloudPlatform files.
2.  _~.Exchange Api.log:_ Output from exchange API
3.  _~.Assistant.log:_ Trading actions between bot and exchange
4.  _~.Datasource.log:_ Data accessed from storage by your bots
5.  _~File Storage.\_Bot\_.log:_ Data access from storage by listed bot
6. _~.trading algobot Main Loop.log:_ Best log to narrow down general cloud platform issues

\*_By closest relationship to your bot. Read source code for more detailed comments and to view other files associated with the cloud platform_

If you wish to debug the platform and your bot, open the _IntervalExecutor.js_ module and place a breakpoint in the following line:

```
fileProcessingInterval.start(loopControl);
# line 142
```

Now, run the IDE. When execution halts, press F11 to step into the module _User.Bot.js_ that will be loaded from the configured bot process folder. Once there you can set more breakpoints or debug the module step by step.

## Step 5: Start Coding

Once you have managed to run the bot successfully, you are good to go. We've found the following workflow is quite practical:

* The main business logic/solution to edit is in  (_Your-Bot-Repo > Trading-Process > User.Bot.js_). Other types of bots (e.g. indicator or extraction) have different process folder types.

* Your bot will not fully successfully run until there is a balance in your Poloniex account and your bot can make an actual trade. The bot status report will also not be written to your storage account until then. You can use the simulation mode described above (_exchangeSimulationMode_ in the AACloud config) for a temporary workaround until you fund your account.

* Code directly in the bot's solution until the code is fully implemented.

* Close the bot's module and go to the cloud platform solution to debug (as explained above). While debugging, the bot's files will pop up in separate tabs, so that you can edit the code in the process.


**[Next: Launching Your Algobot >>](./3-LaunchingYourAlgobot.md)**

[Terms of Service](../Terms.md)  &bull;  [Disclaimer](../Disclaimer.md)

<hr />

**Table of Contents:** [Basic Definitions](../README.md/#basic-definitions) | [About The Competition](../TheCompetition.md) | [The AAPlatform](../AAPlatform.md) | [About Algobots](../Algobots.md) | [Setting Up Your Development Environment](./developing/0-Setup.md) | [Trading Algobots](./developing/1-TradingAlgobots.md) | [Starting Out Your Own Algobot](./developing/2-YourOwnAlgobot.md) | [Launching Your Algobot](./developing/3-LaunchingYourAlgobot.md) | [Watching Algobots in Action](../Algobots-in-action.md) 
