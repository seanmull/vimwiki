
## Jargon
1. Producing: a program that sends messages
2. Queue: a postbox that lives in rabbitMQ
3. Consuming: a program that waits to recieve messages

## Steps to create a producer
1. Connect to rabbitMQ server
2. Create a channel
3. Declare a queue we want to send to
4.  We give it a name that must match what is requested from the consumer
5. Send message to queue
6. Close the connection and exit

## Steps to create a consumer
Similar to producer only we consume messages and listen for any other messages

## RPC pattern

But what if we need to run a function on a remote computer 
and wait for the result? Well, that's a different story. This 
pattern is commonly known as Remote Procedure Call or RPC.

Simple RPC implementation pattern

C  -----> rpc_queue ------> S
|                           I 
--------- reply_to  <--------

### message properties
- persistant - true or false
- content-type - describes the type of encoding.
- reply_to - commonly used to name the callback queue
- correlation_id - used to correlate RPC responces to requests

1. Client starts up.
2. Rpc queue is created.
3. Client sends message to rpc_queue this message has two properties reply_to and correlation id
4. The server (RPC worker) waits for requests from the rpc_queue if it see one it will respond to the reply to queue
5. The client waits for a responce on the reply to queue.  If it matches the correlationId from the reply it returns the response
from the application.

## Pub sub model

