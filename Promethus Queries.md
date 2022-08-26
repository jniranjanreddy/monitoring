## mathers
```
Equality matchers  - ex process_cpu_seconds_total{job="node_exporter"}

Negative Equality Matcher - Ex: process_cpu_seconds_total{job!="node_exporter"}

Regular Expression - Ex: prometheus_http_requests_total{'handler=~"/api.*"'}

Negative Reqular Expression Ex:  prometheus_http_requests_total{'handler!~"/api.*"'}
```



scrape_duration_seconds :- will get all the data that is scraped.

scrape_duration_seconds{InstanceType="m5.large"} :- will get all the data wil instance m5.large

scrape_duration_seconds{AccountID="<AccountNumber>"} :- To get all instance in the Account  XXXX 
Note:- To get  the count check for the  "Total time series on left corner top "


#Memory Available
node_memory_MemAvailable_bytes{AccountID="21008XXXXX"}/1000/1000

#Another method
node_memory_MemAvailable_bytes/1024/1024

#Syntax to intergrate with labels
some_key {some_label="THATLABEL",another_label="THISLABEL"} [#value]

#Example
node_network_receive_bytes_total{AccountID="210083XXXX",InstanceType="t2.medium"}

#or condition
node_network_receive_bytes_total{device=~"eth0|lo",AccountID="2100XXXXX",InstanceType="t2.medium"}

Operators Available 
- and
- or
- unless


Examples:- greater than

node_cpu_seconds_total > 500


Aggregation Operator
- sum
- min
- max
- avg
- count




#To get the active nodes
sum(up)

#To get all the inactive nodes.
count( up == 0)

#TO get the sum to active nodes by Account ID
sum(up) by (AccountID)

#Topk operator to get top N active instances
topk(2,sum(up) by (AccountID))

Here 2 is the top 2 

#BottomK is the operator that CPU spends least N values
bottomk(2,sum(up) by (AccountID))

#min and Max
max(node_cpu_second_total)

Rate()
Outputs the rate at which particular counter is increasing 


Metric 
node_uname_info wuill get you kernel.






Queries worked for AWS metrics
-----------------------------------
sum(up)  -- instance that are up
count( up == 0) -- instance that are down.
100 * (1 - avg by(instance)(irate(node_cpu_seconds_total{mode='idle'}[5m]))) --- for cpu
((node_memory_MemTotal_bytes - (node_memory_Cached_bytes + node_memory_Slab_bytes) - node_memory_MemFree_bytes) / (node_memory_MemTotal_bytes )) * 100 -- for Memory
node_load1 -- server load
