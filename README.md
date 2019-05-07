
# API Documentation

SwitchDex's API gives you all the functionality of most market API's with more coming down the line. You can query orders,trades,deposits and withdrawals. Most of this content is direct to the smart contract so you can query the contract directly to obtain this information, however the API allows you to setup a websocket listener and act on the information as it comes in.

## Socket
There's only one API endpoint, temporarily hosted at:<br />`https://socket.switchdex.ag:8443`<br />
This endpoint will likely change in the future, however requests going to this URL will always resolve.

## Endpoints

### getMarket { token (address), user (address) }<br />
Both arguments are optional. Emit this message and then wait for a `market` response, which will contain:<br />`{ returnTicker, orders, trades, myOrders, myTrades, myFunds }`


### message (order)
This allows you to post an order.<br />(order) should be a JSON object with the following properties:<br />
`amountGive: the amount you want to give (in wei or the base unit of the token)`<br />
`tokenGive: the token you want to give (use the zero address, 0x0000000000000000000000000000000000000000 for ETH)`<br />
`amountGet: the amount you want to get (in wei or the base unit of the token)`<br />
`tokenGet: the token you want to get (use the zero address, 0x0000000000000000000000000000000000000000 for ETH)`<br />
`contractAddr: the EtherDelta smart contract address`<br />
`expires: the block number when the order should expire`<br />
`nonce: a random number`<br />
`user: the address of the user placing the order`<br />
`v, r, s: the signature of "sha256(contractAddr, tokenGet, amountGet, tokenGive, amountGive, expires, nonce)" after being signed by the user`
## Events
### orders
This will emit new orders as they are placed.<br />Its structure will mirror that of market.orders, except that some orders will have a deleted flag.<br />Orders with the deleted flag are no longer valid (canceled or traded).
### trades
This will emit new trades as they happen. Its structure will mirror that of market.trades.
funds<br />
## Rate Limiting
Please keep your connections to a minimum for what you need to do, there is a default rate limit of 6 connections per IP. If you need this increased please ask us on telegram. <br />
## Further Notes
There will be more detail coming in the future about the API with some examples, but right now this should be enough information to get you going.<br />Please keep in mind that this is a work in progress but also a decentralized exchange. Once you've placed a trade there is no way for us to reverse that trade.<br />If you're in doubt of how to use these functions or need more clarification please ask. <br />We've tried to keep all endpoints and events similar to what's out there currently for ease of use.
