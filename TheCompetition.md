**[<< Previous: Introduction](./README.md)**



# About The Competition

The Algobots Arena is an organization built around the competition of cryptocurrency trading algobots, or what we call _algobots_. The foundation of the Arena is powered by the AAPlatform –a system developed by Advanced Algos Ltd. that dramatically simplifies the creation and operation of algobots.

At this point, the AAPlatform is still in the alpha-stage. A large portion of functionality is under development. However, hosting early stage competitions will help drive development as well as integrate early feedback and interests from both developers and traders.

In the near future, the AAPlatform is set to implement an ecosystem enabling end-users access to subscriptions for bots that trade on their behalf. Subscription fees will cover the costs of the bot infrastructure and pay Algobot Teams fees. Fees will be paid in ALGO tokens, the AAPlatform's native token.

Participating in early competitions not only offers the chance to win competition prizes, but makes you a part of the Algobots Community and provides increased potential of monetizing your efforts when the platform is released to the general public.

## Competition Rules

### Preliminary Dates (to be confirmed soon)

The first ever competition starts on **Monday June 4th 2018** at 00:00:00.000 GMT and ends on **Sunday June 10th** at 23:59:59.999 GMT.

Subsequent competitions shall be announced and confirmed later on.

### Algobot Team Registration

We are launching the first competition on an invite-only basis. If you haven't been invited and want in, send us an email to feedback at advancedalgos dot org.

### Requirements

#### Poloniex Account

