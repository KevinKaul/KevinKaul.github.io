---
title: "Word Scoring"
weight: 2
---

> wss://api.xxxxx.com/zh-cmn-Hans-CN/word
## Limit

- send audio up to 20 seconds long 
- reference text up to 50 characters.

## Parameter

| **field** | **type** | **defaults** | **remark**                                                                                         |
|:----------|:---------|:-------------|:---------------------------------------------------------------------------------------------------|
| mode      | string   | required     | word                                                                                               |
| refText   | string   | required     | reference text <br />Reference text support [Chinese special label format](datadict/annotation-zh) |

> [!EXAMPLE] Examples
>
> 

```json
{
  "mode":"word",
  "refText":"明天 明儿"
}
```

## Evaluation Results

- [A complete example of the JSON response result](mode/zh-basic/word-result)

| **field**      | **type**         | **remark**                                                                                                                        |
|:---------------|:-----------------|:----------------------------------------------------------------------------------------------------------------------------------|
| evalId         | string           | evalId                                                                                                                            |
| timestamp      | integer          | task timestamp                                                                                                                    |
|~~attachAudioUrl~~       | string           | audio storage url (this field is only returned when the question type parameter `attachAudioUrl=true`)                                  |
| **audioInfo**  | **dict**         | [Audio Quality Information](mode/common)                                                                                          |
| refText        | string           | reference text                                                                                                                    |
| pinyin         | string           | pinyin transcription of the corresponding reference text (with tones)                                                             |
| overall        | double           | total score (range determined by a point system)<br/>combines the toneless pronunciation of syllables (phn) and tones (toneScore) |
| phn            | double           | pronunciation accuracy without tones (range determined by a point system)                                                         |
| toneScore      | double           | overall tone score (range determined by point system)                                                                             |
| waveTime       | integer          | actual recording duration (ms)                                                                                                    |
| startTime      | integer          | the starting reading position in a recording (ms)                                                                                 |
| endTime        | integer          | the ending reading position in a recording (ms)                                                                                   |
| **characters** | **list\<dict\>** | **array of characters info objects (👇)**                                                                                         |

### characters

| **field**       | **type**          | **remark**                                                                                                                        |
|:----------------|:------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| refText         | string            | reference text                                                                                                                    |
| pinyin          | string            | pinyin transcription of the corresponding reference text (without tones)                                                          |
| overall         | double            | total score (range determined by a point system)<br/>combines the toneless pronunciation of syllables (phn) and tones (toneScore) |
| phn             | double            | pronunciation accuracy without tones (range determined by a point system)                                                         |
| toneRef         | integer           | standard tones (0 to 4 for soft, one to four tones respectively)                                                                  |
| toneConfidence  | list\<integer>    | tone confidence level (range 0 to 100, elements in order: soft, one to four)                                                      |
| toneScore       | double            | overall tone score (range determined by point system)                                                                             |
| erRef           | int               | codified sound labels (1 means it should be pronounced, 0 means it should not be pronounced/not checked)                          |
| erScore         | int               | score for paedophones (1 indicates actual agreement with label, 0 indicates actual inconsistency with label/no check)             |
| type            | string            | [word type](datadict/other)                                                                                                       |
| startTime       | integer           | the starting reading position in a recording (ms)                                                                                 |
| endTime         | integer           | the ending reading position in a recording (ms)                                                                                   |
| **phonemes**    | **list\<dict\>**  | **array of phonemes info objects**                                                                                                |
| ├─ phoneme      | string            | transcription representation of sounds and rhymes                                                                                 |
| ├─ score        | double            | vocalization score (range determined by point system)                                                                             |
| ├─ startTime    | integer           | the starting reading position in a recording (ms)                                                                                 |
| ├─ endTime      | integer           | the ending reading position in a recording (ms)                                                                                   |