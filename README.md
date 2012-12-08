# mau5

Just started a Riak -> ElasticSearch River.

## Idea:

1. Proxy requests through mau5 to Riak.
2. On a confirmed PUT/POST/DELETE, read from Riak.
  * Read could eventually happen through Montage for sibling resolution when 
  multi=true (ES doesn't support siblings)
3. Send resolved sibling to ES for indexing.

## So Far:

Proxy to Riak works.
A PUT with content-type "application/json" results in the data being updated in ES

## TODO:

1. Read from Riak and send to ES
2. Make Read/Write urls configurable
3. Allow config files and command line args to start process
4. Implement Message Queue for guarenteed processing of successful Riak inserts

## Run:

`./bin/mau5`

Assumptions:
* Riak running on port 10018
* ElasticSearch running on port 9200

##### Insert Data

`bash
    curl 127.0.0.1:3500/riak/test/1 -XPUT -d '{somedata:"testing, but with prizes!"}' -v -H "Content-Type: application/json"
    curl 127.0.0.1:3500/riak/test/1 -XPUT -d '{somedata:"This is some testing content"}' -v -H "Content-Type: application/json"
`
##### Query ES

`bash
    curl localhost:9200/riak/test/_search?q=somedata:prizes
`