Make sure you have an account with [Poloniex](https://poloniex.com/). If you don't, go ahead and open one ASAP, as there may be a waiting period. You can attempt the verification process, however, you should be able to trade even if you don't verify your account.

#### Join Our Telegram Channel

[Join the Advanced Algos Telegram Channel](https://t.me/advancedalgos) through which we will offer support before and during the competition.

#### Your Own Bots

Your Algobot Team will need your own GitHub Organization and your own algobots. We will go through the whole process further down this document.

### About Algobots

You are allowed to compete with as many trading algobots as you see fit. You can create as many indicator algobots as required to implement your strategy. You will learn more about the different types of bots further down this document.

In order to guarantee transparency, registered algobots are not allowed to connect to the exchange directly; algobots should connect to the exchange only through the AACloud _Assistant_ (more on this further down this document). AACloud tracks algbots activity and makes the information available for everyone to audit.

**Once a bot is released in the competition it cannot be modified.**

> NOTE: The AAPlatform is still in its infancy, on alpha stage. It is likely that errors may occur at runtime. Should any unhandled error occur –either at the bot or platform level– resulting in the bot interrupting its execution, the bot will be considered dead and will not be restarted. This is unfortunate but it is the reality of alpha-testing. Execution Logs will be provided for post-mortem analisys.

#### Algbots License

The AAMaster algobots offered as templates are released under the GNU Affero General Public License (AGPL) to guarantee:

> * the freedom to use the software for any purpose,
> * the freedom to change the software to suit your needs,
> * the freedom to share the software with your friends and neighbors, and
> * the freedom to share the changes you make.
>
> _(Extract from [The Foundations of the GPL](https://www.gnu.org/licenses/quick-guide-gplv3.html))_

It is a policy of Advanced Algos Ltd. to require all bots running on the AAPlatform to be released under the same license. In order to do that. We will guide you through the process further down this document.

### Markets

The competition takes place in the **USDT-BTC market in Poloniex**.

For the time being, the platform serves both historic and live trades data. Trades are performed at Algobot Team's accounts at the exchange, thus having an account with Poloniex is a requirement for participating.

For the time being, we will only be using Poloniex and the USDT-BTC market to do our trading. We will expand the horizon in upcoming competitions.

### Capital

Each Algobot Team trades with their own funds within their own accounts at the exchange. Algobot Teams are fully responsible for the trading they do.

Each algobot is allowed to trade up to 0.001 BTC Initial Capital (roughly equivalent to USD 10). This is in order to minimize risk at this first ever alpha stage competition.

> NOTE: In order to avoid unnecessary risk, we recommend withdrawing excess funds from the exchange or block them by placing an order at a price you know will not be filled.

#### Partial Profits Trading

Algobots are allowed to trade with partial profits. This is the only way in which they can legally trade with more than the Initial Capital specified above. Thus, the limit is 0.001 BTC + Partial Profits. The platform serves available balances that your algobot can check in order to make sure the limit is not exceeded.

> Algobots attempting to trade more than the allowed limit generate an exception that needs to be handled.

#### Fees

Participating in the competition and running your algobots on the AAPlatform is free of charge at this point in time.

For your information, Poloniex charges the following fees for every order filled:

| **Maker** | **Taker** |
|------|------|
| 0.15% | 0.25% |

Poloniex fees are explained [here](https://poloniex.com/fees/).

The competition does take fees into consideration while calculating the ranking and competition results. For that reason, fees are factored in the available balance served by the platform.

### Ranking

The ranking is determined by a very simple performance metric: [Return on Investment (ROI)](https://www.investopedia.com/terms/r/returnoninvestment.asp).

#### Formula

**ROI** = (Gain from Investment - Cost of Investment) / Cost of Investment (expressed as a percentage)

#### Definitions

* **Cost of Investment** = Initial BTC Balance = 0.001 BTC. For the purpose of this competition, this is a constant, meaning that if you use less than 0.001 BTC to do your trading, we will still use 0.001 BTC as the value for this constant.

> NOTE: It doesn't matter how much BTC you actually have in the exchange. The platform keeps track of your trades and available balances during the competition.

* **Gain from Investment** (or Losses, expressed as negative Gains) = Final BTC Balance

#### Winners

The result of the competition is determined by the position of each algobo in the ranking by the end of the competition.

##### _Example_

**Algobot A** ends up with 0.0015 BTC

Bot A ROI = (0.0015 - 0.001) / 0.001 * 100% = 50%

**Algobot B** ends up with 0.0005 BTC

Bot B ROI = (0.00075 - 0.001) / 0.001 * 100% = -25%

**Algobot C** ends up with 0.001 BTC

Bot B ROI = (0.001 - 0.001) / 0.001 * 100% = 0%

_Final Ranking_:

| **Position** | **Algobot** | **ROI** |
|:------|:------:|------:|
| 1st | A | 50 % |
| 2nd | C | 0 % |
| 3rd | B | -25 % |

### Prizes

The competition awards 0.5 BTC and up to 800,000 ALGO (worth USD 8,000 as of this date) as prize money for the top performers during each competition period, with the following caveats:

* BTC Prizes are awarded to bots with ROI >= 10% (10% profits and higher) only.

* ALGO prices are awarded always, even when ROI is negative (loss).

**The prize money is awarded as follows:**

| **Position** | **BTC Prize** | **ALGO Prize** |
|:-----|-----:|-----:|
| 1st | 0.30 | 300,000 |
| 2nd | 0.15 | 150,000 |
| 3rd | 0.05 |  50,000 |
| 4th to 15th |      |  25,000 |

> NOTE: In the [example above](#example), only Bot A would have been awarded the BTC Prize, as it is the only one with a ROI bigger than 10%. ALGO prizes are awarded irrespectively.

**[Next: The AAPlatform >>](./AAPlatform.md)**

[Terms of Service](./Terms.md)  &bull;  [Disclaimer](./Disclaimer.md)

<hr />

**Table of Contents:** [Basic Definitions](./README.md/#basic-definitions) | [About The Competition](./TheCompetition.md) | [The AAPlatform](./AAPlatform.md) | [About Algobots](./Algobots.md) | [Setting Up Your Development Environment](./developing/0-Setup.md) | [Trading Algobots](./developing/1-TradingAlgobots.md) | [Starting Out Your Own Algobot](./developing/2-YourOwnAlgobot.md) | [Launching Your Algobot](./developing/3-LaunchingYourAlgobot.md) | [Watching Algobots in Action](./Algobots-in-action.md) 
