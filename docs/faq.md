# Binance Chain FAQ v0.3

## What is Binance Chain, or Binance DEX?

Binance Chain is the blockchain initially developed by Binance and community. Binance DEX is the 
decentralized exchange module developed on top of the Binance Chain blockchain. 

## What is the design principle of Binance Chain?

The main focuses for the design of Binance Chain are:

- No custody of funds: traders maintain control of their private keys and funds.
- High performance: low latency, high throughput for a large user base, and high liquidity trading. 
We target to achieve 1 second block times, with 1 confirmation finality.
- Low cost: in both fees and liquidity cost.
- Easy user experience: as friendly as Binance.com.
- Fair trading: minimize front-running, to the extent possible.
- Evolvable: able to develop with forever-improving technology stack, architecture, and ideas.

## What can you do on Binance Chain?

You can:

- Send and receive BNB
- Issue new tokens
- Send, receive, burn/mint and freeze/unfreeze tokens 
- Propose to create trading pairs between two different tokens
- Send orders to buy or sell assets through trading pairs created on the chain

## Will Binance Chain introduce more features and transaction types in the future?

Yes, Binance Chain team and community would pay attentions to the technology advance and requirement trends to make value-transfer and value-exchange easier and easier.

## What is the native coin on Binance Chain?

The Binance Coin, BNB, will be the native asset on Binance Chain. There are 200MM BNB coins in total. 
There will be no mining. The existing coin burns and freezes will still be in effect on the new 
Binance Chain blockchain.

The exact number of BNB coins will be destroyed based on the same number of BNB ERC20 tokens 
that have already been destroyed.

After Binance Chain is live, all BNB ERC20 tokens will be swapped for Binance Chain coins. All 
users who hold BNB ERC20 tokens can deposit them to Binance.com, and upon withdrawal, the new 
Binance Chain native coins will be sent to their new wallets.

## How can I register on Binance Chain/DEX and start trading?

There is no need to register. All you need is a Binance Chain address, which can be generated with 
any wallet that supports Binance Chain. Then you can trade BNB or other assets stored on that address.

## How can I send orders on Binance DEX?
### Order

On Binance DEX, you can send "new order" messages to  buy or sell certain assets. You can also 
send "cancel" messages to cancel existing open orders.

You can use a wallet to send new orders and cancels. Binance DEX also provides API for automatic trading.

In Binance DEX v1.0, the order message contains:

- Symbol: trading pair on the chain
- Side: buy or sell
- Price: only limit price orders are supported in Binance Chain v1.0
Amount
- Time In Force: Binance DEX supports `Immediate Or Cancel` (IOC) and `Good Till Cancel` (GTC) 
orders. GTC orders can quote on the exchange until they are filled by the opposite orders satisfying 
the limit price, or canceled by client themselves, or expire after 72 hours after 00:00 (UTC). 
Check the "What is `Order Expire`" section of the FAQ for more information.
  
Network nodes examine orders to ensure they are valid. Once the orders are accepted, they are 
booked on the next block, and get matched accordingly.

### Match

Binance DEX does all of its matching on the blockchain, i.e. all nodes perform the matches and 
expect the same result. This is to ensure the maximum transparency and to mitigate the chance 
for front-running, even from the block producers. The matching infrastructure is expected to 
evolve and grow in capacity as time progresses.

Binance DEX doesn't do continuous matching as most centralized exchanges do. Instead, it matches 
using periodic auction matching for all the existing open orders received in the past and the 
latest blocks. The match logic is explained in more details later.

### Trade

Once the orders are filled, the corresponding assets would be automatically moved into buyers' 
addresses. The confirmation is instant and no need to wait for further blocks (i.e. T+0 block). 
Buyers can use the bought asset right away, either send it to another address or trade it again.

## Where can I see my assets and trades?

You can always use wallets that support Binance Chain to check your asset balances, open orders, 
and (optionally) order/trade history. Binance Chain Explorer is another tool to check balances 
and transactions.

## When can I see my order on the blockchain after I send it?

It depends. Normally, if you connect to one of the Accelerated Nodes, your orders should get 
accepted and booked into a block in 1-3 seconds. If the order price is marketable, the order 
would be filled and trades would come back in about similar time. If you send from a far-way 
self-setup full node, or there is heavy network traffic, the order may take longer to reach 
a Validator (block producer).

## Can I see others' orders or balances or can other people see my orders or balances?

Yes, anyone can see anyone's orders and balances if they know the corresponding addresses. 
Binance Chain is 100% transparent for transactions and balances.

## What is the Fee Structure?

Fees are charged and shared among the block producers (i.e. Validator) to run the network, 
in order to pay for the network usage and prevent abuse and attack. Since all user transactions, 
include transfer, new order, cancel etc. are recorded in blocks and chain state, the fee would be 
shared among different transactions. New orders are exempt from fees to encourage usage and larger 
trades would be charged more for their benefits from the liquidity provided in the network. 
Order Expire and Cancel are also charged with a fee if they fail to provide any liquidity.

Fees can be paid in any asset, but the network would charge BNB first and apply a discount if the 
address has BNB balance.

The fee is subject to periodical review and adjustment, after agreement from validators, via a 
proposal-vote procedure.

