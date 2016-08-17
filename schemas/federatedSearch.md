# Federeated Search Requests

This section describes how the client can execute federated search requests. The service can return package, hotel, flight products. 

## Sample Request
``` JSON
{
  "header": {
    "messageId": "afb99815-0004-4530-8581-a4aaffb92904",
    "messageType": "federatedSearch.v1",
    "x-correlationId": "afb99815-0004-4530-8581-a4aaffb92904",
    "x-cliendId": "75010105537365102704845373651050168024",
    "x-connectionId": "8t6GMkJAmgkws6qVAGCL"
  },
  "message": {
    "body":{
        "channel" : {
            "id":"uk:oneweb:v1",
        },
        "customer": {
            "id": "08a69bed-cd06-47b8-b759-33b95683aa79"
        },
        "queries":[
            {
                "label":"main",
                "tags":["hotel:mhid.ao4f1g5","hotel:mhid.amase2r"],
                "ranker":"default",
                "limit":"100",
                "entities":["package","tile","hotel"]
            },
            {
                "label":"alternative",
                "index":"popular",
                "limit":10,
                "entities":["hotel"]
            }
        ]
    }
  }
}
```
Each message MUST be wrapped in the above envelope and MUST contain a few basic fields. 

__Header section:__

see: [https://github.com/numo-labs/schema#base-message-format-envelope](./../schema#base-message-format-envelope)

__Message Section:__ 

* body: the body of the message, data which is allowed to go over the connection between the client and the server
* body.channel: a channel object to determine the scope of this message, messages are routed / channel. Sample channels could be oneweb uk, retail uk, ... see [Channel]() Entity for more information.
* body.customer: a customer object, as a search always happens for a "customer" we include the customer object, a customer can also be an anonymous user, as shown here above. see [Customer]() Entity for more information.
* body.queries: an array of queries which will be executed by the backend service. Each query will be executed and results will be streamed back, and the correlationId will be extended to the following format: {x-correlationId}#{label} here in this example thus for all responses regarding the first query, _"x-correlationId": "afb99815-0004-4530-8581-a4aaffb92904#main"_, and for the second query _"x-correlationId": "afb99815-0004-4530-8581-a4aaffb92904#alternative"_,

### Related Entities
* Channel               
* Customer
* Package
* Tile
* Hotel

