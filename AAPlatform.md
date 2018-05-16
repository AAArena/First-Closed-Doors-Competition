**[<< Previous: About The Competition](TheCompetition.md)**

# The AAPlatform

## Leading Principles

We live in a world crammed with bots working behind the scenes whose intellectual property and profits are held close by their companies and developers. Advanced Algos and the surrounding community envision a _World of Tomorrow_ brimming with the greater wealth cultivated by permissionless knowledge and accessible resources. Thus, it is our mission to create a self-sustaining open-source algobot development and access platform –making algobots accessible and easy-to-use for the everyday person.

## Relevant GitHub Organizations

There are three GitHub Organizations you need to be familiar with:

* [AdvancedAlgos](https://github.com/AdvancedAlgos): Features repositories with the AAPlatform code including the bits that run in the cloud (AACloud) and in the web browser, along with a few other platform-related configurations and documentation.

* [AAMasters](https://github.com/AAMasters): Its a showcase GitHub organization similar to the one each Algobot Team needs to create for themselves. It features several examples of bots, each in their corresponding repository.

* [AAArena](https://github.com/AAArena): Its another showcase GitHub organization featuring the AA Application hosting the trading algobot competition you are about to enter.

## AACloud

AACloud is the part of the platform that interacts with algobots and puts them to run in the cloud.

### Run.js

This is where everything starts:

* Run.js makes a number of global definitions (global variables,  constants and parameters),

* loads all relevant configuration files (starting from AACloud's _this.config.json_ where each algobot process to be run is listed),

* and eventually calls the _Main Loop_ module corresponding to the type of algobot it is running.

### Main Loop Modules

The platform's architecture is designed so that algobots are run as self-contained entities, that is, when algobots finish their execution they are unloaded from memory and put to rest until the following scheduled execution starts.

Each type of algobot (extractor, indicator and trading) has a specific workflow, thus each of them are handled from separate Main Loop modules. However, all Main Loop modules share a similar structure:

* They first set up a structure of nested objects to be passed on to algobots;

* objects are initialized, exposing a number of public functions that algobots can consume to perform their business operations;

* the corresponding algobots processes are executed and objects are passed on;

* once algobots finish their run, the Main Loop stores the _Context_;

* and finally, sets the time for the next execution.

<hr />

**[Next: About Algobots](./Algobots.md)**

[Terms of Service](./Terms.md)  &bull;  [Disclaimer](./Disclaimer.md)

<hr />

**Table of Contents:** [Introduction](./README.md) | [Getting Started](./GettingStarted.md) | [About The Competition](./TheCompetition.md) | [The AAPlatform](./AAPlatform.md) | [About Algobots](./Algobots.md) | [Setting Up Your Development Environment](./developing/0-Setup.md) | [Trading Algobots](./developing/1-TradingAlgobots.md) | [Exchange API](./developing/1b-Exchange-API.md) | [Starting Out Your Own Algobot](./developing/2-YourOwnAlgobot.md) | [Launching Your Algobot](./developing/3-LaunchingYourAlgobot.md) | [Watching Algobots in Action](./Algobots-in-action.md)
