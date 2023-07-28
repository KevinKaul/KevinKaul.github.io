---
title: "Sentence Scoring"
weight: 3
---


## Limit

- send audio up to 40 seconds long 
- reference text up to 300 characters.
- can be set to enable real-time return results [Evaluation parameters](mode/common.md)

## Parameter

| **field** | **type** | **defaults** | **remark**                                                                                         |
|:----------|:---------|:-------------|:---------------------------------------------------------------------------------------------------|
| mode      | string   | required     | sentence                                                                                           |
| refText   | string   | required     | reference text <br />Reference text support [English special label format](datadict/annotation-en) |

example：

```json
{
  "mode":"sentence",
  "refText":"Hi there."
}
```

## 1. Evaluation Results

- [A complete example of the JSON response result](mode/en-basic/sentence-result)

| **field**      | **type**          | **remark**                                                                                       |
|:---------------|:------------------|:-------------------------------------------------------------------------------------------------|
| taskId         | string            | taskID                                                                                           |
| timestamp      | integer           | task timestamp                                                                                   |
| audioUrl       | string            | audio storage url (this field is only returned when the question type parameter `audioUrl=true`) |
| **audioInfo**  | **dict**          | [Audio Quality Information](mode/common)                                                         |
| refText        | string            | reference text                                                                                   |
| hypothesis     | string            | actual text read                                                                                 |
| overall        | double            | total score (range determined by scale)                                                          |
| **fluency**    | **dict**          | **fluency score Object**                                                                         |
| ├─ overall     | double            | fluency score (range determined by point scale)                                                  |
| ├─ pause       | integer           | number of pauses                                                                                 |
| ├─ speed       | integer           | speech rate (0: slow, 1: normal, 2: fast)                                                        |
| accuracy       | double            | accuracy (range determined by point scale)                                                       |
| integrity      | double            | completeness (range determined by point scale)                                                   |
| **rhythm**     | **dict**          | **rhythm score object**                                                                          |
| ├─ overall     | double            | rhythm score (range determined by point scale)                                                   |
| ├─ stress      | double            | stress pronunciation score (range determined by point scale)                                     |
| ├─ tone        | double            | rising tone score (range determined by point scale)                                              |
| ├─ sense       | double            | meaning group pause score (range determined by point scale)                                      |
| waveTime       | integer           | actual recording time（ms）                                                                        |
| startTime      | integer           | the starting reading position in a recording (ms)                                                |
| endTime        | integer           | the ending reading position in a recording (ms)                                                  |
| **wordInfo**   | **list\<dict\>**  | **array of word info objects (👇)**                                                              |

### wordInfo

| **field**          | **type**          | **remark**                                                                                                                                     |
|:-------------------|:------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------|
| refText            | string            | reference text                                                                                                                                 |
| hypothesis         | string            | actual text read                                                                                                                               |
| overall            | double            | total score (range determined by scale)                                                                                                        |
| fluency            | double            | fluency score (range determined by point scale)                                                                                                |
| accuracy           | double            | accuracy (range determined by point scale)                                                                                                     |
| integrity          | double            | completeness (range determined by point scale)                                                                                                 |
| **rhythm**         | **dict**          | **word rhythm info objects **                                                                                                                  |
| ├─ stressRef       | integer           | word stress label (1 means it should be accented, 0 means it shouldn't be accented/do not check)                                               |
| ├─ stressScore     | integer           | word stress score (1 means actually agrees with label, 0 means doesn't match/do not check)                                                     |
| ├─ toneRef         | integer           | word rising tone label (1 means it should be sharpened, 0 means it shouldn't be sharpened/do not check)                                        |
| ├─ toneScore       | integer           | word rising tone score (1 means actual agrees with label, 0 means actual does not agree with label/do not check)                               |
| ├─ senseRef        | integer           | word sense group pause label (1 means it should pause, 0 means it shouldn't pause/do not check)                                                |
| ├─ senseScore      | integer           | word sense group pause score (1 means actual agrees with label, 0 means actual does not agree with label/do not check)                         |
| ├─ liaisonRef      | integer           | word continuous reading label (1 means it should be linked with the next word, 0 means it should not be linked/do not check)                   |
| ├─ liaisonScore    | integer           | word continuous reading score（1 means the actual is consistent with the label, 0 means the actual is inconsistent with the label/do not check） |
| type               | string            | [word type](datadict/other)                                                                                                                    |
| startTime          | integer           | the starting reading position in a recording (ms)                                                                                              |
| endTime            | integer           | the ending reading position in a recording (ms)                                                                                                |
| **syllables**      | **list\<dict\>**  | **array of syllable info objects**                                                                                                             |
| ├─ syllable        | string            | Constantly empty                                                                                                                               |
| ├─ score           | double            | Always 0                                                                                                                                       |
| ├─ stressRef       | integer           | Always 0                                                                                                                                       |
| ├─ stressScore     | integer           | Always 0                                                                                                                                       |
| ├─ startTime       | integer           | Always 0                                                                                                                                       |
| ├─ endTime         | integer           | Always 0                                                                                                                                       |
| ├─├─ **phonemes**  | **list\<dict\>**  | **array of phonemes info objects**， refer to *SpeechEvalPro* scheme [English Phonetic Symbol Comparison Table](datadict/phoneme)               |
| ├─├─ phoneme       | string            | phoneme                                                                                                                                        |
| ├─├─ hypothesis    | string            | actual phoneme read                                                                                                                            |
| ├─├─ score         | double            | phoneme score (range determined by point scale)                                                                                                |
| ├─├─ phid          | string            | the position of the letter in the phoneme of the word, such as `1_2`                                                                           |
| ├─├─ ph2alpha      | string            | the original letter information corresponding to the phoneme                                                                                   |
| ├─├─ startTime     | integer           | the starting reading position in a recording (ms)                                                                                              |
| ├─├─ endTime       | integer           | the ending reading position in a recording (ms)                                                                                                |

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