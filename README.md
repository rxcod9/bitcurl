# BitCurl #

Some useful [`curl`](http://curl.haxx.se/) commands for top crypto exchanges.

## BITTREX ##
___
___

### PUBLIC API ###
___
___
#### Get Markets ####
Used to get the open and available trading markets at Bittrex along with other meta data.

basic command
```
curl -s "https://bittrex.com/api/v1.1/public/getmarkets"
```

with pretty json response
```
curl -s "https://bittrex.com/api/v1.1/public/getmarkets" | jq -r
```

Table format output
```
curl -s "https://bittrex.com/api/v1.1/public/getmarkets" | \
jq -r ' ["MarketCurrency","BaseCurrency", "MarketCurrencyLong", "BaseCurrencyLong", "MinTradeSize", "MarketName", "IsActive", "Created", "IsSponsored", "Notice"], (.result[] | [.MarketCurrency, .BaseCurrency, .MarketCurrencyLong, .BaseCurrencyLong, .MinTradeSize, .MarketName, .IsActive, .Created, .IsSponsored, .Notice]) | @tsv' | \
awk -F '\t' '{print $1 "\t" $2 "\t" $3 "\t" $4 "\t" ($5=="MinTradeSize" ? $5 : sprintf("%.8f",$5)) "\t" $6 "\t" ($7=="" ? "NA" : $7) "\t" $8 "\t" ($9=="" ? "NA" : $9) "\t" ($10=="" ? "NA" : $10) "\t"}' | \
column -t -s $'\t'
```

Table format output one liner
```
curl -s "https://bittrex.com/api/v1.1/public/getmarkets" | jq -r ' ["MarketCurrency","BaseCurrency", "MarketCurrencyLong", "BaseCurrencyLong", "MinTradeSize", "MarketName", "IsActive", "Created", "IsSponsored", "Notice"], (.result[] | [.MarketCurrency, .BaseCurrency, .MarketCurrencyLong, .BaseCurrencyLong, .MinTradeSize, .MarketName, .IsActive, .Created, .IsSponsored, .Notice]) | @tsv' | awk -F '\t' '{print $1 "\t" $2 "\t" $3 "\t" $4 "\t" ($5=="MinTradeSize" ? $5 : sprintf("%.8f",$5)) "\t" $6 "\t" ($7=="" ? "NA" : $7) "\t" $8 "\t" ($9=="" ? "NA" : $9) "\t" ($10=="" ? "NA" : $10) "\t"}' | column -t -s $'\t'
```

___
#### Get Currencies ####
Used to get all supported currencies at Bittrex along with other meta data.

basic command
```
curl -s "https://bittrex.com/api/v1.1/public/getcurrencies"
```

with pretty json response
```
curl -s "https://bittrex.com/api/v1.1/public/getcurrencies" | jq -r
```

Table format output
```
curl -s "https://bittrex.com/api/v1.1/public/getcurrencies" | \
jq -r ' ["Currency", "CurrencyLong", "MinConfirmation", "TxFee", "IsActive", "CoinType", "Notice", "BaseAddress"], (.result[] | [.Currency, .CurrencyLong, .MinConfirmation, .TxFee, .IsActive, .CoinType, .Notice, .BaseAddress]) | @tsv' | \
awk -F '\t' '{print $1 "\t" $2 "\t" $3 "\t" $4 "\t" $5 "\t" $6 "\t" ($7=="" ? "NA" : $7) "\t" ($8=="" ? "NA" : $8)}' | \
column -t -s $'\t'
```

Table format output one liner
```
curl -s "https://bittrex.com/api/v1.1/public/getcurrencies" | jq -r ' ["Currency", "CurrencyLong", "MinConfirmation", "TxFee", "IsActive", "CoinType", "Notice", "BaseAddress"], (.result[] | [.Currency, .CurrencyLong, .MinConfirmation, .TxFee, .IsActive, .CoinType, .Notice, .BaseAddress]) | @tsv' | awk -F '\t' '{print $1 "\t" $2 "\t" $3 "\t" $4 "\t" $5 "\t" $6 "\t" ($7=="" ? "NA" : $7) "\t" ($8=="" ? "NA" : $8)}' | column -t -s $'\t'
```

___
#### Get Ticker ####
Used to get the current tick values for a market.

basic command
```
curl -s "https://bittrex.com/api/v1.1/public/getticker?market=BTC-DGB"
```

with pretty json response
```
curl -s "https://bittrex.com/api/v1.1/public/getticker?market=BTC-DGB" | jq -r
```

Table format output
```
curl -s "https://bittrex.com/api/v1.1/public/getticker?market=BTC-DGB" | \
jq -r ' ["Bid", "Ask", "Last"], (.result | [.Bid, .Ask, .Last]) | @tsv' | \
awk -F '\t' '{print ($1=="Bid" ? $1 : sprintf("%.8f",$1)) "\t" ($2=="Ask" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Last" ? $3 : sprintf("%.8f",$3))}' | \
column -t -s $'\t'
```

Table format output one liner
```
curl -s "https://bittrex.com/api/v1.1/public/getticker?market=BTC-DGB" | jq -r ' ["Bid", "Ask", "Last"], (.result | [.Bid, .Ask, .Last]) | @tsv' | awk -F '\t' '{print ($1=="Bid" ? $1 : sprintf("%.8f",$1)) "\t" ($2=="Ask" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Last" ? $3 : sprintf("%.8f",$3))}' | column -t -s $'\t'
```

___
#### Get Market Summaries ####
Used to get the last 24 hour summary of all active markets.

basic command
```
curl -s "https://bittrex.com/api/v1.1/public/getmarketsummaries"
```

with pretty json response
```
curl -s "https://bittrex.com/api/v1.1/public/getmarketsummaries" | jq -r
```

Table format output
```
curl -s "https://bittrex.com/api/v1.1/public/getmarketsummaries" | \
jq -r ' 
["MarketName", "High", "Low", "Volume", "Last", "BaseVolume", "TimeStamp", "Bid", "Ask", "OpenBuyOrders", "OpenSellOrders", "PrevDay", "Created", "DisplayMarketName"], (.result[] | 
[.MarketName, .High, .Low, .Volume, .Last, .BaseVolume, .TimeStamp, .Bid, .Ask, .OpenBuyOrders, .OpenSellOrders, .PrevDay, .Created, .DisplayMarketName]) | @tsv' | \
awk -F '\t' '{print $1 "\t" ($2=="High" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Low" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Volume" ? $4 : sprintf("%.8f",$4)) "\t" ($5=="Last" ? $5 : sprintf("%.8f",$5)) "\t" ($6=="BaseVolume" ? $2 : sprintf("%.8f",$2)) "\t" $7 "\t" ($8=="Bid" ? $8 : sprintf("%.8f",$8)) "\t" ($9=="Ask" ? $9 : sprintf("%.8f",$9)) "\t" $10 "\t" $11 "\t" ($12=="PrevDay" ? $12 : sprintf("%.8f",$12)) "\t" $13 "\t" $14 "\t" }' | \
column -t -s $'\t'
```

Table format output one liner
```
curl -s "https://bittrex.com/api/v1.1/public/getmarketsummaries" | jq -r '["MarketName", "High", "Low", "Volume", "Last", "BaseVolume", "TimeStamp", "Bid", "Ask", "OpenBuyOrders", "OpenSellOrders", "PrevDay", "Created", "DisplayMarketName"], (.result[] | [.MarketName, .High, .Low, .Volume, .Last, .BaseVolume, .TimeStamp, .Bid, .Ask, .OpenBuyOrders, .OpenSellOrders, .PrevDay, .Created, .DisplayMarketName]) | @tsv' | awk -F '\t' '{print $1 "\t" ($2=="High" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Low" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Volume" ? $4 : sprintf("%.8f",$4)) "\t" ($5=="Last" ? $5 : sprintf("%.8f",$5)) "\t" ($6=="BaseVolume" ? $2 : sprintf("%.8f",$2)) "\t" $7 "\t" ($8=="Bid" ? $8 : sprintf("%.8f",$8)) "\t" ($9=="Ask" ? $9 : sprintf("%.8f",$9)) "\t" $10 "\t" $11 "\t" ($12=="PrevDay" ? $12 : sprintf("%.8f",$12)) "\t" $13 "\t" $14 "\t" }' | column -t -s $'\t'
```

___
#### Get Market Summary ####
Used to get the last 24 hour summary of a specific market.

basic command
```
curl -s "https://bittrex.com/api/v1.1/public/getmarketsummary?market=BTC-DGB"
```

with pretty json response
```
curl -s "https://bittrex.com/api/v1.1/public/getmarketsummary?market=BTC-DGB" | jq -r
```

Table format output
```
curl -s "https://bittrex.com/api/v1.1/public/getmarketsummary?market=BTC-DGB" | \
jq -r ' 
["MarketName", "High", "Low", "Volume", "Last", "BaseVolume", "TimeStamp", "Bid", "Ask", "OpenBuyOrders", "OpenSellOrders", "PrevDay", "Created", "DisplayMarketName"], (.result[] | 
[.MarketName, .High, .Low, .Volume, .Last, .BaseVolume, .TimeStamp, .Bid, .Ask, .OpenBuyOrders, .OpenSellOrders, .PrevDay, .Created, .DisplayMarketName]) | @tsv' | \
awk -F '\t' '{print $1 "\t" ($2=="High" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Low" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Volume" ? $4 : sprintf("%.8f",$4)) "\t" ($5=="Last" ? $5 : sprintf("%.8f",$5)) "\t" ($6=="BaseVolume" ? $2 : sprintf("%.8f",$2)) "\t" $7 "\t" ($8=="Bid" ? $8 : sprintf("%.8f",$8)) "\t" ($9=="Ask" ? $9 : sprintf("%.8f",$9)) "\t" $10 "\t" $11 "\t" ($12=="PrevDay" ? $12 : sprintf("%.8f",$12)) "\t" $13 "\t" $14 "\t" }' | \
column -t -s $'\t'
```

Table format output one liner
```
curl -s "https://bittrex.com/api/v1.1/public/getmarketsummary?market=BTC-DGB" | jq -r '["MarketName", "High", "Low", "Volume", "Last", "BaseVolume", "TimeStamp", "Bid", "Ask", "OpenBuyOrders", "OpenSellOrders", "PrevDay", "Created", "DisplayMarketName"], (.result[] | [.MarketName, .High, .Low, .Volume, .Last, .BaseVolume, .TimeStamp, .Bid, .Ask, .OpenBuyOrders, .OpenSellOrders, .PrevDay, .Created, .DisplayMarketName]) | @tsv' | awk -F '\t' '{print $1 "\t" ($2=="High" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Low" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Volume" ? $4 : sprintf("%.8f",$4)) "\t" ($5=="Last" ? $5 : sprintf("%.8f",$5)) "\t" ($6=="BaseVolume" ? $2 : sprintf("%.8f",$2)) "\t" $7 "\t" ($8=="Bid" ? $8 : sprintf("%.8f",$8)) "\t" ($9=="Ask" ? $9 : sprintf("%.8f",$9)) "\t" $10 "\t" $11 "\t" ($12=="PrevDay" ? $12 : sprintf("%.8f",$12)) "\t" $13 "\t" $14 "\t" }' | column -t -s $'\t'
```

___
#### Get Order book ####
Used to get retrieve the orderbook for a given market.

basic command
```
curl -s "https://bittrex.com/api/v1.1/public/getorderbook?market=BTC-DGB&type=both"
```

with pretty json response
```
curl -s "https://bittrex.com/api/v1.1/public/getorderbook?market=BTC-DGB&type=both" | jq -r
```

Table format output
```
curl -s "https://bittrex.com/api/v1.1/public/getorderbook?market=BTC-DGB&type=both" | \
jq -r ' 
["Type", "Quantity", "Rate"], (.result | 
keys[] as $k | (.[$k][] | [$k, .Quantity, .Rate])) | @tsv' | \
awk -F '\t' '{print $1 "\t" ($2=="Quantity" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Rate" ? $3 : sprintf("%.8f",$3)) }' | \
column -t -s $'\t'
```

Table format output one liner
```
curl -s "https://bittrex.com/api/v1.1/public/getorderbook?market=BTC-DGB&type=both" | jq -r '["Type", "Quantity", "Rate"], (.result | keys[] as $k | (.[$k][] | [$k, .Quantity, .Rate])) | @tsv' | awk -F '\t' '{print $1 "\t" ($2=="Quantity" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Rate" ? $3 : sprintf("%.8f",$3)) }' | column -t -s $'\t'
```

___
#### Get Market History ####
Used to get the last 24 hour summary of a specific market.

basic command
```
curl -s "https://bittrex.com/api/v1.1/public/getmarkethistory?market=BTC-DGB"
```

with pretty json response
```
curl -s "https://bittrex.com/api/v1.1/public/getmarkethistory?market=BTC-DGB" | jq -r
```

Table format output
```
curl -s "https://bittrex.com/api/v1.1/public/getmarkethistory?market=BTC-DGB" | \
jq -r ' 
["Id", "TimeStamp", "Quantity", "Price", "Total", "FillType", "OrderType"], (.result[] | 
[.Id, .TimeStamp, .Quantity, .Price, .Total, .FillType, .OrderType]) | @tsv' | \
awk -F '\t' '{print $1 "\t" $2 "\t" ($3=="Quantity" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Price" ? $4 : sprintf("%.8f",$4)) "\t" ($5=="Total" ? $5 : sprintf("%.8f",$5)) "\t" $6 "\t" $7 "\t" }' | \
column -t -s $'\t'
```

Table format output one liner
```
curl -s "https://bittrex.com/api/v1.1/public/getmarkethistory?market=BTC-DGB" | jq -r '["Id", "TimeStamp", "Quantity", "Price", "Total", "FillType", "OrderType"], (.result[] | [.Id, .TimeStamp, .Quantity, .Price, .Total, .FillType, .OrderType]) | @tsv' | awk -F '\t' '{print $1 "\t" $2 "\t" ($3=="Quantity" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Price" ? $4 : sprintf("%.8f",$4)) "\t" ($5=="Total" ? $5 : sprintf("%.8f",$5)) "\t" $6 "\t" $7 "\t" }' | column -t -s $'\t'
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


>TODO
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
Used to retrieve all balances from your account.

basic command
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalances?apikey=$BITTREX_API_KEY&nonce=$NONCE"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" -s $URL

```

basic command one liner
```
NONCE=$(date +%s) && URL="https://bittrex.com/api/v1.1/account/getbalances?apikey=$BITTREX_API_KEY&nonce=$NONCE" && API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET) && curl -H "apisign: $API_SIGN" -s $URL
```

with pretty json response
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalances?apikey=$BITTREX_API_KEY&nonce=$NONCE"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" -s $URL | jq -r

```

with pretty json response one liner
```
NONCE=$(date +%s) && URL="https://bittrex.com/api/v1.1/account/getbalances?apikey=$BITTREX_API_KEY&nonce=$NONCE" && API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET) && curl -H "apisign: $API_SIGN" -s $URL | jq -r
```

Table format output
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalances?apikey=$BITTREX_API_KEY&nonce=$NONCE"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" \
-s $URL | \
jq -r ' ["Currency", "Balance", "Available", "Pending", "CryptoAddress"], (.result[] | select(.Balance > 0) | [.Currency, .Balance, .Available, .Pending, .CryptoAddress]) | @tsv' | \
awk -F '\t' '{print $1 "\t" ($2=="Balance" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Available" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Pending" ? $4 : sprintf("%.8f",$4)) "\t" $5}' | \
column -t -s $'\t'

```

