---
title: "Public Parameters"
weight: -2
---


## 1. Evaluation parameters

### StartMessage
> `common` field content is fixed
>
> `payload` field have required parameters and optional parameters
>
> `payload.params` Refer to the introduction of each question type

| field           | type    | remark                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | defaults |
| :-------------- | :------ |:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| :------- |
| langType        | enum    | english：en-US<br />chinese：zh-cmn-Hans-CN                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | required | | required |
| connectTimeout  | int     | Connection 、Heartbeat timeout (seconds), range: 5-60.                                                                                                                                                                                                                                                                                                                                                                                                                                                     | 15       |
| responseTimeout | int     | Response timeout (seconds), range: 5-60.                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | 15       |
| rank           | int     | Scoring scale, range: 1-100                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | 100      |
| precision           | float   | Score ad:justment coefficient, range: 0.8-1.5 (up to 3 decimal places)<br/>The function of this coefficient is to adjust up or down the score between 30 and 90 (percentage system), and the scores in other ranges remain unchanged<br/>When `precision` >1.0, the score is raised, the closer to 75 points, the higher the adjustment degree<br/>When `precision` <1.0, the score is lowered, the closer to 75 points, the higher the adjustment degree<br/> When `precision` =1.0, no score adjustment | 1.0      |
| ~~attachAudioUrl~~        | boolean | Deprecated ~~Whether to return the audio download URL<br />The audio is kept for about 10 days by default. If you need to save it permanently, it is recommended that the access party download it to its own server~~                                                                                                                                                                                                                                                                                              | false    |
| realtime        | boolean | Whether to return the result in real time<br>Only Chinese/English sentence, chapter question types are supported.                                                                                                                                                                                                                                                                                                                                                                                         | false    |

> [!EXAMPLE] Examples
>
> 
```json
{
    "common": {
        "api":"speecheval",
        "cmd": "start"
    },
    "payload": {
        "langType": "en-US",
        "format": "pcm",
        "params": {
            "refText": "Yes(t:1)?",
            "mode": "sentence"
        }
    }
}
```

### StopMessage
```json
{
    "common": {
        "cmd": "stop",
        "api": "speecheval"
    }
}

```

## 2. Public parameters in the response
### audioInfo（Audio Quality Information）field

| params  | type    | remark                                                                                                                                                       |
|:--------|:--------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| snr     | double  | Signal-to-noise precision, the higher the value, the clearer it is (-20～+60dB)<br/>When this parameter affects the score, the corresponding `tipId`  will be set |
| clip    | double  | The volume is too loud, truncation occurs (0~1)<br/>When this parameter affects the score, the corresponding `tipId`  will be set                            |
| volume  | double  | Recording volume (0~90dB)                                                                                                                                    |
| tipId   | string  | Audio Quality Type ID                                                                                                                                        |

**tipId introduction**

| tipId  | description                                                                                               | remark                                                    |
|:-------|:----------------------------------------------------------------------------------------------------------|:----------------------------------------------------------|
| 00000  | normal audio                                                                                              | None                                                      |
| 90001  | The user's pronunciation is incomplete, such as "good morning", may only say "good"                       | Can prompt incomplete pronunciation                       |
| 90002  | The recognition is incomplete. In this case, most of them are silent and the audio is short.              | Can prompt incomplete pronunciation                       |
| 90003  | Low volume, probably located too far away                                                                 | Can advise users to adjust microphone distance or volume  |
| 90004  | Audio clipped, maybe too close                                                                            | Can advise users to adjust microphone distance or volume  |
| 90005  | Poor audio quality (low signal-to-noise precision caused by noisy recording environment or indistinct speech) | It can prompt the user that the voice is not obvious      |