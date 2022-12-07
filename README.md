### Abstract

Blockchain gaming is regarded as a new path for the future growth of the game industry. Cryptocurrencies have altered the world of virtual assets with the help of the blockchain system, enabling more players to take part in creating and sharing the value of the games. However, there are also views that blockchain games are just another type of Ponzi scheme. To gather the necessary variables for this article, we used Python to crawl CHAINPLAY. gg, a website that compiles information about blockchain games. In order to present the development status of blockchain games as completely as possible, we analyzed the game platform, game chain, game market cap, investor situation, investment platform situation, guilds situation, etc., in this article. Through analysis, we discovered that blockchain games are currently evolving in a very unbalanced "winner takes all" scenario.

### Introduction

#### Background

Over the past few decades, the gaming industry has steadily changed and innovated, becoming a part of mainstream pop culture thanks to increased global interest. The gaming industry is currently estimated to be worth a staggering \$336 billion, potentially larger than all other media genres combined, according to a report by BITKRAFT Ventures and NAAVIK (BITKRAFT & NAAVIK, 2021).

The majority of players, however, have very few options to participate in the value without choosing the professional route because game developers and publishers hold complete ownership of everything that occurs in the games. But now, blockchain-based games are attempting to address this issue.

Blockchain is a cutting-edge implementation of distributed data storage, point-to-point transmission, consensus, encryption, and other Internet-era computing technology. Decentralization is its essential characteristic. Blockchain brings the following changes to the game industry: First of all, because blockchain data is transparent, players or outside organizations can audit the game rules, which increases trust in the gaming system. Second, players own virtual assets in blockchain games that have enormous market liquidity and are independent of the game operators. Encourage players to take a more active role in creating and sharing value within the game economy. Finally, unlike traditional games, blockchain games' user-generated content is saved by the players themselves. It has the potential to be shared across several games, incentivizing them to contribute to the creation of new content (Min et al., 2019).

#### Research Theme

1.2.1 Research Topic

Our research topic is the current state of blockchain gaming.

1.2.2 Related Concepts

Blockchain game: a set of digital games created and implemented by the characteristics of blockchain technologies.

Play-to-Earn: commonly known as GameFi or P2E, empowers regular players to influence important gaming industry choices. To make money more efficiently, it has sparked the development of sizable online communities, in-game economies, and company structures. Each game has monetary incentives for participation and achievement (Cricket Star Manager, 2022).

NFTs: In virtual environments, NFTs can take the form of anything, including objects, music, and more. In the instance of GameFi, users can "earn" digital assets through gameplay, which they can then choose to exchange for real money (Cricket Star Manager, 2022).

#### Motivation

The future of the gaming industry is thought to lie in blockchain gaming. However, a bad reputation for the new technology was created by numerous ICO frauds and worthless "air tokens." We are interested in what the blockchain game has brought. Therefore, it is important to research how blockchain games are progressing.

### Methods

CHAINPLAY is a blockchain game information website that aggregates a lot of information such as game’s market cap, token price, genre, etc. The overall structure of this site is in the form of tables, with many small tables split into large tables. The clear structure helps us to locate elements quickly, but unfortunately, this site uses many dynamic rendering techniques, which causes some difficulties for our crawling.

We mainly use *selenium*, *bs4* and *pandas* to collect information and have crawled over 1,700 games to analyze the current state of the GameFi industry.

### Variables:

#### Basic information:

In the home page list, we focus on information such as game name, game detailed page link, game token name, blockchain, game genre, running platform, token price, token value and game market value.It is worth mentioning that through the game detailed page link, we can get the contract address of the game token.

![descript](media/6cbf3c3f6905b5a4670526e7f9793e5e.png)Graph 3–1 Basic information (inspect the element)

#### 

#### Detailed information:

With the link to the game details page previously grabbed, we can access each game's detailed page to grab the token contract address, scholarship guild and partnered games.

![descript](media/536d9c64eb0b15c926b2df8748d5cc99.png)Graph 3–2 Detailed information (inspect the element)

![descript](media/8ec1ce4deece309cea0ee33a11b9a0c5.png)Graph 3–3 Detailed information (inspect the element)

