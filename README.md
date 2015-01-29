# V2

## Server

* MUST choose a port that SHOULD be random — SERVICE_PORT
* MUST choose a secret — SECRET_RESPONSE

The server MUST run both workflows in parallel.

### Service workflow

* MUST listen on port SERVICE_PORT with a socket of type `router`
* Upon requests, MUST reply with a secret response

### Discovery workflow

* MUST use a socket of type `pub` to publish its LOCATION every second on port 6665
* the LOCATION is defined by the last octet of the server IP and SERVICE_PORT and format MUST be "last_ip_octet:SERVICE_PORT"


## Client

The client MUST start with the "Discovery workflow"

### Discovery workflow

* for every possible last_ip_octet (1-254) the client SHOULD subscribe to topic `discovery` on port 6665
* Upon received messages from subscriptions, the client SHOULD generate the respective ADDRESS from the last_ip_octet and PORT and use it for the "Connect Workflow"

### Connect workflow

1. SHOULD connect to the ADDRESS with a socket of type `dealer`
2. MUST send `"Hello from NICKNAME"` where is the name of the sender.
3. MUST log the reply
4. SHOULD return and continue on the "Discovery workflow"
