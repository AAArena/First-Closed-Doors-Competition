**[<< Previous: Setting Up Your Development Environment](./0-Setup.md)**



# Trading Algobots

You are almost done with your set up. Let's briefely discuss t-bots before actually cloning one to use as a template.

## Overview

At this early stage, the AAPlatform and the trading algobot templates solve several of the main issues around algorithmic trading:

* Infrastructure to run bots in the cloud;
* Crucial historical and live trades data;
* Connection with exchanges, placement and handling of orders.

This leaves Algobot Teams free to focus in the creative side of things: coming up with and implementing a trading strategy.

There are four AACloud modules particularly significant to trading algobots:

* _Data Dependencies_ & _Status Dependencies_: Your trading algobot's config file contains two declarations of dependencies: data and status dependencies. Dependencies exist because t-bots use other algobot's datasets, or require certain data to be on a certain state. The dependencies modules load declared dependencies and pass them on to the bot through the Assistant module.

* _Context_: In terms of context, trading algobots require the latest status report, the history of what was done on previous runs and the execution context tracking balances, trades, positions and so on. Context is saved in files as outputs of trading algobots. The context module reads the last status report, gets the date of the last execution, fetches the corresponding context file and serves it to the Assistant module.

* _Assistant_: The Assistant module processes information available from other modules and serves a digest version to the trading algobot. The Assistant module also acts as an interface with the exchange, as it offers methods for placing, closing and moving orders.

Let's review how AACloud interacts with trading algobots...

## Trading Bot Process Main Loop.js

As explained elsewhere, Main Loop modules have a common structure that can be summarized in the following actions:

* Set up objects

* Initialize objects exposing public functions

* Execute algobots processes

* Save context

* Schedule next execution

Let's take a closer look at how all this is done in the case of trading algobots...

### Set Up & Initialize Objects

It all starts with _function loop()_ defining the modules that will become available to the rest of the infrastructure and to algobots themselves:

```JavaScript
...
const UTILITIES = require(ROOT_DIR + 'Utilities');
const BLOB_STORAGE = require(ROOT_DIR + 'Blob Storage');
const DEBUG_MODULE = require(ROOT_DIR + 'Debug Log');
const POLONIEX_CLIENT_MODULE = require(ROOT_DIR + 'Poloniex API Client');
const EXCHANGE_API = require(ROOT_DIR + 'ExchangeAPI');
const CONTEXT = require(ROOT_DIR + 'Context');
const ASSISTANT = require(ROOT_DIR + 'Assistant');
const STATUS_REPORT = require(ROOT_DIR + 'Status Report');
const DATA_SET = require(ROOT_DIR + 'Data Set');
const STATUS_DEPENDENCIES = require(ROOT_DIR + 'Status Dependencies');
const DATA_DEPENDENCIES = require(ROOT_DIR + 'Data Dependencies');
...
```

Each of these modules in AACloud work as an object. In each module a _new_ function (e.g. _newContext_ in the Context module) constructs _thisObject_ –the main object of the module– defining properties and functions. These are the public functions which algobots can execute. Once the object is constructed and certain low-level operations are performed, _thisObject_ is returned as a result of the _new_ function.

The way in which the Trading Bot Process Main Loop sets up and initializes the nested objects structure is by calling each module, one after the other, passing on objects while initializing them, which are nested as each of the modules construct their own objects returning them to the Main Loop.
This is how it actually works:

Status Dependencies are initialized first...

```JavaScript
function initializeStatusDependencies() {
   if (FULL_LOG === true) { logger.write("[INFO] run -> loop -> initializeStatusDependencies ->  Entering function."); }
   statusDependencies = STATUS_DEPENDENCIES.newStatusDependencies(bot, DEBUG_MODULE, STATUS_REPORT, BLOB_STORAGE, UTILITIES);
   statusDependencies.initialize(processConfig.statusDependencies, undefined, undefined, onInizialized);
...
```

Then it's the turn of Data Dependencies...

