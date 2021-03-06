# AutoComplete

 

## Sample Request
``` JSON
{
    "header": {
        "messageId": "afb99815-0004-4530-8581-a4aaffb92904",
        "x-correlationId": "afb99815-0004-4530-8581-a4aaffb92904",
        "x-cliendId": "75010105537365102704845373651050168024",
        "x-connectionId": "8t6GMkJAmgkws6qVAGCL"
    },
    "body":{
        "customer": {
            "id": "08a69bed-cd06-47b8-b759-33b95683aa79"
        },
        "queries":[
            {
                "label":"main",
                "entities":["autocomplete"],
                "query": {
                    "tags":["spain"],
                    "index":"default",
                    "limit":"10"
                }
            },
            {
                "label":"popular",
                "entities":["autocomplete"],
                "query": {
                    "index":"popular",
                    "limit":"10"
                }
            }
        ]
    }
  }

```
Each message MUST be wrapped in the above envelope and MUST contain a few basic fields. 

__Header section:__

see: [https://github.com/numo-labs/schema#base-message-format-envelope](./../schema#base-message-format-envelope)

__Message Section:__ 

* body: the body of the message, data which is allowed to go over the connection between the client and the server
* body.customer: a customer object, as a search always happens for a "customer" we include the customer object, a customer can also be an anonymous user, as shown here above. see [Customer]() Entity for more information.
* body.queries: an array of queries which will be executed by the backend service. Each query will be executed and results will be streamed back, and the correlationId will be extended to the following format: {x-correlationId}#{label} here in this example thus for all responses regarding the first query, _"x-correlationId": "afb99815-0004-4530-8581-a4aaffb92904#main"_, and for the second query _"x-correlationId": "afb99815-0004-4530-8581-a4aaffb92904#alternative"_,

### Related Entities
* AutoComplete               

