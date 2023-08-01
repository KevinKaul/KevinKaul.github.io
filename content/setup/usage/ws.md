---
title: "- 2. Websocket streaming evaluation"
weight: 3
---

## Evaluation flowchart

{{< mermaid >}}
sequenceDiagram
Client->>Server: Establish a connection (Carry the token in the header or in the url)
Server-->>Client: The connection was successful
Client->>Server: StartMessage
Server-->>Client: StartedMessage
loop 
Client->>Server: Send audio data (binary)
Server->>Client: Returns real-time results (if you send startMsg with real-time and sentence or paragraph type)
end
Client->>Server: StopMessage
Server-->>Client:  (Result &&  CompletedMessage) ||  (ErrorMessage &&  CompletedMessage)
{{< /mermaid >}}

### - StartMessage
[Public Parameters](mode/common.md)
> `common` field content is fixed
> 
> `payload` field have required parameters and optional parameters
> 
> `payload.params` Refer to the introduction of each question type 

### - StopMessage
**content is fixed**
```json
{
    "common": {
        "cmd": "stop",
        "api": "speecheval"
    }
}
```

### - Response

####    - Score Result
e.g.
```json
{
    "ack": "result",
    "code": "00000",
    "eof": 1, // The final result is 1, the real-time result is 0
    "evalId": "705452d7-bd98-456d-981f-d461cc97e3f3",
    "msg": "success",
    "timestamp": 1670870100,
    "result": {
      .... // Refer to the introduction of each question type
    },
    "request": { // Your startMsg.payload parameter (with default value)
        "langType": "en-US",
        "format": "pcm",
        "params": {
          "refText": "refText",
          "mode": "sentence"
        }
    }
}

```



####    - ErrorMessage

e.g.
```json
{
    "ack":    "error",
    "code":   "34006",
    "msg":    "app no available times",
    "evalId": "9fb0c0e6-5aad-4028-a6f2-4242072f8cfa"
}

```

#### - WarningMessage

e.g.
```json
{
    "ack":    "warning",
    "code":   "35102",
    "msg":    "audio length exceeded",
    "evalId": "10d817ac-db8b-4f0e-9cbc-d90197b79c72"
}

```
#### - CompletedMessage

e.g.
```json
{
    "ack":    "completed",
    "code":   "00000",
    "msg":    "success",
    "evalId": "10d817ac-db8b-4f0e-9cbc-d90197b79c72"
}

```



### Special instructions
> [!tip] Hint
>
> 1. Regardless of whether the final `score result` is returned, a `Completedmessage` will be returned, and eventually the server will actively close the connection.
> 
> 2. `ErrorMessage` and `score result` do not appear at the same time, they are mutually exclusive.
> 
> 3. `WarningMessage` may appear after sending `startMessage` or after sending `stopMessage`, so attention needs to be paid to determining the return value of `ack` field.