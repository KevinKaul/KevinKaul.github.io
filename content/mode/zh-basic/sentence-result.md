---
bookHidden: true
---

# Chinese sentence evaluation question type returns the original result

```json
{
    "accuracy":92.8462142944336,
    "audioInfo":{
        "clip":0,
        "snr":57.8266677856445,
        "tipId":"00000",
        "volume":60.88525390625
    },
    "characters":[
        {
            "endTime":920,
            "erRef":0,
            "erScore":0,
            "fluency":60.3578758239746,
            "overall":96.5647888183594,
            "phn":94.9913635253906,
            "pinyin":"zao",
            "refText":"早",
            "startTime":530,
            "toneConfidence":[
                0,
                0,
                0,
                99,
                1
            ],
            "senseRef":0,
            "senseScore":0,
            "toneRef":3,
            "toneScore":99.9748077392578,
            "intonationRef":0,
            "intonationScore":0,
            "elongationRef":0,
            "elongationScore":0,
            "type":"normal"
        },
        {
            "endTime":1320,
            "erRef":0,
            "erScore":0,
            "fluency":96.701904296875,
            "overall":67.434944152832,
            "phn":70.1153869628906,
            "pinyin":"shang",
            "refText":"上",
            "startTime":920,
            "toneConfidence":[
                43,
                46,
                0,
                0,
                11
            ],
            "senseRef":0,
            "senseScore":0,
            "toneRef":3,
            "toneScore":95.7534942626953,
            "intonationRef":0,
            "intonationScore":0,
            "elongationRef":0,
            "elongationScore":0,
            "type":"normal"
        },
        {
            "endTime":2330,
            "erRef":0,
            "erScore":0,
            "fluency":64.3783416748047,
            "overall":98.4538345336914,
            "phn":99.8040161132812,
            "pinyin":"hao",
            "refText":"好",
            "startTime":1940,
            "toneConfidence":[
                0,
                0,
                6,
                90,
                4
            ],
            "senseRef":0,
            "senseScore":0,
            "toneRef":3,
            "toneScore":95.7534942626953,
            "intonationRef":0,
            "intonationScore":0,
            "elongationRef":0,
            "elongationScore":0,
            "type":"normal"
        }
    ],
    "endTime":2730,
    "fluency":{
        "overall":73.8774719238281,
        "pause":1,
        "speed":0
    },
    "integrity":100,
    "overall":95.6002044677734,
    "phn":92.8462142944336,
    "pinyin":"zao3 shang0 hao3",
    "refText":"早上好。",
    "rhythm":{
        "er":100,
        "overall":95.4380340576172,
        "sense":100,
        "tone":88.5950775146484,
        "intonation":100,
        "elongation":100
    },
    "startTime":530,
    "waveTime":3096

}
```

### Return results in real time

```json
{
    "hypothesis":"早上",
    "wordInfo":[
        {
            "index":0,
            "refText":"早",
            "score":98.2038116455078,
            "type":"normal"
        },
        {
            "index":1,
            "refText":"上",
            "score":98.2038116455078,
            "type":"normal"
        }
    ],
    "evalId":"b1195999-1446-4a71-a671-699c2ceb607f",
    "timestamp":1670465928
}
```