```JavaScript
function initializeDataDependencies() {
   if (FULL_LOG === true) { logger.write("[INFO] run -> loop -> initializeDataDependencies ->  Entering function."); }
   dataDependencies = DATA_DEPENDENCIES.newDataDependencies(bot, DEBUG_MODULE, DATA_SET, BLOB_STORAGE, UTILITIES);
   dataDependencies.initialize(processConfig.dataDependencies, onInizialized);
...
```

Now Context is initialized with a reference to Status Dependencies...

```JavaScript
function initializeContext() {
   if (FULL_LOG === true) { logger.write("[INFO] run -> loop -> initializeContext ->  Entering function."); }
   context = CONTEXT.newContext(bot, DEBUG_MODULE, BLOB_STORAGE, UTILITIES, STATUS_REPORT);
   context.initialize(statusDependencies, onInizialized);
...
```
Exchange API follows...

```JavaScript
function initializeExchangeAPI() {
   if (FULL_LOG === true) { logger.write("[INFO] run -> loop -> initializeExchangeAPI ->  Entering function."); }
   exchangeAPI = EXCHANGE_API.newExchangeAPI(bot, DEBUG_MODULE, POLONIEX_CLIENT_MODULE);
   exchangeAPI.initialize(onInizialized);
...
```

Finally, Assitant is initialized with references to Context, Exchange API and Data Dependencies...

```JavaScript
function initializeAssistant() {
   if (FULL_LOG === true) { logger.write("[INFO] run -> loop -> initializeAssistant ->  Entering function."); }
   assistant = ASSISTANT.newAssistant(bot, DEBUG_MODULE, UTILITIES);
   assistant.initialize(context, exchangeAPI, dataDependencies, onInizialized);
...
```

Thus, the whole object structure ends up in the _Assitant_ object, with the following arrangement:

```
Assitant
	│
	├── Context
	│	  │
	│	  └── Status Dependencies
	│
	├── Exchange API
	│
	└── Data Dependencies
```

### Execute Algobots Processes

Once the object structure is constructed _function initializeUserBot()_ passes the Assistant object to the _UserBot.js_ module in the t-bot and _function startUserBot()_ executes it. **This makes the Assistant object the one and only direct interface of AACloud with t-bots.**

### Save Context & Schedule Next Execution

Once the t-bot finishes its execution, _function saveContext()_ saves the context and _function loopControl(nextWaitTime)_ sets the wait time for the next execution according to configuration values.

## How T-Bots Use the Assistant Object

The overall strategy when working with trading algobots can be summarized in the following bullet points:

* Bots are executed every one minute.

* Each time the bot runs, it first needs to understand the context of the current execution. Bots get the context info from the Assitant object.

* Then the bot embarks in the calculations required by its trading strategy. At this point in time, there are very few indicators offering processed information. As [explained earlier](../Algobots.md#indicator-algobots-aka-i-bots), we encourage you to respect the proposed incumbencies architectecture and put the Technical Analysis logic in **indicator algobots**. Almost all Technical Analysis indicators are calculated from trades and volume data. Their formulas are in the pubic domain and even code is readily available if you search around. You are free to use open source code within your bot's code.

* Once calculations are performed, the bot decides what to do, and uses the Assitant to place orders on the exchange.

<hr />

**[Next: Exchange API >>](./1b-Exchange-API.md)**

[Terms of Service](../Terms.md)  &bull;  [Disclaimer](../Disclaimer.md)

<hr />

**Table of Contents:** [Basic Definitions](../README.md/#basic-definitions) | [About The Competition](../TheCompetition.md) | [The AAPlatform](../AAPlatform.md) | [About Algobots](../Algobots.md) | [Setting Up Your Development Environment](./0-Setup.md) | [Trading Algobots](./1-TradingAlgobots.md) | [Exchange API](./1b-Exchange-API.md) | [Starting Out Your Own Algobot](./2-YourOwnAlgobot.md) | [Launching Your Algobot](./3-LaunchingYourAlgobot.md) | [Watching Algobots in Action](../Algobots-in-action.md) 
