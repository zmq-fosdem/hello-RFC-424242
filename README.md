###ZMQ FOSDEM RFC

Let`s rock!

# Server workflow
1. server should bind to port 6666 with REP socket
2. server receives a message with a single frame
3. If message saying 'Hello' server replies with single frames with 'Hello World'
4. Otherwise server reply with 'Error'

# Cient workflow
1. client connects to tcp://192.168.43.186:6666 with REQ with socket
2. client send a message with a single frame 'Hello'
3. client wait for server response
