---
title: "Paragraphs Scoring"
weight: 4
---

## Limit

- send audio up to 300 seconds long 
- reference text up to 10,000 characters.
- can be set to enable real-time return results [Evaluation parameters](mode/common.md)

## Parameter

| **field** | **type** | **defaults** | **remark**                                                                                         |
|:----------|:---------|:-------------|:---------------------------------------------------------------------------------------------------|
| mode      | string   | required     | chapter                                                                                            |
| refText   | string   | required     | reference text <br />Reference text support [English special label format](datadict/annotation-en) |

example：

```json
{
  "mode":"chapter",
  "refText":"I believe there is a person who brings sunshine into your life. That person may have enough to spread around."
}
```

## 1. Evaluation Results

- [A complete example of the JSON response result](mode/en-basic/chapter-result)

| **field**        | **type**         | **remark**                                                                                       |
|:-----------------|:-----------------|:-------------------------------------------------------------------------------------------------|
| taskId           | string           | taskID                                                                                           |
| timestamp        | integer          | task timestamp                                                                                   |
| audioUrl         | string           | audio storage url (this field is only returned when the question type parameter `audioUrl=true`) |
| **audioInfo**    | **dict**         | [Audio Quality Information](mode/common)                                                         |
| refText          | string           | reference text                                                                                   |
| hypothesis       | string           | actual text read                                                                                 |
| overall          | double           | total score (range determined by scale)                                                          |
| fluency          | double           | fluency score (range determined by point scale)                                                  |
| accuracy         | double           | accuracy (range determined by point scale)                                                       |
| integrity        | double           | completeness (range determined by point scale)                                                   |
| waveTime         | integer          | actual recording time (ms)                                                                       |
| startTime        | integer          | the starting reading position in a recording (ms)                                                |
| endTime          | integer          | the ending reading position in a recording (ms)                                                  |
| **sentenceInfo** | **list\<dict\>** | **array of sentence info objects (👇)**                                                          |

### sentenceInfo

| **field**      | **type**          | **remark**                                                                        |
|:---------------|:------------------|:----------------------------------------------------------------------------------|
| refText        | string            | reference text                                                                    |
| hypothesis     | string            | actual text read                                                                  |
| score          | double            | total score for a single sentence (the range is determined by the scoring system) |
| startTime      | integer           | the starting reading position in a recording (ms)                                 |
| endTime        | integer           | the ending reading position in a recording (ms)                                   |
| **fluency**    | **dict**          | **fluency Score Object**                                                          |
| ├─ overall     | double            | fluency score (range determined by point scale)                                   |
| ├─ pause       | integer           | number of pauses                                                                  |
| ├─ speed       | integer           | speech rate (0: slow, 1: normal, 2: fast)                                         |
| **wordInfo**   | **list\<dict\>**  | **word information object array**                                                 |
| ├─ refText     | string            | reference texts                                                                   |
| ├─ hypothesis  | string            | actual text read                                                                  |
| ├─ score       | double            | total word score (range determined by point scale)                                |
| ├─ startTime   | integer           | the starting reading position in a recording (ms)                                 |
| ├─ endTime     | integer           | the ending reading position in a recording (ms)                                   |
| ├─ type        | string            | [word type](datadict/other)                                                       |

## 2. Real-time Results

| **field**     | **type**  | **remark**                                                  |
|:--------------|:----------|:------------------------------------------------------------|
| taskId        | string    | taskID                                                      |
| timestamp     | integer   | task timestamp                                              |
| hypothesis    | string    | actual text read                                            |
| **wordInfo**  | **list**  | **word information object array**                           |
| ├─ index      | integer   | the corresponding word sequence number in `params.refText`  |
| ├─ refText    | string    | reference text                                              |
| ├─ score      | double    | word score                                                  |
| ├─ type       | string    | [word type](datadict/other)                                 |