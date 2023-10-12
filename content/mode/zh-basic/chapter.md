---
title: "Paragraphs Scoring"
weight: 4
---

> wss://api.xxxxx.com/zh-cmn-Hans-CN/chapter
## Limit

- send audio up to 300 seconds long 
- reference text up to 2000 characters.
- can be set to enable real-time return results   [Evaluation parameters](mode/common.md)

## Parameter

| **field**  | **type**  | **defaults**  | **remark**                                                                                         |
|:-----------|:----------|:--------------|:---------------------------------------------------------------------------------------------------|
| mode       | string    | required      | chapter                                                                                            |
| refText    | string    | required      | reference text <br />Reference text support [Chinese special label format](datadict/annotation-zh) |
| phonemes   | boolean   | false         | whether or not to return consonant vowel information                                               |

> [!EXAMPLE] Examples
>
> 

```json
{
  "mode":"chapter",
  "refText":"我们的明天更美丽！"
}
```

## 1. Evaluation Results

- [A complete example of the JSON response result](mode/zh-basic/chapter-result)

| **field**         | **type**          | **remark**                                                                                       |
|:------------------|:------------------|:-------------------------------------------------------------------------------------------------|
| evalId            | string            | evalId                                                                                           |
| timestamp         | integer           | task timestamp                                                                                   |
|~~attachAudioUrl~~          | string            | audio storage url (this field is only returned when the question type parameter `attachAudioUrl=true`) |
| **audioInfo**     | **dict**          | [Audio Quality Information](mode/common)                                                         |
| refText           | string            | reference text                                                                                   |
| pinyin            | string            | pinyin transcription of the corresponding reference text (with tones)                            |
| overall           | double            | total score (range determined by a point system)                                                 |
| accuracy          | double            | accuracy (range determined by point scale)                                                       |
| fluency           | double            | fluency score (range determined by point scale)                                                  |
| integrity         | double            | completeness (range determined by point scale)                                                   |
| phn               | double            | pronunciation accuracy without tones (range determined by a point system)                        |
| **rhythm**        | **dict**          | **rhythm score object**                                                                          |
| ├─ overall        | double            | rhythm score (range determined by point scale)                                                   |
| ├─ tone           | double            | rising tone score (range determined by point scale)                                              |
| ├─ er             | double            | rising tone score (range determined by point scale)                                              |
| ├─ sense          | double            | meaning group pause score (range determined by point scale)                                      |
| ├─ intonation     | double            | rising tone score (range determined by point scale)                                              |
| ├─ elongation     | double            | extended Tone Score (range determined by point system)                                           |
| waveTime          | integer           | actual recording time（ms）                                                                        |
| startTime         | integer           | the starting reading position in a recording (ms)                                                |
| endTime           | integer           | the ending reading position in a recording (ms)                                                  |
| **sentenceInfo**  | **list\<dict\>**  | **array of sentence info objects (👇)**                                                          |

### sentenceInfo

| **field**                         | **type**          | **remark**                                                                                                                                    |
|:----------------------------------|:------------------|:----------------------------------------------------------------------------------------------------------------------------------------------|
| refText                           | string            | reference text                                                                                                                                |
| overall                           | double            | total single-sentence score (range determined by a point system)                                                                              |
| **fluency**                       | **dict**          | **fluency Score Object**                                                                                                                      |
| ├─ overall                        | double            | fluency score (range determined by point scale)                                                                                               |
| ├─ pause                          | integer           | number of pauses                                                                                                                              |
| ├─ speed                          | integer           | speech rate (0: slow, 1: normal, 2: fast)                                                                                                     |
| **characters**                    | **list\<dict\>**  | **characters information object array**                                                                                                       |
| ├─ refText                        | string            | reference text                                                                                                                                |
| ├─ pinyin                         | string            | pinyin transcription of the corresponding reference text (without tones)                                                                      |
| ├─ overall                        | double            | word overall score (range determined by a point system)<br/>combines the toneless pronunciation of syllables (phn) and tones (toneScore)      |
| ├─ fluency                        | double            | fluency score (range determined by point scale)                                                                                               |
| ├─ phn                            | double            | pronunciation accuracy without tones (range determined by a point system)                                                                     |
| ├─ toneRef                        | integer           | standard tones (0 to 4 for soft, one to four tones respectively)                                                                              |
| ├─ toneScore                      | double            | overall Tone Score (range determined by point system)                                                                                         |
| ├─ toneConfidence                 | list\<integer>    | tone confidence level (range 0 to 100, elements in order: soft, one to four)                                                                  |
| ├─ erRef                          | int               | codified sound labels (1 means it should be pronounced, 0 means it should not be pronounced/not checked)                                      |
| ├─ erScore                        | int               | score for paedophones (1 indicates actual agreement with label, 0 indicates actual inconsistency with label/no check)                         |
| ├─ senseRef【additional】           | integer           | meaning group pause label (1 means it should be a short pause, 2 means it should be a long pause, 0 means it shouldn't be paused/not checked) |
| ├─ senseScore【additional】         | integer           | meaning group pause score (1 indicates actual consistency with labeling, 0 indicates actual inconsistency with labeling/no check)             |
| ├─ intonationRef【additional】      | integer           | raise/lower tone labels (1 means it should be raised, 0 means it should be lowered/not checked)                                               |
| ├─ intonationScore【additional】    | integer           | lift-and-tune score (1 indicates actual agreement with labeling, 0 indicates actual disagreement with labeling/no check)                      |
| ├─ elongationRef【additional】      | integer           | extended tone labels (1 means it should be extended, 0 means it should not be extended/not checked)                                           |
| ├─ elongationScore【additional】    | integer           | extended Tone Score (1 indicates actual consistency with labeling, 0 indicates actual inconsistency with labeling/no check)                   |
| ├─ type                           | string            | [word type](datadict/other)                                                                                                                   |
| ├─ startTime                      | integer           | the starting reading position in a recording (ms)                                                                                             |
| ├─ endTime                        | integer           | the ending reading position in a recording (ms)                                                                                               |
| ├─├─ **phonemes**                 | **list\<dict\>**  | **array of phonemes info objects**                                                                                                            |
| ├─├─ phoneme                      | string            | transcription representation of sounds and rhymes                                                                                             |
| ├─├─ score                        | double            | vocalization score (range determined by point system)                                                                                         |
| ├─├─ startTime                    | integer           | the starting reading position in a recording (ms)                                                                                             |
| ├─├─ endTime                      | integer           | the ending reading position in a recording (ms)                                                                                               |



## 2. Real-time Results

| **field**     | **type**  | **remark**                                                  |
|:--------------|:----------|:------------------------------------------------------------|
| evalId        | string    | evalId                                                      |
| timestamp     | integer   | task timestamp                                              |
| hypothesis    | string    | actual text read                                            |
| **wordInfo**  | **list**  | **word information object array**                           |
| ├─ index      | integer   | the corresponding word sequence number in `params.refText`  |
| ├─ refText    | string    | reference text                                              |
| ├─ score      | double    | word score                                                  |
| ├─ type       | string    | [word type](datadict/other)                                 |