- Trade fee is calculated based on trade notional value, while fees for other transactions are fixed. 
- It is free to send a new GTC order, cancel a partially filled order, or expire a partially filled order.
- Non-Trade related transactions would be charged with a fee when the transactions happen, and can 
only be paid in BNB. The transaction will be rejected if the address does not have enough BNB.
- Trade-related transactions would be charged with a fee when an order is filled, or 
canceled/expired/IOC-expired with no fills. If there is enough BNB to pay, BNB fee structure would 
be used, otherwise, non-BNB fee structure would be used. 
- If the whole order value and free balance for the receiving asset are not enough to pay the fee, 
all the receiving asset and its residual balance would be charged.

## What is `Order Expire`?

Orders accepted by Binance DEX would either get filled with other orders or remain in the order book, 
but they would not stay on the order book forever. These orders will expire and be removed from the 
order book after the 1st midnight (UTC) after 72 hours once the order gets accepted. A small fee 
would be charged for the network usage, if there is no fill at all for the order (deemed as no intention to trade).

## What is `Immediate Or Cancel order`?

Immediate Or Cancel is a special order type. Once the order is accepted into a block, Immediate Or 
Cancel orders only exist in this block round. The order may get filled to zero, or partially or fully 
filled by other orders, and then would become expired and removed from the order book right away. 
As a result, it would not be tradable in the next round of matching. A small fee would be charged 
for the network usage, if there is no fill at all for the order (deemed as no intention to trade).

## I forgot the private key for my address, how can I get it back?

Sorry, you cannot. Owner of the address takes full responsibility of the private key protection. 
Binance Chain and official wallets do not have your private key.

## My private key got stolen by hackers, how can I recover my assets?

Sorry, you take full responsibility of your private key ownership and protection. Binance Chain 
and official wallets would not record, or transfer out your private key.

##  Is there any limit to using the API to send orders or check market data?

Yes, there are rate limits to ensure no waste and abuse on the network infrastructure. Please 
check the API documentation.

## What does Wallet and API cost to use?

No fee or commission at all.

## What Market Data can I get?

The market data provided via Wallet and API are similar to Binance.com, including ticker data, order book, 
trade and KLine. They can be watched from Wallet and read from REST or Websocket API. Please check 
the API documentation for details.

## What is the Accelerated Node?

While users can submit transactions and most of the queries via normal, self-run full nodes, Accelerated 
Node provides more secure and faster lines to access Binance Chain.

Accelerated Node is special infrastructure built around Validator to facilitate accelerated transaction 
routing and provide richer, faster user interfaces. There are always several Accelerated Nodes running 
at the same time around the world ( owned by different organizations) and you are encouraged to choose 
one of them to use, or allow Wallet / API Lib to choose one randomly.

## What are the tick size and lot size? Are they fixed?

Tick size is the minimum unit to increase or decrease for the price (in quote asset) of an order, 
while lot size is the minimum unit to increase or decrease for the quantity (in base asset) of an 
order. They are not the same as on Binance.com. They can be queried from API or checked from Wallet UI.

Tick Size and lot size are not fixed. Binance Chain would automatically review the values to make 
sure proper order size and notional periodically.

## Are there limits on notional value of an order?

The smallest order you can send for a trading pair is 1 lot size quantity at 1 tick size price. No other limits.

## What is the decimal precision for prices and quantities on Binance Chain/DEX?

Amounts are represented as integers, and all coins have a fixed scale of 8. This means that if 
a balance of 100000000 were to be exposed to a wallet integrator, that would represent a balance of 1 coin.

## How can I issue an asset?

Anyone can pay a fee and issue an asset as Token on Binance Chain, as long as they provide 
proper information for the below, and then run through the command line or http interfaces.

- Name: a description string less than 21 letters
- Symbol: an identifier string less than 9 letters, which must be composed of [0-9A-Z]
- Total Supply: a positive number less than or equal to 90 billions
- Mint-able: whether the token can increase Total Supply in later time or not

## What is the consensus algorithm used on Binance Chain?

Binance Chain uses BFT and PoS (upcoming) based consensus mechanism to produce blocks among 
a series of qualified Validators. This is similar to the architectures of several existing 
popular blockchain platforms such as EOS and NEO.

## Can I run a full node for Binance Chain?

Yes, you can. A full node contains all the information and application logics for Binance Chain. 
It can receive and broadcast blocks and transactions with other full nodes and even validators. 
The only exception is it would not participate consensus if the full node is not a Validator.

## Does Binance Chain support Smart Contracts?

No. This was an intentional design decision to improve the performance of the system and eliminate 
having to support unnecessary features.

## How can I transfer tokens, such as Bitcoin, from other block chains onto Binance Chain?

Native inter-chain mechanism is not supported in Binance Chain in the initial version, but may 
be in the future. Binance.com may serve as a bridge to trade across tokens between Binance 
Chain and other chains. Peg Token may be issued on Binance Chain to facilitate trading digital 
asset from other block chains.

## How would a third-party integrate with Binance Chain and Binance DEX?

A wallet provider may choose to only support the feature set of Binance Chain, which would just 
cover wallets, addresses, balances and transfers. To improve their implementation further, 
they could choose to integrate Binance DEX which would add trading, order history, cancellations, 
trading, charts, etc.
