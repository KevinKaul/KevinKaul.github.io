---
title: "Phoneme Scoring"
weight: 1
---

> wss://api.xxxxx.com/en-US/chapter
## Limit

- send audio up to 20 seconds long 
- reference text up to 100 characters.

## Parameter

| **field** | **type** | **defaults** | **remark**                                                                                                                                                                                                                       |
|:---------|:--------|:------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| mode      | string   | required     | phoneme                                                                                                                                                                                                                          |
| refText   | string   | required     | reference text <br />Only phoneme representation in *SpeechEvalPro* format is supported, see [English Phonetic Symbol Comparison Table](datadict/phoneme) for details. Multiple phonetic symbols are separated by English spaces |

> [!EXAMPLE] Examples
>
> 

```json
{
  "mode":"phoneme",
  "refText":"t iy"
}
```

## Evaluation Results

- [A complete example of the JSON response result](mode/en-basic/phoneme-result)

| **field**     | **type**         | **remark**                                                                                       |
|:--------------|:-----------------|:-------------------------------------------------------------------------------------------------|
| evalId        | string           | evalId                                                                                           |
| timestamp     | integer          | task timestamp                                                                                   |
|~~attachAudioUrl~~      | string           | audio storage url (this field is only returned when the question type parameter `attachAudioUrl=true`) |
| **audioInfo** | **dict**         | [Audio Quality Information](mode/common)                                                         |
| refText       | string           | reference text                                                                                   |
| hypothesis    | string           | actual text read                                                                                 |
| overall       | double           | total score (range determined by scale)                                                          |
| fluency       | double           | fluency score (range determined by point scale)                                                  |
| accuracy      | double           | accuracy (range determined by point scale)                                                       |
| integrity     | double           | completeness (range determined by point scale)                                                   |
| waveTime      | integer          | actual recording time (ms)                                                                       |
| startTime     | integer          | the starting reading position in a recording (ms)                                                |
| endTime       | integer          | the ending reading position in a recording (ms)                                                  |
| **phonemes**  | **list\<dict\>** | **array of phoneme info objects **                                                               |
| ├─ phoneme    | string           | reference text                                                                                   |
| ├─ hypothesis | string           | actual text read（*SpeechEvalPro* format）                                                         |
| ├─ score      | double           | total word score (range determined by point scale)                                               |
| ├─ startTime  | integer          | the starting reading position in a recording (ms)                                                |
| ├─ endTime    | integer          | the ending reading position in a recording (ms)                                                  |
| ├─ type       | string           | [phoneme type](datadict/other)                                                                   |
