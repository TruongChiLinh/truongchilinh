
Task : 
1. Filter JSON records with symbol == "TSLA" from the file ./transaction-log.txt.
2 .Extract the order_id from the filtered transactions.
3 .Use xargs to iterate over the extracted order_id values.
4 .For each order_id, send a HTTP GET request to https://example.com/api/{order_id} using curl.
5 .Save the response from each request to ./output.txt.
Explan :
jq -r '. | select(.symbol == "TSLA") | .order_id' ./transaction-log.txt | xargs -I {} curl -s "https://example.com/api/{}" >> ./output.txt

jq -r '. | select(.symbol == "TSLA") | .order_id' ./transaction-log.txt

This part uses jq to filter the JSON file ./transaction-log.txt for entries where the symbol field equals "TSLA".
.order_id extracts the order_id from the filtered records.
The -r flag ensures that the output is raw (without quotes around the order_id values).
xargs -I {} curl -s "https://example.com/api/{}" >> ./output.txt

xargs takes each order_id output from the previous jq command and replaces {} with the order_id in the curl command.
curl -s sends a silent HTTP GET request to https://example.com/api/{order_id}, where {order_id} is replaced by the actual order_id.
>> ./output.txt appends the responses from the curl requests into the output.txt file.
Result:
This script will filter out the transactions where the symbol is "TSLA".
It will send GET requests for each order_id and append the responses to output.txt.