With URL (<https://chainplay.gg/funding-rounds/>), we can enter the page presenting the recent crypto gaming funding rounds. Here we target at the information including projects, funding rounds, total funding amount and investors.

![descript](media/cbab95a96bed256df1140f35934f6abc.png)Graph 3–4 Detailed information (inspect the element)

Likewise, with URL (https://chainplay.gg/investors/), we can find the top venture capital firms investing in blockchain games. Here we target at all kinds of investor types, and the current ROI. And on "Gaming -ICO" page (URL: https://chainplay.gg/gaming-ico/), we target at the different tokens offering types as well as raised amount.

![descript](media/e48973a390ad75ef66d25c8ad65e6860.png)Graph 3–5 Detailed information (inspect the element)

![descript](media/98e375f709f5230a6bb91fe691e95202.png)Graph 3–6 Detailed information (inspect the element)

With URL (<https://chainplay.gg/fundraising-platforms/>), we can enter the page of fundraising platform. In this page we need to obtain these information, including IDO platforms, current ROI, all time high ROI, token generate events, and amount raised.

![descript](media/a885efc1f106d792c8b356dc4366e12b.png)Graph 3–7 Detailed information (inspect the element)

By entering the URL (https://chainplay.gg/guild-performance/), we can access the guild performance page. In this page, we can get the information of Guilds name, market capitalization, and partnered games.

![descript](media/10f70e924de7777ddc37dde973ebd3c3.png)Graph 3–8 Detailed information (inspect the element)

### Procedure

#### Basic information:

For most of the elements in the home page list, we used the css selector in selenium to locate and get the text, and put the information we got in the custom list.

![descript](media/5fc0f825a1ea398e03563d5a653aa814.png)Graph 4–1 Basic information (code)

The next page of the main list does not have a separate link, but loads on the main page when the button was clicked. So we use selenium to simulate the manual click on the next page and use for loops to crawl for information.

![descript](media/a932223f9d407b29354d588afd030a19.png)Graph 4–2 Basic information (code)

However, Blockchain and platform do not have any text attribute or value in the source code, the way texts appear on the website is by hovering over the icon. We couldn't solve the source code directly, but we found that the icons had corresponding hyperlinks that had the characters we wanted, so we crawled the hyperlink text and extracted the characters we wanted by string processing.

![descript](media/e1a5ab85e69a24a1dcbcdcbd5fd0a4ef.png)Graph 4–3 Basic information (code)

![descript](media/f82e9fe9b3cbb8a8451603df83cae53a.png)Graph 4–4 Basic information (code)

![descript](media/7553e258568c82fbada830512b8b0ce6.png)Graph 4–5 Basic information (code)

#### 

#### Detailed information:

The scholarship guild and partnered games are not different from the previous methods, just locate and get the text, but the token contract address is very special. The token address is an incomplete text both in the source code. But we found that when we clicked the copy button the full address appeared in the system clipboard. So we took selenium to simulate the click and used pandas to read the data from the clipboard.

![descript](media/4eb1f90ba16f8f34d0a0c6dde554175e.png)Graph 4–6 Detailed information (code)

For funding rounds and gaming ICOs, we used the css selector to get the information we want.

![descript](media/4e37c6ae004c83dd9663956df21f6ef3.png)Graph 4–7 Detailed information (code)

![descript](media/3a3a7c914454a87bf3483efd74f72bfe.png)Graph 4–8 Detailed information (code)

For investors, we also used css selectors. But the investor type cannot be selected directly, so we got the link at first and extracted the investor type from it.

![descript](media/b51e346dc171ab5a96de0038887b7cc1.png)Graph 4–9 Detailed information (code)

For fundraising platforms, we used the css selector to get the information we want. However, blockchain information cannot be obtained directly from the icon. So we first got the platform's detailed page link, and then got the blockchain name from the detailed page.

![descript](media/8dc9e88d721637e01dc5a35d0f016ef2.png)Graph 4–10 Detailed information (code)

![descript](media/8fa5934a6a74739455049f5b8a641dd8.png)Graph 4–11 Detailed information (code)

The procedure of crawling relevant information on the game guilds page is consistent with the above-mentioned part.

![descript](media/dc4ad30848efad6b0590c44094d8e7d3.png)Graph 4–12 Detailed information (code)

### Data format & Raw data

After finishing the steps above, we used pandas to store the basic information data in csv file.

![descript](media/a9c7bffb2bae1c5326f00fa682f9b89b.png)Graph 5–1 Data format (code)

![descript](media/655f0b12f9d0a95cd055feb65d15dbb1.png)Graph 5–2 Raw main form (1738 rows × 11 columns)

Here is the table of funding rounds, we also used pandas to store information.

![descript](media/f69a9a3d28df559e6a3ce212ec2a237d.png)

Graph 5–3 Data format (code)

![descript](media/0fad260879179c558de28f807edfdbda.png)Graph 5–4 Raw scholarship form (467 rows × 4 columns)

And we used the same method to output the table "Gaming ICOs" and "investors".

![descript](media/b93e3cccdae00c9e535ac3142261c7e3.png)Graph 5–5 Data format (code)

![descript](media/582634124fa766d3c4012fc3fb2f16a0.png)Graph 5–6 Raw scholarship form (822 rows × 10 columns)

![descript](media/5260161c2f73a0bac03cbe4bd9d8ee0c.png)Graph 5–7 Data format (code)

![descript](media/d44012438819e384e7acb7d6ae602198.png)Graph 5–8 Raw scholarship form (724 rows × 6 columns)

We also generated a table of games, scholarship guilds, and guild partner games.

![descript](media/60b3518c21ee88b51e42a1a50d5c60de.png)

Graph 5–9 Raw scholarship form (1738 rows × 3 columns)

The table of the game guilds, including token price, market capitalization, discord index, number of partnered games, and investors.

![descript](media/44a3ae8d01671a23c4a81f0d07dca4e0.png)Graph 5–10 Raw guilds form (22 rows × 6 columns)

#### Data processing

As is shown in Graph 5–9, there is no one-to-one correspondence between the number of scholarship guilds and collaborations, so we used the explode function that comes with pandas to split this table and rename the columns.

![descript](media/3681567d22793f8f341852a15e089f08.png)Graph 5–11 Exploded scholarship form (1738 rows × 3 columns)

![descript](media/c7302fc0d02d8d176386b759f9db03ac.png)Graph 5–12 Exploded scholarship form (1738 rows × 3 columns)

We merged the main form and the scholarship form to produce a complete main form.Finally we exported the table for further analysis and visualization in excel.

![descript](media/3a02a177eaaed6cf51d835f095de02b7.png)Graph 5–13 Main form (2010 rows × 14 columns)

### Results

*Which* **platforms***are more* **easy to play** *Blockchain games ？*

![descript](media/b20ed7b91732989c727541c46b7d1a49.png)

In the current network environment, the most widely used platform for blockchain games is browser, with 1257 games adapted. Android and iOS followed with 551 and 510 games respectively. But there may be a trend towards simultaneous development of Android and iOS and other mobile environments, after all, it is the era of mobile terminals.

*How many* **games** *have launched* **on the blockchains?** *How about* **the distribution of single-chain games and multi-chain game***s?Which is the* **most popular blockchain for the games**

![descript](media/2a2daa4b44820df828113de66ce1d5da.png)![descript](media/5a9589ca5c0d6d7a0877baae1516c9f6.png)![descript](media/874e7658a56a8e4e1cbc30ebfc2e1a40.png)

Among the games that have been launched, 94% of the games have been on the blockchain, and only 6% of th remain have not yet been on the blockchain. The vast majority of blockchain games are single-chain, accounting for 91%. In terms of the amount of games and the market cap of games, Ethereum and BSC both occupy the top 2 positions. BSC is dominant in the number of games selected (774 games, accounting for 41% of the total number of games); and Ethereum contributes 80% of the game market value with \$4.544 billion, which is absolutely dominant.

*What do* **Market Cap** *talk about* **blockchain games** *market?*

![descript](media/87df114b9868fa849aa51af42aeac68c.png)![descript](media/e36ac5e886eb22c6e21ebc42df7e8813.png)

The market capitalization of blockchain games released by the top 10 games account for 76% proportion that it has a great impact on the entire blockchain games market. The Sandbox has the highest market valuation at over \$1 billion, followed by Decentraland with \$941 million and Axie Infinity with \$792 million, occupying second and third places respectively, far ahead of other games.

![descript](media/c11b7eae9de1e7fcdd4d4d260df91753.png)**How many games** *are currently running* **fundraising funding rounds***? How much* **fundraising funding amount** *does each* **funding rounds raise** *separately?* **Which projects** *are most* **favored by capital***？*

![descript](media/35181b8dc9bfc1167dbf5b71072b9502.png)

There are 464 projects in the fundraising funding round, with a total fundraising funding amount about \$2,952 million, of which up to 46% of the game projects are in the private round, but the funding amount of this round is smaller. The seed round is the largest fundraising funding amount, accounting for 23% of the total funding amount, and the second one is the Sereies A round, accounting for 23%.

![descript](media/65cdddd0c3c480e653173f4a23fa23df.png)

The Limit Break project has the largest funding amount, which makes us interested in it. Founded by former Machine Zone CEO Gabriel Leydon, Limit Break is dedicated to transforming the gaming industry through FREE-TO-OWN (F2O) NARRATIVE. Such a huge funding amount maybe have a lot to do with the previous success of Limit break founder Gabriel Leydon, whose mobile game company Machine Zone has developed a number of best-selling games, including " Game of War: Fire Age", "Mobile Strik" and "Final Fantasy XV: A New Empire".

*Which* **investor type** *is the most* **popular of the Venture Capital Firms***？ What is the* **current situation** *of the blockchain games* **Investors***?*

![descript](media/2c10f2e867ee52eec929c9363681a727.png)![descript](media/50cd42c8b605db5fb2a15546128495ba.png)

![descript](media/97af5111f2edecfeb1fb418454d3a219.png)![descript](media/777c1967970208009d66d1bde7cd06c2.png)

When it comes to fundraising investors, there are a total of 689 investors. However, it can be assumed that nearly half (47%) of the companies are not actively investing and have not made any investments in the blockchain games yet. Only 11% of the investors can invest in more than 10 projects. The most active companies are X21 Digital and Animoca Brands, both with 77 investments. And ignoring 49% of no data, 32% of current fundraising ROI of investors is less than 100%，meaning that more than half of the investors are losing money at the current stage.

*On the Gaming ICOs page, what was the past crypto gaming* **tokens offering type** *?* **How much fundraising** *has been for these games that have already been on public sale? What were their* **distribution trends***? Which game was the* **biggest fundraiser***?*

![descript](media/1156c3bbb979abd19e67246deb9fd767.png)![descript](media/dc717a5c507e7b98ebed6c60d50a0a41.png)![descript](media/6d1b36a6d06453e8bd81dd8db76fe747.png)

![descript](media/c35f5cd12da6293d8291b0df75a86f2f.png)

A total of 822 token offers were made for 374 games, 796 of which chose the IDO type, accounting for 97% of the sale type, occupying an absolute choice. For the 374 games, 292 of the funds raised by a single game were concentrated in the range of less than \$500,000, accounting for 78%. Therefore, the corresponding total amount of funds raised was relatively high, with 7,6729,285 dollars, nearly 50% of the total amount raised by all games. Although there are only 18 games\` raised fund more than 1 million raised, their total raised fund still account for 20% of the total raised. Among them, the game with the biggest raised is Froyo Games FROYO, with 4 million dollars.

*What is* **the size of the fundraising amount** *for games on all IDO platform? What is* **the past situation and current situation** *of the blockchain gaming launchpads on all IDO platform?*

*![descript](media/c0a033fa01b3210a9ab139fbb68d1d7f.png)![descript](media/81b0c0923c35c4235c8e7da67278c127.png)![descript](media/fdc01b5dc42533a2e882269ce1692f1a.png)*

Total fundraised in gaming category on all IDO platforms is \$124.97M. The fundraising platform chosen by games is not overly concentrated, and the platform with the highest fundraising amount is PancakeSwap, which has \$9,487,500.By comparing the number of raised money and Token Generation Events on different fundraising platforms, we can find that, for projects with high fund-raised funds, their Token Generation Events show a downward trend of fluctuation. In other words, projects with high fund-raising funds generally may have more Token Generation Events.

By comparing the number of fundraising funds and Token Generation Events on different platforms, we can find that there is an overall correlation between them, and projects with high fundraising amounts are generally more Token Generation Events.Through the histogram comparison table of All Time High ROI and Current ROI, it can be seen that the fundraising platform has formed a clear downward trend between the historical high and the current market, and current return on investment is not ideal. This can be seen by taking a deeper look at the current fundraising ROI pie chart: nearly 80% of current ROI of fundraising games is less than 100%，while there are 10% of games that have no data. The current ROI of fundraising games on IDO platforms and investor which we discussed before reflect that low return on fundraising investment has become the mainstream trend of the blockchain game markets, and the current blockchain games market is sluggish.

**Which gaming guilds** *are most* **favored by capital***？Is the* **market cap** **of the guild** *related to* **the number of games** *released?*

![descript](media/1181899e4c68227f57ad366528951d0b.png)![descript](media/e6f72a6df0689fe0dfc4082f2fea0884.png)

In the 22 gaming guilds, only 10 of them reported their game market cap, of which Merit Circle MC has 65% of the total market cap at \$143,703,743 followed by Yield Guild Games YGG with 20% of the market cap;however, as can be seen from the line chart, the number of partner games of the guild is not positively correlated with the market cap of the guilds.

*How many* **upcoming events** *in the* **process of fundraising***? Which I***DO platform** *is the most* **popular** *and what are the reasons behind it?*

![descript](media/9e859d7c191738b3ed1195d593d6dd98.png)![descript](media/2171acb0446233edb983fcbd0fcf1320.png)

For the 146 upcoming events, 141 of them chose Token Sale for issuance, becoming mainstream with an absolute margin of 97%. By releasing multiple rounds of fundraising plans on different IDO platforms, Reign of Terror became the highest fundraisinge goal among upcoming events, reaching \$26.3 million, accounting for 49% of all upcoming events.

![descript](media/72c24b3b1db789993ed4341d4e67ecc4.png)![descript](media/c9d7032f78f00eaec3a658b951400fb4.png)

Although there is no trend of concentration among different projects on the IDO platform, IDO on StarLaunch raised \$25,250,000, accounting for 47% of the upcoming events fundraising, and in this level, it has become the most popular IDO platform.

### Conclusions

It is debatable whether blockchain games, an emerging trend in game development, can take the gaming industry in a new direction. The primary purpose of this research is to explore the current development status of blockchain games. To create a more thorough description, we crawled as much of Chainplay. gg's relevant content about blockchain games. The analysis of the blockchain game platform, chain, game market value, investor situation, investment platform situation and game guild expanded our understanding of the development status of blockchain games.

The data analysis results show that 91% of games on the platform are single-chain games, and mobile terminals and browsers are both the leading platforms for users to play.

In terms of blockchain, the number of games on the bsc and Ethereum account for nearly 60% of the total. And Ethereum makes up 80% of the market value of games, which is overwhelming. The top 10 games that Chainplay.gg released in their market capitalization for blockchain games make up 76% of the total market capitalization.

As for funding projects, most of the projects are still in the seed round and private placement stage, which accounts for 81% of the total number of projects. Projects in the seed round raised the most funds, accounting for 23% of the total funding amount. At the same time, the Limit Break project is the one with the most funding.

Regarding fundraising investors, about 52% of venture capital firms are of Crypto Ventures. As for Initial Coin Offering, 5% of games raised more than \$1 million, and these games accounted for 20 per cent of the total funds raised.

From the perspective of return on investment, 32% of investors, who make up the vast majority of all investors, have an investment return rate of less than 100%, and 80% of the fundraising platforms have an investment return rate of less than 100%. Of course, at the same time, only a few investors have obtained high profits. Based on the analysis results above, we argued that the current state of blockchain games is a very unbalanced "winner takes all" situation, and related investments are risky.

Also, this study has some limitations: First, we cannot conduct a long-term dynamic data monitor because our data scraping capability is still in its infancy. Second, there might be an easier way to do all the data crawling; our code needs to be simplified.

### Reference

BITKRAFT, V., & NAAVIK (2021). Gaming Industry Nearly Twice as Large as Reported, at \$336B. <https://www.bitkraft.vc/gaming-industry-market-size/>

Cricket Star Manager (2022). Play-to-Earn: The New Crypto Standard Changing the Future of Online Gaming. Medium. https://medium.com/@cricketstarmanager/play-to-earn-the-new-crypto-standard-changing-the-future-of-online-gaming-6472bbb55252

Min, T., Wang, H., Guo, Y., & Cai, W. (2019). Blockchain Games: A Survey. 2019 IEEE Conference on Games (CoG). https://doi.org/10.1109/CIG.2019.8848111
