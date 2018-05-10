**[<< Previous: About The Competition](TheCompetition.md)**

# The AAPlatform

## Overview

Historically, trading algorithms have been used in traditional markets and are used in crypto markets as well. Successful bots are most likely kept in the dark by their creators, usually large financial corporations, in order to protect their intellectual property and keep profits for themselves.

In contrast, algobots are open source and so are other applications running on the AAPlatform. Advanced Algos incentivizes bot's evolution via non-stop competitions between algobots and Algobot Teams, fostering collaboration and permissionless innovation.

Algobot Teams can take existing bots and improve them, either by collaborating with the maintainer team submitting pull requests, or by starting up a whole new project forking the bot's code. These principles allow bots to evolve much faster than any private corporate enterprise could dream of.

Trading algobots perform trades and are judged by their performance in competitions. Trading is done with real crypto assets and orders are placed in real crypto exchanges, through the AAPlatform. Algobot Teams constantly tweak their algobots to improve performance, speeding up evolution. Users and the general public will eventually have an active role too: they will support Algobot Teams and their algobots by subscribing and paying a fee to have trading algobots work on their behalf, effectively taking part in the competitions, just like fans in the arena.

The project attracts a community related to the crypto, IT and gaming industries through algobots competitions, incentivizing them via competition prizes, and tying them up in a comprehensive business model in which all stakeholders profit. The market itself becomes a part of the economic circuit as platform tokens circulate among actors, each of them cashing out or procuring tokens as needed. A limited supply of tokens to be sold at successive token sale events sets free market forces in motion, guaranteeing that only the best performing bots will get support and thrive while the rest die.

The business model will eventually allow end users (not participating in the development of algobots) to subscribe to the services of trading algobots, effectively hiring them to work on their behalf. This feature extends the business beyond the Algobots Community, enabling the massification of the service of the platform and the algobots running on it. At the same time, the business model incentivizes the Algobots Community to keep improving bots competing both for clients and for competition prizes at the same time.

## Relevant GitHub Organizations

There are three GitHub Organizations you need to be familiar with:

* [Advanced Algos](https://github.com/AdvancedAlgos): Features repositories with the AAPlatform code including the bits that run in the cloud (AACloud) and in the web browser, along with a few other platform-related configurations and documentation.

* [AAMasters](https://github.com/AAMasters): Its a showcase GitHub organization similar to the one each Algobot Team needs to create for themselves. It features several examples of bots, each in their corresponding repository.

* [AAArena](https://github.com/AAArena): Its another showcase GitHub organization featuring the AA Application hosting the trading algobot competition you are about to enter.

## AACloud

AACloud is the part of the platform that interacts with algobots and puts them to run in the cloud.

### Run.js

This is where everything starts:

* Run.js makes a number of global definitions (global variables,  constants and parameters),

* loads all relevant configuration files (starting from AACloud's _ this.config.json_ where each algobot process to be run is listed),

* and eventually calls the _Main Loop_ module corresponding to the type of bot it is running.

### Main Loop Modules

The platoform's architecture is designed so that algobots are run as self-contained entities, that is, when algobots finish their execution they are unloaded from memory and put to rest until the following scheduled execution.

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

**Table of Contents:** [Basic Definitions](./README.md/#basic-definitions) | [About The Competition](./TheCompetition.md) | [The AAPlatform](./AAPlatform.md) | [About Algobots](./Algobots.md) | [Setting Up Your Development Environment](./developing/0-Setup.md) | [Trading Algobots](./developing/1-TradingAlgobots.md) | [Starting Out Your Own Algobot](./developing/2-YourOwnAlgobot.md) | [Launching Your Algobot](./developing/3-LaunchingYourAlgobot.md) | [Watching Algobots in Action](./Algobots-in-action.md) 