Table format output one liner
```
NONCE=$(date +%s) && URL="https://bittrex.com/api/v1.1/account/getbalances?apikey=$BITTREX_API_KEY&nonce=$NONCE" && API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET) && curl -H "apisign: $API_SIGN" -s $URL | jq -r ' ["Currency", "Balance", "Available", "Pending", "CryptoAddress"], (.result[] | select(.Balance > 0) | [.Currency, .Balance, .Available, .Pending, .CryptoAddress]) | @tsv' | awk -F '\t' '{print $1 "\t" ($2=="Balance" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Available" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Pending" ? $4 : sprintf("%.8f",$4)) "\t" $5}' | column -t -s $'\t'
```

___
#### Get Balance ####
Used to retrieve the balance from your account for a specific currency.

basic command
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalance?apikey=$BITTREX_API_KEY&nonce=$NONCE&currency=DGB"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" -s $URL

```

basic command one liner
```
NONCE=$(date +%s) && URL="https://bittrex.com/api/v1.1/account/getbalance?apikey=$BITTREX_API_KEY&nonce=$NONCE&currency=DGB" && API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET) && curl -H "apisign: $API_SIGN" -s $URL
```

with pretty json response
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalance?apikey=$BITTREX_API_KEY&nonce=$NONCE&currency=DGB"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" -s $URL | jq -r

```

