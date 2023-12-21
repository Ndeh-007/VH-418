vc418_server
=====

An OTP application

Built with Erlang, this server runs algorithms requested by the client. The server processes these requests and send response back to the client.

## Structure
The server runs on port `8080`, unless its values are in the source code and rebuilt. There is open to request from any host.

## Endpoints
The server has 2 endpoints
`http://localhost:8080/reduce` and `http://localhost:8080/scan` which accepts only get requests with key `nprocs`. Each of these end points call their respective algorithms

## Algorithms
1. Reduce
    - This is a fairly simple reduce. 
    - The values of each process are their process index in the range `1 - N` boundaries included.
    - The combine function is a simple addition
        ```erlang
            %% Reduce Combine Function

            fun (Left, Right) -> Left + Right end.
        ```
    - The algorithm returns the sum of all process values.
2. Scan
    - A fairly Simple scan.
    - Implements Exclusive scan.
        - The Initial accumulator is 0, and initial values are 1 for all processes
        - Is supposed to return an array of sums where each value is the sum of values before it.
    - Implements two combine functions, add and concatenate
        ```erlang
            %% Scan combine functions

            % add
            fun (Left, Right) -> Left + Right end.

            % concatenate
             fun (Left, Right) -> Left ++ Right end.
        ```
    
For each algorithm, events are traced using an event tracer. The data from the tracing is parsed to a json format and sent as a reply to the request made.
the JSON Follows the format
```json
{
    "nprocs": 4,
    "program":"reduce",
    "tree":[
        ...,
        {
        "self": "<0.319.0>",
        "parent": "<0.318.0>",
        "children": []
        },
        ...
    ], 
    "data":[
        ...,
        {
            "type": "event",
            "priority": 80,
            "send_time": 1702418998414,
            "receive_time": 1702418998414,
            "from": "<0.316.0>",
            "to": "<0.318.0>",
            "msg": "At the leaf",
            "data": {
                "action": null,
                "value": 2 // this it the value from the combine function.
            }
        },
        ...
    ]
}

```


Build
-----

    $ rebar3 compile

Launch server
-----

    $ rebar3 shell --apps vc418_server

    or

    $ rebar3 shell 
