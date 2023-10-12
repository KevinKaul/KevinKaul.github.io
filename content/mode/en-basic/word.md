---
title: "Word Scoring"
weight: 2
---

> wss://api.xxxxx.com/en-US/word
## Limit

- send audio up to 20 seconds long 
- reference text up to 100 characters.

## Parameter

| **field** | **type** | **defaults** | **remark**                                                                                         |
|:----------|:---------|:-------------|:---------------------------------------------------------------------------------------------------|
| mode      | string   | required     | word                                                                                               |
| refText   | string   | required     | reference text <br />Reference text support [English special label format](datadict/annotation-en) |

> [!EXAMPLE] Examples
>
> 

```json
{
  "mode":"word",
  "refText":"hello world"
}
```

## Evaluation Results

- [A complete example of the JSON response result](mode/en-basic/word-result)

| **field**     | **type**         | **remark**                                                                                       |
|:--------------|:-----------------|:-------------------------------------------------------------------------------------------------|
| evalId        | string           | evalId                                                                                           |
| timestamp     | integer          | task timestamp                                                                                   |
|~~attachAudioUrl~~      | string           | audio storage url (this field is only returned when the question type parameter `attachAudioUrl=true`) |
| **audioInfo** | **dict**         | [Audio Quality Information](mode/common)                                                         |
| refText       | string           | reference text                                                                                   |
| hypothesis    | string           | actual text read                                                                                 |
| overall       | double           | total score (range determined by scale)                                                          |
| accuracy      | double           | accuracy (range determined by point scale)                                                       |
| waveTime      | integer          | actual recording time（ms）                                                                        |
| startTime     | integer          | the starting reading position in a recording (ms)（ms）                                            |
| endTime       | integer          | the ending reading position in a recording (ms)（ms）                                              |
| **wordInfo**  | **list\<dict\>** | **array of word info objects (👇)**                                                              |

### wordInfo

| **field**        | **type**          | **remark**                                                                                                                       |
|:-----------------|:------------------|:---------------------------------------------------------------------------------------------------------------------------------|
| refText          | string            | reference text                                                                                                                   |
| hypothesis       | string            | actual text read                                                                                                                 |
| score            | double            | total score (range determined by scale)                                                                                          |
| accuracy         | double            | word accuracy (range determined by point scale)                                                                                  |
| **rhythm**       | **dict**          | **word rhythm info objects **                                                                                                    |
| ├─ stressRef     | integer           | word stress label (1 means it should be accented, 0 means it shouldn't be accented/do not check)                                 |
| ├─ stressScore   | integer           | word stress score (1 means actually agrees with label, 0 means doesn't match/do not check)                                       |
| type             | string            | [word type](datadict/other)                                                                                                      |
| startTime        | integer           | the starting reading position in a recording (ms)                                                                                |
| endTime          | integer           | the ending reading position in a recording (ms)                                                                                  |
| **syllables**    | **list\<dict\>**  | **array of syllable info objects**, refer to *SpeechEvalPro* scheme [English Phonetic Symbol Comparison Table](datadict/phoneme) |
| ├─ syllable      | string            | phonemic composition of syllables. Phonemes are separated by underscores, such as g_uh_d                                         |
| ├─ score         | double            | syllable score (range determined by scale)                                                                                       |
| ├─ stressRef     | integer           | syllable stress label (1 means it should be stressed, 0 means it shouldn't)                                                      |
| ├─ stressScore   | integer           | syllable stress score (1 means actually agrees with label, 0 means doesn't match/do not check)                                   |
| startTime        | integer           | the starting reading position in a recording (ms)                                                                                |
| endTime          | integer           | the ending reading position in a recording (ms)                                                                                  |
| **├─ phonemes**  | **list\<dict\>**  | **array of phonemes info objects**， refer to *SpeechEvalPro* scheme [English Phonetic Symbol Comparison Table](datadict/phoneme) |
| ├─├─ phoneme     | string            | phoneme                                                                                                                          |
| ├─├─ hypothesis  | string            | actual phoneme read                                                                                                              |
| ├─├─ score       | double            | phoneme score (range determined by point scale)                                                                                  |
| ├─├─ phid        | string            | the position of the letter in the phoneme of the word, such as `1_2`                                                             |
| ├─├─ ph2alpha    | string            | the original letter information corresponding to the phoneme                                                                     |
| ├─├─ startTime   | integer           | the starting reading position in a recording (ms)                                                                                |
| ├─├─ endTime     | integer           | the ending reading position in a recording (ms)                                                                                  |