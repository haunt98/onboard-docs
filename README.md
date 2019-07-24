# Stateful and Stateless

## Key difference

Stateless app don't store data.

Stateful app require backing storage, persistent storage that will survive service restarts.

## Stateless

- Process requests based only on information relayed with each request not related with earlier requests.

- Different requests can be processed by different servers.

## Stateful

- Databases

- Transactions

- Process requests based on information relayed with each request and information stored from earlier requests.

- Same server process all requests linked to same state information, or state information needs to be shared with all servers.

## How do Stateful apps maintain state information

- Transaction affinity: load distribution knows transaction's existence and direct all requests within transaction's scope to same server.

- Session affinity: load distribution knows client session's existence and direct all requests of client session to same server.

- Server affinity: load distribution knows multiple server might be accptable -> choose a best server.

- Distributed systems: both server affinity and session affinity -> directing client requests to server's cluster members.

- Workload management service: both server affinity and transaction affinity.

## Example

Stateful apps store state from client request on the server itself and use that state for future requests.

Stateful apps don't need to make a second call to DB as session stored on server itself.
**Drawbacks**: load balancer with 2 servers behind, first request to login go to server 1 and second request might go to server 2, server 1 know user is logged in but server 2 is not.

Stateless apps don't store any state on the server, they use DB instead. DB is Stateful - persistent storage

State generated and stored somewhere:

- Stored on server side -> generate session -> Stateful app

- Stored on client side -> generate data for further requests -> Stateless app

## Why need Stateless apps

There is no relationship between requests.

Client does not wait for synchronization from the server -> faster.

## How Stateless apps work

App is dependent on DB because it doesn't store any state in its memory or disks.

In Stateful app, each server remembers users's state which logged in to, load balancer need to config to routing requests to same server as earlier requests -> not load balancer anymore

In Stateless app, load balancer doesn't need to worry about routing requests -> truly load balancer
