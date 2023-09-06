![Article Banner](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/02/media/article-banner.jpg?raw=true)

During the surge crypto and NFT popularity in 2021/2022 I set out on a mission to monetize my software project by making use of these emerging technologies.

At a high level the solution I found involved creating and selling an NFT on OpenSea which would give any potential owners the right to generate an access key for my application.
## The application

During this digital gold rush, thinking of ways to make money with NFTs, one strategy I found was tracking the moves of NFT influencers or people with know-how in the space and buying the same NFTs
they bought in the hopes that they might have some insider information which might translate into profitable resale opportunities (or this was the theory at least).

To help with this, I built a Discord bot that allowed you to track multiple Ethereum wallet and contract addresses and notified your server when there was a new purchase on OpenSea. Initially it was just my friends and I using it but I quickly started thinking of ways I could monetize it by opening it up to more users. I will go into more detail about this bot in a separate post 👀.

## Access control

Firstly, I needed a way to restrict access to the bot and the quickest and easiest way I could think of was to have users provide an access key to enable the bot after it was added to their server, effectively granting them access to its features.

After I got this implemented, the next step was to figure out a way to make NFTs act as the access key.

## Eternally on the blockchain

Creating the actual NFT was surprisingly straightforward, especially since I didn't need a custom contract. I just created a visually pleasing GIF and uploaded that to OpenSea.

<img src="https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/02/media/os-create-new.png?raw=true" alt="OpenSea Create New NFT" width="400"/>

*OpenSea Create New NFT Form*

The only interesting thing about this was that instead of creating 1000 (or however many access keys I wanted) unique NFTs, I could just set the supply of this one NFT to 1000. This meant the NFT could have more than 1 owner and people could also buy more than 1 of this NFT.

![OpenSea NFT Supply](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/02/media/os-supply.png?raw=true)

*OpenSea NFT Supply Setting*

If you're curious, my NFT collection can be found [here](https://opensea.io/collection/fresh-mints-bot).

## The bots I was looking for

This is where [Collab.Land](https://www.collab.land/) came in. Collab.Land is a Discord bot that allows server owners to verify if a user owns a specific NFT and give that user a certain Discord role if they do.

This was a well-known tool used by many other Discord servers at the time and it was perfect for this use case.

Since I could control access to certain bot commands based on the Discord roles of a user, this meant I could have a command that generated an access key for my bot that only users with the NFT owner role could execute.

## Registration flow

With this information in mind, this was the user registration flow I envisioned:

1. New user joins my application's Discord server
2. They buy the NFT on OpenSea
3. They verify their ownership in the server
4. They generate an access key
5. They can now use my bot 🥳

## Server setup 

Based on the above, I started by creating a Discord server that any user of my application had to join to verify ownership and obtain an access key. I then added Collab.Land to this server.

To configure the Collab.Land bot you just had to point it to the NFT collection that you wanted your users to own, configure how many they should have and what role you want to give them if they meet these conditions. You could also have it monitor this regularly in case users sold or transffered these NFTs, for example.

In my case, the Discord bot was called `Fresh Mints` (good right?) so I named the NFT collection `fresh-mints-bot` on OpenSea, I wanted any user to have at least 1 NFT and I created an owner role called `Fresh Family` (😅).

![Collab.Land Setup](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/02/media/collab-land-setup.png?raw=true)

*The Collab.Land Setup*

Now anyone could join the server and easily verify their assets to obtain the `Fresh Family` owner role.

![Collab.Land Verification](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/02/media/collab-land-verify.png?raw=true)

*The Collab.Land Verification Prompt*

## Managing access keys

At this point I could have just manually given users with that role an access key but to automatically manage the access key generation and validation I actually created a second bot that did just that.

It was a simple application that created and managed UUIDs (the access keys) in a database while also storing relevant information about the owner and the validity of the key.

![Activation Key Example](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/02/media/activation-key-example.png?raw=true)

*Activation Key Example*

It only allowed users with the `Fresh Family` role to generate an access key by running a Discord command but it also monitored the server and in case someone lost that role it would deactivate their instance of the bot.

![Bot Activation Command](https://github.com/pawKer/blog.raresdinu.ro/blob/main/articles/02/media/activation-step.png?raw=true)

*Bot activation command*

## Putting it all together
So, there you have it – just like that I was able to take payment for the access to my application using NFTs and crypto without the need for setting up any complex payment system.

It looked good on paper, and the few users that joined were able to complete the process without issues. But, as the crypto market cooled off and NFTs lost their buzz, the bot didn't quite reach the heights I'd hoped for. Still, it was a good learning opportunity and a chance to surf the new crypto wave for a moment 🌊🏄‍♂️.