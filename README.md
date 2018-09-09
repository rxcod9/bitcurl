# BitCurl #

An introduction to crypto exchanges [`curl`](http://curl.haxx.se/) commands.

## BITTREX ##
___
___

### PUBLIC API ###
___
___
#### Get Markets ####
___
Used to get the open and available trading markets at Bittrex along with other meta data.
___

basic command
```
curl -s https://bittrex.com/api/v1.1/public/getmarkets
```

json pretty print response
```
curl -s https://bittrex.com/api/v1.1/public/getmarkets | \
jq -r
```

___
#### Get Currencies ####
___
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

___
#### Get Ticker ####
___
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

___
#### Get Market Summaries ####
___
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

___
#### Get Market Summary ####
___
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

___
#### Get Order book ####
___
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

___
#### Get Market History ####
___
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

___
___

### MARKET API ###
___
___


> #### EXPORT API KEYS FIRST ####


 ```
export BITTREX_API_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
export BITTREX_API_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
 ```


>TODO___
___
___
### ACCOUNT API ###
___
___


> #### EXPORT API KEYS FIRST ####
 

 ```
export BITTREX_API_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
export BITTREX_API_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
 ```

___
#### Get Balances ####
___
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

___
#### Get Balance ####
___
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