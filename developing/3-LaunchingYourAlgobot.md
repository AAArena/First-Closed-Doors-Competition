**[<< Previous: Starting Out Your Own Algobot](./2-YourOwnAlgobot.md)**



# Launching Your Algobot

Now that your algobot is ready and you are happy with its behavior, it is time to release it under the AGPL license, register your Algobot Team and algobots in the AAPlatform and eventually run it in the cloud. Running in the cloud is not that different from running the algobot locally.

### Release Under AGPL License

If your algobot is based on any of the AAMasters t-bots, chances are you already have a LICENSE file in your repository. If you do and you can see the _AGPL-3.0_ notice on the top right corner of your repository (like in the below image) you are free to [skip]() the next few steps.

![AGPL License](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Bot-License-05.png)

If you don't have the license file or you don't see the _AGPL-3.0_ notice, then follow this quick process:

#### Step 1

Go the algobot's repository in GitHub and click the _Create new file_ button:

![AGPL License](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Bot-License-01.png)

#### Step 2

Enter the word _LICENSE_ (in all CAPS!) in the text field and click the button _Choose a license template_:

![AGPL License](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Bot-License-02.png)

#### Step 3

Scroll the page and cick the _GNU Affero General Public License v3.0_ link:

![AGPL License](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Bot-License-03.png)

#### Step 4

Click the _Review and submit_ button and follow the rest of the usual steps to commit the changes:

![AGPL License](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Bot-License-04.png)

> NOTE: Make sure you don't modify the license text in any way.

#### Step 5

Go back to your repository root and make sure the AGPL icon has been added to the top right corner of the page, next to the _contributors_ counter:

![AGPL License](https://github.com/AdvancedAlgos/Documentation/blob/master/Media/Dev-Teams-Getting-Sarted-Guide/Bot-License-05.png)

### Configure Algobot Team and Algobots in the Web Platform

Fork and clone the [AAPlatform](https://github.com/AdvancedAlgos/AAPlatform) repository and open _ecosystem.json_. You will need to locate the following piece of code:

```
    {
      "codeName": "AASpartans",
      "displayName": "AA Spartans",
      "bots": [
        {
          "repo": "AADumbO-Trading-Bot",
          "configFile": "this.bot.config.json"
        }
      ],
      "plotters": []
    }
```

Copy the piece of code and replicate it immediately below the closing key, **adding a comma in between the two segments**:

```
    {
      "codeName": "AASpartans",
      "displayName": "AA Spartans",
      "bots": [
        {
          "repo": "AADumbO-Trading-Bot",
          "configFile": "this.bot.config.json"
        }
      ],
      "plotters": []
    }, # <– ADD THIS COMMA AND CHANGE YOUR INFO BELOW
    {
      "codeName": "AASpartans",
      "displayName": "AA Spartans",
      "bots": [
        {
          "repo": "AADumbO-Trading-Bot",
          "configFile": "this.bot.config.json"
        }
      ],
      "plotters": []
    }
```

Modify the pasted code to incorporate the details of your own GitHub organization and your own algobots:


```
    {
      "codeName": "AASpartans",
      "displayName": "AA Spartans",
      "bots": [
        {
          "repo": "AADumbO-Trading-Bot",
          "configFile": "this.bot.config.json"
        }
      ],
      "plotters": []
    },
    {
      "codeName": "AAYourOrganization",
      "displayName": "AA Your Organization",
      "bots": [
        {
          "repo": "AAYourBot-Trading-Bot",
          "configFile": "this.bot.config.json"
        }
      ],
      "plotters": []
    }
```

#### Git CLI commands for above:
```
$ git clone https://github.com/_Your_Fork_/AAPlatform
$ cd AAPlatform
# Make changes as explained above (e.g. vi ecosystem.json)
$ git add .
$ git commit -m 'Add MyTeam to AAPlatform'
$ git push origin master
# In your browser, go to https://github.com/_Your_Fork_/AAPlatform/compare. Make sure Base fork is AdvancedAlgos/AAPlatform and head fork is yours. You may have to click on 'compare across forks.'
Click 'Create Pull Request' button.
```
Once you are finished, commit the changes and submit a pull request. Someone in the AdvancedAlgos Organization will analyze your request and pull it into the main branch's code if everything looks right.

Once that is done, you will be able to see your t-bot's activity at http://aawebdevelop.azurewebsites.net/

### Competition Configuration

Once your algobot is finished and tested, you need to register it in the competition's configuration file. Fork and open [_this.competition.config.json_](https://github.com/AAArena/First-Closed-Doors-Competition/blob/master/this.competition.config.json). Locate the following segment:

```
      {
        "devTeam": "AAMasters",
        "bot": "AAMariam",
        "release": "1.0.0"
      }

```

Copy the piece of code and replicate it immediately below the closing key, **adding a comma in between the two segments**:


```
      {
        "devTeam": "AAMasters",
        "bot": "AAMariam",
        "release": "1.0.0"
      },  # <– ADD THIS COMMA AND CHANGE YOUR INFO BELOW
      {
        "devTeam": "AAYourOrganization",
        "bot": "AAYourBot",
        "release": "1.0.0"
      }
```

Modify the pasted code to incorporate the details of your own GitHub organization and your own t-bot. Create a pull request and wait for someone at our end to review it.


<hr />

### Support

[Join the Advanced Algos Telegram Channel](https://t.me/advancedalgos)

### Feedback

We hope your participation is fun and educational and we'd love to make it better. Please submit any issues you experience during the competition in the [issues section](https://github.com/AAArena/First-Closed-Doors-Competition/issues) of this repository. Please also submit **any** suggestions or other feedback you might have to enhance future experiences via email to feedback at advancedalgos dot org.


<hr />

**[Next: Watching Algobots in Action](../Algobots-in-action.md)**

[Terms of Service](../Terms.md)  &bull;  [Disclaimer](../Disclaimer.md)

<hr />

**Table of Contents:** [Introduction](../README.md) | [Getting Started](../GettingStarted.md) | [About The Competition](../TheCompetition.md) | [The AAPlatform](../AAPlatform.md) | [About Algobots](../Algobots.md) | [Setting Up Your Development Environment](./0-Setup.md) | [Trading Algobots](./1-TradingAlgobots.md) | [Exchange API](./1b-Exchange-API.md) | [Starting Out Your Own Algobot](./2-YourOwnAlgobot.md) | [Launching Your Algobot](./3-LaunchingYourAlgobot.md) | [Watching Algobots in Action](../Algobots-in-action.md) 

