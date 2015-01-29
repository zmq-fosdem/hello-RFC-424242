###ZMQ FOSDEM RFC

Let`s rock!

# Server workflow
1. server should bind to port 6666 with REP socket, or a ROUTER socket (then the server will receive a routing ID frame plus an empty delimiter frame before each Hello frame).
2. server receives a message with a single frame (if REP socket) or three frames (if ROUTER socket).
3. If message saying 'Hello' server replies with a single frame with its name, or three frames (routing ID, empty delimiter frame, name frame).
4. Otherwise server reply with 'Error' (with routing ID and empty delimiter, for ROUTER sockets).

# Cient workflow
1. client connects to tcp://192.168.43.186:6666 with REQ socket, or DEALER socket (then the client must always send an empty frame at the start of each message, to emulate the REQ socket).
2. client send a message with a single frame 'Hello' (if REQ socket) or two frames (if DEALER socket)
3. client wait for server response


#RFC 2

## Server workflow I
* server should listen on port with router socket
* the server should reply with a secret info

## Server workflow II
* server should use pub socket to publish the server address (from workflow I) every second on port 6665
* the beacon format should be "last_ip_octet:port"


## Cient workflow I
* client subscribe to topic ```discovery``` on port 6665
* on every received message client should execute workflow II

## Client workflow II
* client should connect to server using dealer socket
* client should send 'Hello' and receive the secret
