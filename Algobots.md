**[<< Previous: The AAPlatform](./AAPlatform.md)**


# About Algobots

Algobots are open source projects in Github, programed in JavaScript. AACloud calls algobots and puts them to run in specific time intervals. They consume services from the platform and data from other algobots, especially from indicator algobots, and at the same time, produce an output that is stored in the cloud (to be consumed by other algobots).

### Types of Algobots

The AAPlatform handles three different types of bots, differentiating them by their incumbencies:

#### Extractor Algobots (AKA e-bots)

They extract raw trades and order books data from exchanges and store it in a standardized format for other bots to consume.

You will not need to program these kinds of bots for this competition, as we will be using an existing one –[Charly](https://github.com/AAMasters/AACharly-Extraction-Bot)– who gets raw data from Poloniex, the one exchange we will be working with.

#### Indicator Algobots (AKA i-bots)

They process raw trades data and other indicators to output elaborate data structures, mainly technical indicators, for trading algobots to consume.

You will most likely need to program i-bots in order to perform Technical Analysis studies or functions. While it is true that you can process data and do all sorts of calculations from within your trading algobot's code, this is not recommended. Advanced Algos Ltd. encourages developers to respect incumbencies assigned to each type of algobot, for several reasons:

1. The AAPlatform's architecture is designed so that algobots can consume data from other algobots, in order for the network to reuse resources. By respecting the incumbencies of each type of algobot you contribute to growing the platform along with the embedded ecosystem in a sustainable manner.

2. The AAPlatform is set up as a marketplace of extractor, indicator and trading algobots. If you program and release an i-bot, you will soon be able to monetize that effort as algobots consuming the data your i-bot generates will pay you a fee.

3. If instead of creating an indicator algobot, you do the technical analysis from within your trading algobot, anyone can come at a later time, extract from your trading algobot the code that performs the technical analysis, and create their own indicator algobot with it. This means you may permanently lose the chance to monetize the indicator functions and effectively allow someone else to do it instead.

#### Trading Algobots (AKA t-bots)

They automate trading strategies and place orders through the platform, which connects to exchanges via exchanges APIs to trade cryptocurrency.

### How Algobots Work

Algobots mission is –in essence– creating *products* that others can consume. To do this, they run *processes* which produce and store *datasets*.

Eeach algobot may have several processes, and processes don't necessarily have a one-to-one relationship with products. That is, a product can be the result of the work of one or more processes.

Algobot processes are self-contained entities, meaning that they run when called by the AACloud and stop when they finish the task at hand, to wake up again only when AACloud calls the process the next time (in configurable intervals). The datasets processes create are the actual *output* of algobots which are stored in Azure cloud storage containers. But processes also produce and store a second valuable piece of information: *status reports*.

Status reports serve as temporal annotations that algobots read every time they are called by AACloud so as to know what was done in the previous run and what the state of affairs is at the present time. Status reports are dynamic, and they change constantly, with updates after every single run of the associated process.

We established that algobots produce products for others to consume. This "others" include other algobots, meaning that algobots usually depend on the datasets produced by other algobots. We call these *data dependencies*, which are declared on each algobot configuration file.

Algobots consume their own status report and they might as well consume status reports from other algobots. We call these *status dependencies*, which are too declared in each algobot configuration file.

At this point in time, there are five different types of datasets: market files, daily files, minutes files, single file and file sequence. These types of datasets define the structure of the data and how it is stored.

A *market file* contains data spanning the whole existence of the market, that is, from the day the pair (e.g. USDT-BTC) started trading up to the present time. The data is stored in one single file, which is appended every time the process runs generating new data.

A *daily file* contains data segmented by day. That is, the process generates one file per day and stores it in the deepest level of a folder tree structure of the following type:  Year > Month > Day.

A *minutes file* contains data pertaining to one single minute and is stored in the deepest level of a folder tree structure of the following type:  Year > Month > Day > Hour > Minute.

A *file sequence* consists of sequential information that is not necessarily structured on any particular timeframe. The process stores two types of files: the one ending in *.Sequence.json* contains the number of files in the sequence, and the sequence is formed by multiple files ending in a sequential number (e.g. 15.json).

A *single file* is pretty much just that: a dataset that is stored in one file only.

### Real Life Example

Let's put all this in perspective by analyzing the processes, products and dependencies of a few existing algobots.

[Charly]( https://github.com/AAMasters/AACharly-Extraction-Bot) is an extractor algobot. As his [README file]( https://github.com/AAMasters/AACharly-Extraction-Bot/blob/master/README.md) explains, he "gets trades data for all markets –both historic and live– assuring consistency using recursive processes, and store it in a highly fragmented and usable dataset".

Also explained in Charly's README file, Charly offers one product which is defined by the dataset scope and various characteristics. Please, go on and review [Charly's README file]( https://github.com/AAMasters/AACharly-Extraction-Bot/blob/master/README.md)  and become familiarized with the concepts detailed in there.

Charly has three different processes: Poloniex-Live-Trades, Poloniex-Historic-Trades and Poloniex-Hole-Fixing. These three process combined generate the one single dataset that constitutes Charly's single product. The dataset is stored under the *minutes file* structure.

Now, let's see what [Bruce]( https://github.com/AAMasters/AABruce-Indicator-Bot), an indicator algobot, does with Charly's product. As you can learn from [Bruce's README file]( https://github.com/AAMasters/AABruce-Indicator-Bot/blob/master/README.md) he produces two datasets: candles at 1 minute resolution and volumes at 1 minute resolution. The datasets are stored under the _daily file_ type of dataset.

Now scroll down the README file and see what Bruce's dependencies are. That's right. Bruce depends on Charly's product. Bruce's processes take the trades data that Charly extracted from the exchange, performs calculations to build 1 minute candles and stores his own dataset with more elaborate data. In other words, Bruce is adding value to Charly's product and offering a new value-added product of his own.

But the value-adding chain does not stop there. Let's take a look at another i-bot, [Olivia]( https://github.com/AAMasters/AAOlivia-Indicator-Bot). According to her [README file]( https://github.com/AAMasters/AAOlivia-Indicator-Bot/blob/master/README.md) Olivia offers four different products: candles at sub-hour resolutions, candles in resolutions above one hour, volumes in sub-hour resolutions and volumes in resolutions above one hour. And guess what? Indeed, Olivia uses Bruce's one minute candles and one minute volumes to produce complementary candles and volumes at different resolutions.

And so it goes. The last link in the chain usually comes in the form of trading algobots using data from indicator algobots, as that is the ultimate purpose of the whole algobots ecosystem: to provide trading algobots with quality preprocessed data they can use to make the best possible trading decisions.

Let's take a look at [Artudito]( https://github.com/AAMasters/AAArtudito-Trading-Bot), for instance. Artudito –a t-bot– uses candles and volumes from Olivia to make trading decisions. Of course, the main goal of a t-bot like Artudito is to perform profitable trading. However, notice that trading algobots too have outputs, and thus offer products that are consumable by others. Trading bots output three different products: Live Trading History, Backtest Trading History and Competition Trading History. Those datasets are available for others to consume. For instance, the [AAWeb application](https://aawebproduction.azurewebsites.net) uses those datasets to show t-bots activities on a visual environment resembling typical candlestick charts so that anyone can dive in and analyze what algobots are doing.

## About Plotters

Plotters are –too– JavaScript programs created by Algobot Teams. They serve the purpose of creating a visual representation of datasets so that people can easily interpret the data. For instance, [Plotters-Candles-Volumes]( https://github.com/AAMasters/Plotters-Candles-Volumes) creates the visual representation of candlesticks and volume graphs.

Algobots are usually associated to plotters in order for the AAWeb app to be able to plot the corresponding datasets. For instance, trading algobots use [Plotters-Trading]( https://github.com/AAMasters/Plotters-Trading).

<hr />

**[Next: Setting Up Your Development Environment >>](./developing/0-Setup.md)**

[Terms of Service](./Terms.md)  &bull;  [Disclaimer](./Disclaimer.md)

<hr />

**Table of Contents:** [Introduction](./README.md) | [Getting Started](./GettingStarted.md) | [About The Competition](./TheCompetition.md) | [The AAPlatform](./AAPlatform.md) | [About Algobots](./Algobots.md) | [Setting Up Your Development Environment](./developing/0-Setup.md) | [Trading Algobots](./developing/1-TradingAlgobots.md) | [Exchange API](./developing/1b-Exchange-API.md) | [Starting Out Your Own Algobot](./developing/2-YourOwnAlgobot.md) | [Launching Your Algobot](./developing/3-LaunchingYourAlgobot.md) | [Watching Algobots in Action](./Algobots-in-action.md)
