# mau5

Just started a Riak -> ElasticSearch River.

## Idea:

1) Proxy requests through mau5 to Riak.
2) On a confirmed PUT/POST/DELETE, read from Riak.
  a) Read could eventually happen through Montage for sibling resolution when 
  multi=true (ES doesn't support siblings)
3) Send resolved sibling to ES for indexing.

## So Far:

Proxy to Riak works.

## TODO:

1) Read from Riak and send to ES
2) Make Read/Write urls configurable
3) Allow config files and command line args to start process
4) Implement Message Queue for guarenteed processing of successful Riak inserts

## Run:

`./bin/mau5`

`curl localhost:3500 -XPUT -v -d somedata="thisis" -H "Content-Type: application/json"`
