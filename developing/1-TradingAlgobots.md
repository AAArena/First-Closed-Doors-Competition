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

* _Assistant_: The Assistant module processes information available from other modules and serves a digest version to the trading algobot. It also serves the datasource with trades, candles, etc. The Assistant module also acts as an interface with the exchange, as it offers methods for placing, closing and moving orders.

In its current version, AACloud provides an object (_platform_) containing other objects:

* _datasource_: preloads ready-to-consume data comprised of candlesticks and stair patterns;
* _assistant_: opens, closes and moves positions

The overall strategy when working with trading algobots can be summarized in the following bullet points:

* Bots are executed every one minute.

* Each time the bot runs, it first needs to understand the context of the current execution. Bots get the context info from the Assitant module.

* Then the bot embarks in the calculations required by its trading strategy. At this point in time, there are very few indicators offering processed information. As [explained earlier](#indicator-algobots-aka-i-bots), we encourage you to respect the proposed incumbencies architectecture and put the Technical Analysis logic in **indicator algobots**. Almost all Technical Analysis indicators are calculated from trades and volume data. Their formulas are in the pubic domain and even code is readily available if you search around. You are free to use open source code within your bot's code.

* Once calculations are performed, the bot decides what to do, and uses the platform to place orders on the exchange.

## Exchanges API

The AAPlatform places orders on exchanges through the use of the exchanges' APIs. You will need to create an API Key and configure your bot to use it.

### Creating the API Key

This is how you create an API Key in Poloniex:

Go to the tools menu and select _API KEYS_...

![Poloniex](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Poloniex-API-01.png)

If you have never used the API before, chances are it is disabled at the exchange. So before actually creating an API Key you will need to enable them...

![Poloniex](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Poloniex-API-02.png)

You will need to follow the validation process involving checking your email and confirming your choice. Once that is taken care of, go back to the tools menu and click _API KEY_ again. You should now see a screen offering to create a new key...

![Poloniex](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Poloniex-API-03.png)

Once you create your key, the system will present it as follows...

![Poloniex](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Poloniex-API-04.png)

**Make sure you DO NOT enable withdrawals nor IP access restrictions**.

### Creating an API Key File

Next, you will use the information in the API Key to a create a _.json_ file with the following structure using your own Key and Secret information:

```
{ "Key" : "6HS4YUEB-865UY9W4-KGHEHHJ-GH72ETG1", "Secret" : "1a3529851a05439asdasdw63426378ggd65701ac4a5d53c4859aa3511a8aa65acbd7e713bba755d0b1591ebe3a7618a71393ef4d3d11310628e1db"}
```

Create a folder named _API-Keys_ at the same level of the platform's repository (out of the folder AACloud) and save the file using the following naming convention:

"**AA**" + **BotName** + "**.**" + **ExchangeName** + "**.json**"

e.g.: AAMariam.Poloniex.json

**NOTE: Make sure the folder and file doesn't accidentally end up in GitHub! Your API KEYs should be kept secret!**


**[Next: Starting Out Your Own Algobot >>](./2-YourOwnAlgobot.md)**

[Terms of Service](../Terms.md)  &bull;  [Disclaimer](../Disclaimer.md)

<hr />

**Table of Contents:** [Basic Definitions](../README.md/#basic-definitions) | [About The Competition](../TheCompetition.md) | [The AAPlatform](../AAPlatform.md) | [About Algobots](../Algobots.md) | [Setting Up Your Development Environment](./0-Setup.md) | [Trading Algobots](./1-TradingAlgobots.md) | [Starting Out Your Own Algobot](./2-YourOwnAlgobot.md) | [Launching Your Algobot](./3-LaunchingYourAlgobot.md)
