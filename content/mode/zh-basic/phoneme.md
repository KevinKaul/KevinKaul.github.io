---
title: "Hanyu Pinyin Scoring"
weight: 1
---


## Limit

- send audio up to 20 seconds long 
- reference text up to 100 characters.

## Parameter

| **field** | **type** | **defaults** | **remark**                                                                                                                                                                                                                                                                                                                |
|:----------|:---------|:-------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| mode      | string   | required     | phoneme                                                                                                                                                                                                                                                                                                                   |
| refText   | string   | required     | Reference text, supporting consonants, rhymes, unvoiced syllables, voiced syllables, no more than 100 characters<br/>Only supports pinyin representation in `SpeechEvalPro` format ——[Chinese special label format](datadict/annotation-zh) . Multiple consonants, rhymes, and syllables are separated by English spaces. |

- Tones are 0~4 for soft, one to four tones respectively, defaults to one tone when no tone is written.

- Rhymes only support inputting the first 24 rhymes in the [rhyme scheme](datadict/pinyin).

- Syllable spelling is supported (except for monosyllables), see [Syllable Spelling Labeling Format](datadict/annotation-zh) for more details.

> [!EXAMPLE] Examples
>
> 

```json
{
  "mode":"phoneme",
  "refText":"i u v b po1 mo1(*) fo"
}
```

## Evaluation Results

- [A complete example of the JSON response result](mode/zh-basic/phoneme-result)

| **field**         | **type**         | **remark**                                                                                                                                                     |
|:------------------|:-----------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| taskId            | string           | taskID                                                                                                                                                         |
| timestamp         | integer          | task timestamp                                                                                                                                                 |
| audioUrl          | string           | audio storage url (this field is only returned when the question type parameter `audioUrl=true`)                                                               |
| **audioInfo**     | **dict**         | [Audio Quality Information](mode/common)                                                                                                                       |
| refText           | string           | reference text                                                                                                                                                 |
| overall           | double           | total score                                                                                                                                                    |
| phn               | double           | pronunciation accuracy without tones (range determined by a point system)                                                                                      |
| toneScore         | double           | overall tone score (range determined by point system)                                                                                                          |
| accuracy          | double           | accuracy (range determined by point scale)                                                                                                                     |
| fluency           | double           | fluency score (range determined by point scale)                                                                                                                |
| integrity         | double           | completeness (range determined by point scale)                                                                                                                 |
| waveTime          | integer          | actual recording time（ms）                                                                                                                                      |
| startTime         | integer          | the starting reading position in a recording (ms)                                                                                                              |
| endTime           | integer          | the ending reading position in a recording (ms)                                                                                                                |
| **syllables**     | **list\<dict\>** | **array of syllables info objects**                                                                                                                            |
| ├─ refText        | string           | reference text (transcribed representation of consonants), if it ends in `(*)` it means that the syllable needs to be [spelled out](datadict/annotation-zh.md) |
| ├─ overall        | double           | syllable overall score (range determined by a point system)<br/>synthesizes the toneless pronunciation (phn) and toneScore of syllables                        |
| ├─ phn            | double           | pronunciation accuracy without tones (range determined by a point system)                                                                                      |
| ├─ toneRef        | integer          | standard tones (0 to 4 for soft, one to four tones respectively)                                                                                               |
| ├─ toneConfidence | integer[]        | tone confidence level (range 0 to 100, elements in order: soft, one to four)                                                                                   |
| ├─ toneScore      | double           | tone score (range determined by point system)                                                                                                                  |
| ├─ startTime      | integer          | the starting reading position in a recording (ms)                                                                                                              |
| ├─ endTime        | integer          | the ending reading position in a recording (ms)                                                                                                                |
| **phonemes**      | **list\<dict\>** | **array of phonemes info objects**                                                                                                                             |
| ├─ phoneme        | string           | transcription representation of sounds and rhymes                                                                                                              |
| ├─ score          | double           | vocalization score (range determined by point system)                                                                                                          |
| ├─ startTime      | integer          | the starting reading position in a recording (ms)                                                                                                              |
| ├─ endTime        | integer          | the ending reading position in a recording (ms)                                                                                                                |
