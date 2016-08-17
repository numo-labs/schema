# schema
JSON schema definitions for numo-labs.

## Federated search

For Federated search, we will use streaming services. These streaming asynchronous services will pass messages between client and server and between the different micro-services in the federated search stack. 

### Base Message format (envelope)

``` JSON
{
  "header": {
    "messageId": "afb99815-0004-4530-8581-a4aaffb92904",
    "messageType": "package.v1",
    "x-correlationId": "afb99815-0004-4530-8581-a4aaffb92904",
    "x-cliendId": "75010105537365102704845373651050168024",
    "x-connectionId": "8t6GMkJAmgkws6qVAGCL"
  },
  "message": {
    "body":{
        "foo":"a"
    },
    "internal":{
        "bar":"b"
    }
  }
}
```
Each message MUST be wrapped in the above envelope and MUST contain a few basic fields. 

__Header section:__

* messageId: (Required) A client side generated unique id.
* messageType: (Required) Type of message here for exapmple a searchRequest message.
* x-correlationId: (Optional) A client side generated unique id and through the stack forwarded message, which can be used so correlated returned messages back to the request.
* x-clientId: (Optional) In case of a request, we need a client Id to be able to send messages back to the correct client
* x-connectionId: (Optional) In case of a request, we need a connection Id to be able to send messages back to the correct connection for the client, we assume the client can have multiple connections open to the same server. 

__Message Section:__ 

* body: the body of the message, data which is allowed to go over the connection between the client and the server
* internal: this part of the message is for internal (server side only use) and will never be exposed to the client, this can be extremely useful if you only want to send a partial result to the client, but want to archive the full response. In our example "bar":"b" will never been send to the client. 

## Federated Search Messages

### Requests
* [Federated Search Message](./schemas/federatedSearch.md)

