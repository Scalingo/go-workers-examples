# Async jobs between Go and Ruby

## Execution

```
go run worker.go &
ruby client.rb
workers: 2014/11/27 22:36:02.666316 processing queue myqueue with 10 workers.
workers: 2014/11/27 22:36:21.715090 myqueue JID-f550915700b61b5c81cf115b start
workers: 2014/11/27 22:36:21.715121 myqueue JID-f550915700b61b5c81cf115b args:  ["hello"]
running task &{0xc20803c058 {"retry":true,"queue":"myqueue","class":"MyGoWorker","args":["hello"],"jid":"f550915700b61b5c81cf115b","enqueued_at":1417124181.7106063}}
workers: 2014/11/27 22:36:21.715466 myqueue JID-f550915700b61b5c81cf115b done: 372.041us
```

```
sidekiq -r ./worker.rb &
go run client.go
2014-11-27T21:37:12.693Z 27168 TID-ou7skmuls MyRubyWorker JID-1b6d81aa565d69f14da6eb83 INFO: start
Hello from Sidekiq: hello
2014-11-27T21:37:12.693Z 27168 TID-ou7skmuls MyRubyWorker JID-1b6d81aa565d69f14da6eb83 INFO: done: 0.0 sec
```

## Libs

### Go

It uses go-workers which is a Sidekiq-compatible tool to run and enqueue
jobs.

### Ruby

Sidekiq gem is used for job management

