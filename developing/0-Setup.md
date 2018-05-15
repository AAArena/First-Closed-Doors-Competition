**[<< Previous: About Algobots](../Algobots.md)**


# Setting up your Development Environment

To setup and develop your own algobot, you'll need to pull in several code repositories as well as make a few directories to store configurations. This is a sample view of the final directory structure with important files/folder annotated. Instructions for creating all of this will follow and your directory and file names will differ.

```
.                               # Top level directory located at your choice
├── AACloud                     # Will be cloned from git repository
│   ├── ...                     # A variety of files and folders
│   ├── AACloud.sln             # Used only with VS IDE to launch project
│   └── this.config.json    	# You will configure your algobots to test and develop
│ 
├── API-Keys                    # You will create this dir at same level as AACloud
│   └── AABot.Poloniex.json     # Your Poloniex API Key (more on this further down this doc)
│ 
├── Connection-Strings          # You will create this dir at same level as AACloud
│   └── Development              
│       ├─ .connstring          # Storage connection files to be supplied by Advanced Algos Ltd.
│       └─ ...  
│ 
├── Logs                        # AACloud will output logs here –the folder is created 
│                               # once you run AACloud for the first time
│ 
├── AAPlatform                  # Will be cloned from git repository
│   └── ecosystem.json          # You will be adding your team and algobots to the cloud
│
└── AAYourTeam                  # Directory named after your Algobot Team
    └── AAAlgobot-Trading-Bot   # Your custom algobot repository     
        ├─ Trading-Process
        │    └── User.Bot.js    # You will customize your bot logic here
        └─ this.bot.config.json # Your algobot configuration

```

## Step 1: Setting Up Your Algobot Team Github Organization

Let's start by [setting up a GitHub organization](https://github.com/account/organizations/new) named after your own Algobot Team. Make sure the name of the organization starts with "AA", just like in the above example _AAMasters_. Also make sure that the word "_algobot_" is part of the organization's description.

## Step 2: Node.js

Before we start, make sure you have Node.js installed. If you don't, please [download and install Node.js](https://nodejs.org/en/download/).

![Node.js](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Node-js-01.png)

## Step 3: Azure Storage Explorer

Bots consume and store data in the Microsoft Azure cloud. This tool will allow you to browse and manage data.

### Download, Install, Run

Download and install the [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/).

The following screen should pop up when you launch Azure Storage Explorer:

![Azure Storage Explorer](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Azure-Storage-Explorer-02.png)

Select _Use a connection string or a shared access signature URI_ and click **Next**.

Select _Use a connection string_ and paste the following connection string in the corresponding field to connect to the testnet storage:

```
DefaultEndpointsProtocol=https;AccountName=aatestnet;AccountKey=rQRuD8KeD0upqcN9532zqZTknKwkYJDpGzkATGptk9lIEovkLchdOGOJVld26cUjpzTA4enxsxpCB33B0pOZRg==;EndpointSuffix=core.windows.net
```

![Azure Storage Explorer](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Azure-Storage-Explorer-03.png)

Click **Next** and **Connect** in the following screen.

> **NOTE**: Please bear in mind that this connection string allows you to browse data in the testnet environment. When you produce your own bot it will store data in the production storage for which you will get your own connection string (more on this further down this document).

Storage Explorer will load on the following screen:

![Azure Storage Explorer](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Azure-Storage-Explorer-01.png)

## Step 4: Clone the AACloud

Clone the [AACloud](https://github.com/AdvancedAlgos/AACloud) repository in your local machine.

#### Using Git CLI
```
$ git clone https://github.com/AdvancedAlgos/AACloud
```

#### or Using GitHub Desktop

If you are an advanced GitHub user you are probably using Git via the command-line. If you are not, we recommend [downloading and installing the GitHub Desktop](https://desktop.github.com/) application.

If you are not familiar with GitHub at all, we highly recommend you invest the time in learning it, as it is the most popular collaboration and version control system. For further information on how to use GitHub Desktop, please refer to the [Getting Started with GitHub Desktop guide](https://help.github.com/desktop/guides/getting-started-with-github-desktop/) or [watch this video tutorial](https://www.youtube.com/watch?v=GqNAD4XoZ6k).

Once you have launched GitHub Desktop and logged in with your GitHub credentials, this is what you need to do to clone the platform's repository:

Go to _File > Clone Repository_

![GitHub Desktop](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/GitHub-Desktop-01.png)

Click on the URL tab and paste the repository URL in corresponding field:

```
https://github.com/AdvancedAlgos/AACloud
```

Choose where in your local machine GitHub should copy the files.

![GitHub Desktop](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/GitHub-Desktop-02.png)

Once you clone the repository, GitHub desktop keeps track of the changes that may occur in the files in your local machine and helps synchronize the changes with the online repository via commits and pushes.

## Step 5: NPM

We use NMP to handle dependencies, thus you will need to install NMP to finish the setup of your environment. This is how to do it:

Open a Command Prompt instance, go to your AACloud directory and run the following command: ```install npm``` 

![NPM](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/NPM-install.png)

<hr />

**[Next: Trading Algobots >>](./1-TradingAlgobots.md)**

[Terms of Service](../Terms.md)  &bull;  [Disclaimer](../Disclaimer.md)

<hr />

**Table of Contents:** [Basic Definitions](../README.md/#basic-definitions) | [About The Competition](../TheCompetition.md) | [The AAPlatform](../AAPlatform.md) | [About Algobots](../Algobots.md) | [Setting Up Your Development Environment](./0-Setup.md) | [Trading Algobots](./1-TradingAlgobots.md) | [Exchange API](./1b-Exchange-API.md) | [Starting Out Your Own Algobot](./2-YourOwnAlgobot.md) | [Launching Your Algobot](./3-LaunchingYourAlgobot.md) | [Watching Algobots in Action](../Algobots-in-action.md) 