with pretty json response one liner
```
NONCE=$(date +%s) && URL="https://bittrex.com/api/v1.1/account/getbalance?apikey=$BITTREX_API_KEY&nonce=$NONCE&currency=DGB" && API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET) && curl -H "apisign: $API_SIGN" -s $URL | jq -r
```

Table format output
```
NONCE=$(date +%s)
URL="https://bittrex.com/api/v1.1/account/getbalance?apikey=$BITTREX_API_KEY&nonce=$NONCE&currency=DGB"
API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET)
curl -H "apisign: $API_SIGN" \
-s $URL | \
jq -r ' ["Currency", "Balance", "Available", "Pending", "CryptoAddress", "Requested", "Uuid"], (.result | [.Currency, .Balance, .Available, .Pending, .CryptoAddress, .Requested, .Uuid]) | @tsv' | \
awk -F '\t' '{print $1 "\t" ($2=="Balance" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Available" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Pending" ? $4 : sprintf("%.8f",$4)) "\t" $5 "\t" $6 "\t" $7}' | \
column -t -s $'\t'

```

Table format output one liner
```
NONCE=$(date +%s) && URL="https://bittrex.com/api/v1.1/account/getbalance?apikey=$BITTREX_API_KEY&nonce=$NONCE&currency=DGB" && API_SIGN=$(echo -n $URL | openssl sha512 -hmac $BITTREX_API_SECRET) && curl -H "apisign: $API_SIGN" -s $URL | jq -r ' ["Currency", "Balance", "Available", "Pending", "CryptoAddress", "Requested", "Uuid"], (.result | [.Currency, .Balance, .Available, .Pending, .CryptoAddress, .Requested, .Uuid]) | @tsv' | awk -F '\t' '{print $1 "\t" ($2=="Balance" ? $2 : sprintf("%.8f",$2)) "\t" ($3=="Available" ? $3 : sprintf("%.8f",$3)) "\t" ($4=="Pending" ? $4 : sprintf("%.8f",$4)) "\t" $5 "\t" $6 "\t" $7}' | column -t -s $'\t'
```