![Article Banner GIF](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/article-banner-gif.gif?raw=true)
# Table of contents
  * [The Fresh Mints Bot 🍃](#the-fresh-mints-bot)
  * [Overview](#overview)
  * [Technical overview](#technical-overview)
  * [Features ✨](#features)
  * [Screenshots 📸](#screenshots)
  * [Server setup](#server-setup)
    + [Fresh Mints Activation Guide 🔐](#fresh-mints-activation-guide)
      - [Step 1](#step-1)
      - [Step 2](#step-2)
      - [Step 3](#step-3)
      - [Step 4](#step-4)
      - [Deactivating an activated server](#deactivating-an-activated-server)
    + [Fresh Mints Setup Guide 🧰](#fresh-mints-setup-guide)
      - [Step 1](#step-1-1)
      - [Step 2](#step-2-1)
      - [Step 3](#step-3-1)
      - [Step 4](#step-4-1)
      - [Step 5](#step-5)
      - [Info](#info)
      - [Additional Features](#additional-features)
  * [Technical implementation 🧑‍💻](#technical-implementation)
    + [How does a Discord bot work?](#how-does-a-discord-bot-work-)
    + [Bot commands](#bot-commands)
    + [Bot events](#bot-events)
    + [Embeds](#embeds)
    + [Server config](#server-config)
    + [Ethereum APIs](#ethereum-apis)
    + [Caching](#caching)
    + [Identifying NFT transactions](#identifying-nft-transactions)
    + [Cron jobs](#cron-jobs)
    + [Monitoring](#monitoring)
  * [Monetization 💸](#monetization)
  * [Template](#template)
  * [Conclusion](#conclusion)

# The Fresh Mints Bot
In a previous post I talked about my journey with monetizing a software application by using NFTs. In this post I want to talk about that application. 

In that digital gold-rush of 2021/2022 that lasted for what seemed like a few moments, I was looking for ways to leverage my software skills to gain an advantage on this emerging NFT market. One of the ways I thought of was by creating some sort of script that constantly monitored the Ethereum wallets of known NFT traders / flippers (e.g. GarryVee) and quickly trying to buy the same NFTs they bought in the hopes of turning it into profit.

This script idea turned into a Discord bot since that was the main medium of communication for NFT enthusiasts. To quote my previous self, this is how I described the bot:

> Fresh Mints is a Discord bot that allows you to track Ethereum wallet and contract addresses and sends alerts to your server when there is a new NFT mint or a purchase on OpenSea. Keep your server informed of whenever whales or influencers are making moves so that your community can jump on the trends before everyone else.

## Overview

The way Fresh Mints worked was: a user would add the bot to their server, configure a number of addresses they wanted to track and they would receive alerts on a channel in the server whenever these addresses minted or purchased an NFT.

## Technical overview

From a technical point of view, the bot created a cron job for each server that it joined that was calling an API at regular intervals to get information about the latest transactions of the addresses the server was tracking.

If one of these transaction was an NFT mint or purchase, the bot would send an alert to the configured channel.

## Features
* **Track Ethereum wallet addresses** - Track any Ethereum wallet address for new NFT mints
* **Track Ethereum contact addresses** - Track any Ethereum contract address for new NFT mints
* **Track OpenSea Purchases** - Track any purchase on OpenSea that the wallet addresses make
* **Customize tracking schedule** - Set the frequency of the bot checking the tracked addresses
* **Customize alert channel** - Set a channel where the alert messages will be sent
* **Tags on alerts** - Set a role to be tagged whenever the bot sends a new alert


## Screenshots

<img src="https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/server-config.jpg?raw=true" alt="Server Config" width="300"/>

*Example server configuration*

<img src="https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/help.jpg?raw=true" alt="Command List" width="300"/>

*All the possible bot commands*

<img src="https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/alerts.jpg?raw=true" alt="Alert Examples" width="300"/>

*Examples of alert messages*

<img src="https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/following-addr.jpg?raw=true" alt="Tracked Addresses" width="300"/>

*Example of a list of tracked addresses*

## Server setup
An invite link to the Fresh Mints Discord channel can be found [here](http://discord.gg/7EPagRsSCH).

### Fresh Mints Activation Guide
#### Step 1
Get the **Fresh Mints NFT** from [OpenSea](https://opensea.io/collection/fresh-mints-bot).

![Fresh Mints NFT](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/nft.gif?raw=true)

*Fresh Mints NFT*

#### Step 2
Verify ownership using the CollabLand bot in the `#verify-ownership` channel.

![Collab.Land Verification Prompt](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/collab-land-verify.png?raw=true)

*Collab.Land Verification Prompt*
#### Step 3
Once you have the `Fresh Family` role, go to the `#redeem-key` channel and use the `/activation-key` command to get your key.
#### Step 4
You now have an activation key which you can use to activate the bot on your server 🎉.

To find out how check the [setup guide below](#fresh-mints-setup-guide).

ℹ️ You can only get a single key at the moment.

ℹ️ If at any point you don't remember your key just repeat [Step 3](#step-3).

#### Deactivating an activated server
If you want to use your activation key on another server you first need to deactivate the currently activated server.

To do that you can just use the `/deactivate` command.

After that you can use the `/activate <activation-key> ` command again with your key on the new server you want to activate.

ℹ️ If you forgot your key you can just repeat [Step 3](#step-3) from above.

### Fresh Mints Setup Guide
Follow this guide to set up the Fresh Mints bot on your server.
#### Step 1
Add the Fresh Mints bot to your server using [this link](https://discord.com/api/oauth2/authorize?client_id=912778050435948614&permissions=277025614912&scope=bot%20applications.commands).

<img src="https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/add-bot-to-server.png?raw=true" alt="Add Bot to Server" width="300"/>

*Adding the bot to the server*

ℹ️ To use the bot commands you currently need to have Administrator permissions in that server

#### Step 2

Use the `/activate` command with the activation key you got from the ⁠[activation guide](#fresh-mints-activation-guide).

![Bot Activation Command](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/activation-step.png?raw=true)

*Bot Activation Command*

**Success** 🎉 If everything went well your server should now be activated!

#### Step 3
To start using the bot you need to set up a channel where the alerts will be sent to using the `/alert-channel` command.

![Alert Channel Setup Command](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/alert-channel-setup.png?raw=true)

*Alert Channel Setup Command*

ℹ️ Optionally, you can set up a channel for info logs from the bot using the `/info-channel` command. This is recommended and would help if you ever have any problems with it.

#### Step 4
Now you need to follow some ETH addresses. You can add some using the `/add` command or `/add-contract` for contract addresses.

For starters, you can use the `/load-default-wallets` command to load a list of wallets of NFT influencers.

![Adding Wallet Command](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/adding-wallet-cmd.png?raw=true)

*Adding Wallet Command*

ℹ️ Use the /who command to confirm the list of addresses you’re now following.

#### Step 5
You’re now ready to go ✅

Just use the `/toggle` command to turn on the alerts on the server.

#### Info
You can use the `/info` command to confirm the server settings.

<img src="https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/server-info-cmd.png?raw=true" alt="Server Info Command" width="300"/>

*Server Info Command*

To see a list of all available commands use the `/help` command.

#### Additional Features
A list of other features of the bot.

**Tags on alerts** - If you want a role to be tagged whenever the bot sends a new alert, use the `/set-alert-role` command. To clear it use the `/clear-alert-role`.

**Tracking OpenSea Purchases** - If you want the bot to also track any purchase on OpenSea that the addresses make use the `/track-opensea-buys` command.

## Technical implementation

Before jumping into the details it's worth mentioning that this code was implemented over a year ago so some details might not still apply (specifically related to the Discord bot API).

The bot is implemented in Node with Typescript and it ran mostly in Docker on one of my Raspberry Pis (3B and 4) or on server on Google Cloud.

The code is now [publicly available on Github](https://github.com/pawKer/fresh-mints). 

### How does a Discord bot work?
A Discord bot is nothing but a constantly running application process that is sitting waiting to receive events from the servers the bot is in. The main logic within this application is reacting to these events.

The permissions the bot has in that server determines what actions the bot can do (e.g. send messages, delete messages, kick users, etc.).

To create this process you simply have to create a `Discord Client` and login to the API using the API Key

```
const client: DiscordClient = new Client({
  intents: [Intents.FLAGS.GUILDS, Intents.FLAGS.GUILD_MESSAGES], // These are the permissions that the bot needs on the servers it joins
}) as DiscordClient;

client.login(process.env.DISCORD_API_SECRET);
```

A useful tip is that to configure global variables for your bot you can just add them to this client object as this will be available throughout your operations.

```
client.db = new ServerSettingsRepository();
client.activationKeysDb = new ActivationKeysRepository();
client.apiClient = apiClient;
client.useEtherscan = false;
client.MAINTAINANCE_MODE = false;
```

### Bot commands
If I remember correctly, when I first started implementing the bot, there was simply a method that would be called on every message sent to the server. You would then need to parse that message text to see if it started with a `/` and if it contained a supported command.

Not long after, Discord released the concept of *Slash Commands* which meant you could register a number of accepted commands for your bot that would also show up nicely in the UI.

![Discord Slash Commands](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/slash-commands.png?raw=true)

*Discord Slash Commands*

This made it a lot nicer to code and to make it even better I defined a `Command` type for each of my commands that each had the Discord `SlashCommandBuilder` definition (needed to register the command) and an `execute` method that would be the custom logic that runs.

```
const helpCommand: Command = {
  data: new SlashCommandBuilder()
    .setName("help")
    .setDescription("Get a list of all the bot's commands."),
  async execute(client, interaction) {
    await interaction.reply({ embeds: [getHelpEmbed()] });
  },
};
```
*The /help command*

I'm not sure if this process has improved in the meantime but, at that time, to load all of the defined commands from their respective files I had to add a bit of pretty complex logic. However, this meant I could define each command in its own file and separate them in folder for each category.

```
/commands
    |-> 
        /activation
            |-> 
                activate.ts
                dectivate.ts
        /admin
            |-> 
                maintainance-mode.ts
        /info
            |-> 
                help.ts
                info.ts
                who.ts
...
```

```
const readCommands = async (): Promise<Command[]> => {
  const commands: Command[] = [];
  let res: string[];
  if (process.env.NODE_ENV === "prod") {
    res = glob.sync(`**/*.js`, {
      cwd: `${process.cwd()}/commands/`,
    });
  } else {
    res = res = glob.sync(`**/*.ts`, {
      cwd: `${process.cwd()}/src/commands/`,
    });
  }

  for (const file of res) {
    const fileNoExt = file.substring(0, file.length - 3);

    const command: Command = (await import(`../commands/${fileNoExt}`))
      .default as Command;
    commands.push(command);
  }
  return commands;
};
```

*Reading commands from files*

After reading them in, you could quite easily send them to the Discord API to be registered. This only needs to be done when you add new commands or update the description or parameters of existing commands. 

I wrote the following script to do it:

```
readCommands().then(async (commands) => {
  const deployCmds: string[] = commands.map((cmd) => cmd.data.toJSON());
  await updateCommands(deployCmds);
});
```

```
const rest = new REST({ version: "9" }).setToken(
  process.env.DISCORD_API_SECRET
);
const updateCommands = async (commands: string[]): Promise<void> => {
  try {
    await rest.put(
      Routes.applicationGuildCommands(
        BOT_ID,
        GUILD_ID
      ),
      {
        body: commands,
      }
    );
  } catch (error) {
    console.error(error);
  }
};
```
*Registering commands to the Discord API*

Locally, you need to import all of the commands in a similar way and set them on the client in a map for easy access.
```
client.commands = new Collection<string, Command>();
readCommands().then((commands) => {
  commands.forEach((cmd) => {
    if (client && client.commands) client.commands.set(cmd.data.name, cmd);
  });
});
```
*Note: This doesn't actually register the command code with the corresponding bot command, we'll do that later. Here we're just loading them in memory.*

But how does the correct command get executed? 

### Bot events
The way the bot is notified about the messages in a server is through events. Messages are just one type of event called an `Interaction Create Event` but you can have others such as `Guild Create Event` (the bot joins a new server) or `Ready Event` (the bot setup is complete).

```
const readyEvent = {
  name: "ready",
  once: true,
  async execute(client: DiscordClient) {
    console.log(`Online as ${client?.user?.tag}`);
  },
};
```

Similar to commands, you can have events trigger a function when that event is received by the bot. You can have them in their own file just like above, read them in and register them in a similar way. This time it doesn't actually have to be with the Discord API, just on the local bot client.

```
client.events = new Collection<string, DiscordEvent>();
readEvents().then((events) => {
  events.forEach((ev) => {
    console.log(ev);
    if (ev.once) {
      client.once(ev.name, (...args: unknown[]) => ev.execute(...args));
    } else {
      client.on(ev.name, (...args: unknown[]) => ev.execute(...args));
    }
  });
});
```

The most interesting event is definitely the `Interaction Create Event`. The input to this event function is an `Interaction` object which has all the details such as the command name, the server on which the interaction was created, the user who created it, etc. Based on this interaction, we can decide if the user has the right permissions and we can call the correct command function.

```
const interactionCreateEvent = {
  name: "interactionCreate",
  async execute(interaction: Interaction) {

    // If the message is not a slash command ignore it
    if (!interaction.isCommand()) return; 

    const client = interaction.client as DiscordClient;
    const member = interaction.member as GuildMember;

    // Get the corresponding command function from the map on the client
    const command = client.commands.get(interaction.commandName); 

    if (!command) return;

    const guild: Guild | null = interaction.guild;

    if (!guild) return;

    // Check if the user is an ADMIN - I wanted my bot to 
    // only be configurable by server admins
    if (!member.permissions.has("ADMINISTRATOR")) {
      await interaction.reply({
        content: "You do not have permission to run this command.",
        ephemeral: true,
      });
      return;
    }

    try {
      // Execute the command handler code
      await command.execute(client, interaction);
    } catch (error) {
      console.error(`[${guild.id}]`, error);
      await interaction.reply({
        content: "There was an error while executing this command!",
        ephemeral: true,
      });
    }
  },
};
```

That is how the command files from above are linked to the actual Discord messages. To summarize, when a user sends a message in a server that the bot is in, that creates an `Interaction Create Event` which contains all the relevant information and that our bot is listening for. When the bot receives the event, based on the interaction information it can decide what command code to execute (or any other custom logic).

## Embeds
It's quickly worth mentioning what message embeds are. They're just a way of sending Discord messages with a customizable format.

<img src="https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/embed-example.png?raw=true" alt="Embed message example" width="300"/>

*Embed message example*

In code they look like this:
```
const infoEmbed = new MessageEmbed()
    .setColor("#7bbb57")
    .setTitle("Config info")
    .setDescription(`These are the current bot settings:`)
    .addFields(
      {
        name: "Scheduled messages status",
        value: messagesStatus ? "ON 🟢" : "OFF 🔴",
      },
      {
        name: "Alert channel",
        value: `<#${alertChannelId}>`,
      },
      {
        name: "Info channel",
        value: infoChannelId ? `<#${infoChannelId}>` : "Not set.",
      },
      {
        name: "Schedule",
        value: `The bot will check the addresses: \`${schedule}\`.`,
      },
     ...
    )
    .setTimestamp();
```

They can be sent to the server, for example, as a reply to an interaction:
```
await interaction.reply({embeds: [infoEmbed]});
```

## Server config
It quickly became apparent that I will need a way to persist the different settings for each server that the bot joins. To do this, I used Mongo DB. I won't go into too much detail about how it works but to make things easier I used the `mongoose` library.

Esentially, I stored an object for each server that contained any server specific information and used the server (guild) id as a primary key.

I tried to follow good coding practices by creating a DB repository interface and implementing that in case I needed to swap MongoDB out for some other DB in the future.

```
export interface IServerSettingsRepository {
  find(serverId: string): Promise<MongoResult | null>;
  findAllStartedJobs(): Promise<MongoResult[]>;
  save(serverId: string, data: ServerDataDTO): Promise<void>;
}
```
*Note: the return type should have been DB agonstic but I thought I'd cross that bridge when I got to it (#YAGNI)*

## Ethereum APIs

The data that my application needed was: given an ETH addresses, what are the latest X transactions that that address made? This was something I initially thought was quite common but it turns out someone needs to index and enrich all the blockchain information before it becomes available in that format. After some research, the options that met the criteria of having a good quota of free calls were: the [Etherscan API](https://docs.etherscan.io/) and the [Covalent API](https://www.covalenthq.com/docs/api/transactions/).

The best option really would have been to run my own ETH node and get the data directly from the blockchain myself but that didn't seem reasonable for a project in this stage. If it would've gained traction that would've probably been the direction to go in.

After using the Etherscan API for a while, it was apparent that it didn't provide enough data to be able to distinguish all the different types of transactions and filter out the ones that were not relevant. This was a deal breaker as it meant the bot would send out a lot of false positives.

So, the [Covalent API](https://www.covalenthq.com/docs/api/transactions/get-recent-transactions-for-address-v3/) became the main source of data. With limits of 5 requests per second and 100K daily it was important to make good use of this.

## Caching
The way the bot worked is it polled the API every minute (at its fastest setting) for each tracked address for each server. So if the bot was active in 4 servers and each server tracked 20 addresses that would already be over 100K requests per day.

To combat this we needed a better strategy.

Given that the idea of the bot was you would track NFT influencers it was very likely that most people would track the same few addresses. That means that if server A already checked the address XYZ in the last minute, there's no point in server B making the request again since it should already be cached. What's more, the Covalent API provided a `nextUpdate` field in the response because it also only updated its data at regular intervals so this really made sense.

The cache was just a map stored on the Discord client object like we did above.

```
const requestCache: Collection<string, RequestCacheItem> = new Collection();
client.requestCache = requestCache;
```

To make sure that each server only got notified about an a Covalent API request once, each tracked address had a `lastIdRead` property, the id being a unique identifier of an API request.

The caching logic then was:
* If there's already a response in the cache for this ETH address *and* we are still before the `nextUpdate`
    * if the `lastIdRead` of this address is the same as the id of the cached response
        * **Do nothing** - this has already been processed once
    * else we don't need to send an api request and we can **use the cached response**
* Else, we need to **make the API request**

In code that looks roughly like this:
```
const cacheItem = client.requestCache.get(address);
if (cacheItem && cacheItem.nextUpdate && Date.now() < cacheItem.nextUpdate) {
    if (data.lastIdRead && data.lastIdRead === cacheItem.id) {
      return;
    }
    // Use data from the cache
    data.lastIdRead = cacheItem.id;
  } else {
    // Make new API request
    const res: EthApiResponse = await client.apiClient.getApiResponseAsMap(...);
    client.requestCache.set(address, res);
    data.lastIdRead = res.id;
  }
```

I had also implemented a similar mechanism for database requests to also reduce the number of DB calls.

## Identifying NFT transactions
This was perhaps one of the more challenging parts of this project. Not technically, but with my limited knowledge of the blockchain and the big variety of transaction types it was hard to identify what were the transactions that I needed to send alerts for.

The Covalent API response was huge (>150K rows for 25 transactions) and contained a lot if information. You could only request the transactions of an address at a time and you got back a list of transactions. Each transaction had a series of log events and this was where the main data was.

```
const collectionName = log_event.sender_name;
const collectionTicker = log_event.sender_contract_ticker_symbol;
const collectionAddress = log_event.sender_address;
const txHash = log_event.tx_hash;
```

Each log event then had some information that was decoded from the blockchain transaction such as:
```
const operation = log_event.decoded.name;
fromAddr = log_event.decoded.params[0].value;
const toAddr = log_event.decoded.params[1].value;
const valueName = log_event.decoded.params[2].name;
const value = log_event.decoded.params[2].value;
```

Depending on the operation (e.g. `Transfer`, `Transfer Single`, etc.) all of these parameters were slighlty different.

This took a lot of trial and error to refine but the final logic that decided whether a transaction should send an alert was:
```
/*
    Mints
        For wallet:
            * Needs to come from black hole address
            * Needs to go to the address of the owner
            * Transaction fromAddress needs to be the owner address
            * The value should be null
            * The operation should be Transfer
        For contract:
            * Need to come from black hole address
            * The to_address should be the address of the contract
            * The value should be null
            * The operation should be Transfer
*/
private shouldAdd(
    fromAddr: string,
    toAddr: string,
    txFrom: string,
    collectionAddr: string,
    trackedAddr: string,
    txValue: string | null,
    txValueName: string,
    toAddrLabel: string | null,
    isContract?: boolean
  ): boolean {
    if (txValueName === "value" && txValue !== null) {
      return false;
    }

    if (isContract) {
      if (
        fromAddr === BotConstants.BLACK_HOLE_ADDRESS &&
        collectionAddr === trackedAddr
      ) {
        return true;
      }
    } else {
      if (toAddr === trackedAddr && txFrom === trackedAddr) {
        return true;
      }
      if (toAddrLabel === "OpenSea" && toAddr === trackedAddr) {
        return true;
      }
    }
    return false;
  }
}
```

This is by no means perfect and it probably misses some new transaction types but it did work quite well.

## Cron jobs
To regularly poll the Covalent API I decided to use cron jobs. Every server could configure its own cron job and set the interval at which they wanted the polling to run.

This introduced a challenge: how to define a cron job for each server and restore it's state if the bot restarts.

The answer was fairly simple: store the cron job schedule expression and the running state in the database.

This meant that whenever the bot restarted I could go to the database, get all the servers that had a cron job running and restart the cron jobs.

The cron job itself just triggered a function that started the process of checking the lastest transactions for the tracked addresses by getting the data from the Covalent API.

```
const restartAllRunningCrons = async (client: DiscordClient): Promise<void> => {
  const runningCrons: MongoResult[] = await client.db.findAllStartedJobs();

  for (const dbData of runningCrons) {
    const serverData: ServerDataDTO = dbData;

    const scheduledMessage = new cron.CronJob(serverData.schedule, async () => {
      await getMintsScheduledJob(client, dbData._id);
    });

    scheduledMessage.start();
  }

  console.log(`Restarted ${runningCrons.length} crons.`);
};
```

## Monitoring
On top of the usual logging, I also started a basic Express server along side the bot to expose Prometheus metrics on an endpoint.

I could then import these metrics into an instance of Grafana to create some dashboards.

I was tracking some metrics such as the number of API calls, number of API errors, number of DB errors, number of servers the bot is in, number of unique addresses tracked.

<img src="https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/03/media/grafana-dash.png?raw=true" alt="Grafana Dashboard for the Bot" width="500"/>

*The Grafana Dashboard for the Bot*

## Monetization
I wrote a whole different post about this but it's worth quickly mentioning it here as well.
To be able to monetize this bot I implemented an access key system whereby in order to be able to use the bot you had to provide an access key.

To generate access keys I created a separate bot that did just that. To be able to request an access key from this bot you had to have a special role in Discord which you could only get if you were a verified owner of one of my NFTs.

The full code of the activation key bot is now also [publicly available on Github](https://github.com/pawKer/fresh-mints-activation-bot).

The Activation Key Bot was very simple and it had two tasks: 
1. Issue access keys to verified owners of the NFT
2. Invalidate access keys if users lost the owner role in Discord

The first task was achieved by simply generating new entries in a database where the access key was stored along side with any useful information about the user.

The second task was achieved by having the bot monitor every verified user of my bot to check whether they still had the correct owner role in Discord (the Collab.Land bot made sure to remove the role if the user transferred or sold the NFT).

The activation logic can be found [here](https://github.com/pawKer/fresh-mints/blob/main/src/commands/activation/activate.ts) and the access key generation can be found [here](https://github.com/pawKer/fresh-mints-activation-bot/blob/main/src/commands/activation-key.ts).

## Template
After creating these two bots, I realised they shared a lot of the logic so I wanted to create a reusable Discord bot template that would simplify the start up process for anyone wanting to create a bot. 

It can be found [here](https://github.com/pawKer/discord-bot-typescript-template) and it includes loading commands and events dynamically, a script to deploy commands, a basic implementation of MongoDB, a basic embed + docker, eslint, prettier, typescript configuration.

# Conclusion
I put a lot of time and effort into this little bot and it was a great learning experience. I got to learn about the Discord API, blockchain, MongoDB, caching, access keys and even Blender (for the NFT creation).

Unfortunately my monetization plans didn't turn out as expected but I'm still happy with the knowedlge I gained and hopefully someone will find my experience above useful.

HODL 🚀🌙 😂