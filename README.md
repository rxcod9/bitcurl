# BitCurl #

An introduction to crypto exchanges [`curl`](http://curl.haxx.se/) commands.

## BITTREX ##


### PUBLIC API ###

Get Markets
Used to get the open and available trading markets at Bittrex along with other meta data.

basic command
```
curl -s https://bittrex.com/api/v1.1/public/getmarkets
```

json pretty print response
```
curl -s https://bittrex.com/api/v1.1/public/getmarkets | \
jq -r
```

Get Currencies
Used to get all supported currencies at Bittrex along with other meta data.

basic command
```
curl -s https://bittrex.com/api/v1.1/public/getcurrencies
```

json pretty print response
```
curl -s https://bittrex.com/api/v1.1/public/getcurrencies | \
jq -r
```

Get Ticker
Used to get the current tick values for a market.

basic command
```
curl -s https://bittrex.com/api/v1.1/public/getticker?market=BTC-DGB
```

json pretty print response
```
curl -s https://bittrex.com/api/v1.1/public/getticker?market=BTC-DGB | \
jq -r
```

Get Market Summaries
Used to get the last 24 hour summary of all active markets.

basic command
```
curl -s https://bittrex.com/api/v1.1/public/getmarketsummaries
```

json pretty print response
```
curl -s https://bittrex.com/api/v1.1/public/getmarketsummaries | \
jq -r
```

Get Market Summary
Used to get the last 24 hour summary of a specific market.

basic command
```
curl -s https://bittrex.com/api/v1.1/public/getmarketsummary?market=BTC-DGB
```

json pretty print response
```
curl -s https://bittrex.com/api/v1.1/public/getmarketsummary?market=BTC-DGB | \
jq -r
```

Get Order book
Used to get retrieve the orderbook for a given market.

basic command
```
curl -s https://bittrex.com/api/v1.1/public/getorderbook?market=BTC-DGB\&type=both
```

json pretty print response
```
curl -s https://bittrex.com/api/v1.1/public/getorderbook?market=BTC-DGB\&type=both | \
jq -r
```

Get Market History
Used to get the last 24 hour summary of a specific market.

basic command
```
curl -s https://bittrex.com/api/v1.1/public/getmarkethistory?market=BTC-DGB
```

json pretty print response
```
curl -s https://bittrex.com/api/v1.1/public/getmarkethistory?market=BTC-DGB | \
jq -r
```


### MARKET API ###

#### EXPORT API KEYS FIRST ####


 ```
export BITTREX_API_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
export BITTREX_API_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
 ```


>TODO

### ACCOUNT API ###

#### EXPORT API KEYS FIRST ####
 

 ```
export BITTREX_API_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
export BITTREX_API_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
 ```


Get Balances
Used to retrieve all balances from your account.

basic command
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalances?apikey=$BITTREX_API_KEY&nonce=$NONCE"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" \
-s $URL

```

json pretty print response
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalances?apikey=$BITTREX_API_KEY&nonce=$NONCE"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" \
-s $URL | \
jq -r

```

Get Balance
Used to retrieve the balance from your account for a specific currency.

basic command
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalance?apikey=$BITTREX_API_KEY&currency=DGB&nonce=$NONCE"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" \
-s $URL

```

json pretty print response
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalance?apikey=$BITTREX_API_KEY&currency=DGB&nonce=$NONCE"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" \
-s $URL | \
jq -r

```