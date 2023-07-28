---
title: "Chinese special label format"
weight: 2
---

# Chinese special label format

In different Chinese question types, the reference text (refText) supports the input of multiple annotation formats to meet the requirements of specific reading methods.

When passing in parameters, use the corresponding annotation format directly in the `refText` field, for example:


```json
{
    "mode": "word",
    "refText": "长(zhang3)长(chang2)"
}
```

Pass in the parameters according to the specified label format, and the score will be scored according to this format

> **Notice**
>
> If a label format is passed in an unsupported question type, the scoring result will not be affected.

### Single character pronunciation annotation format

Dimension formatting only applies to the character preceding the parenthesis.

| Label item                              | format                                                                                                                                                                                                                          | example               |
|:----------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------|
| Polyphonic characters (specify pinyin)  | (xx1) or (z:xx1)<br>`xx` represents the consonant, `1` represents the tone<br>The value of the tone is 0~4, which means soft tone, one tone to four tone, respectively, and the default tone is soft tone if no tone is written | 长(zhang3)长(chang2)    |
| Erhuayin                                | (er:0) do not read Erhuayin<br>(er:1) read Erhuayin<br>Erhua sound is not considered when there is no label                                                                                                                     | 前门(er:0)              |

### Multi-word pronunciation annotation format

Dimension formatting applies to all characters within a square bracket preceding the parenthesis.

| Label item      | format                                                                                                                                                                                                                                                                                                                           | example                  |
|:----------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------|
| specify pinyin  | \[abc](xx1) or \[abc](z:xx1)<br>`abc` indicates the character whose pronunciation needs to be specified, `xx` indicates the consonant and final, and `1` indicates the tone<br/>The values of the tone are 0~4, which respectively indicate a soft tone, one to four tones, and the default tone is soft when no tone is written | \[110](yao1 yao1 ling2)  |

### Syllable spelling markup format

It is used in the syllable spelling scene of the Chinese Pinyin question type. When spelling a syllable, it must be a complete syllable marked with tones, and pay attention to the use of brackets and asterisks in half-width (English) characters.

| Label item  | Support question type  | format    | example     | remark                           |
|:------------|:-----------------------|:----------|:------------|:---------------------------------|
| basic       | phoneme                | No label  | zhuang4     | Pronunciation : zhuang           |
| phonics     | phoneme                | (*)       | zhuang4(*)  | Pronunciation : zh_u_ang_zhuang  |

> **Notice**
>
> For the following 16 overall syllables and 11 other zero-consonant syllables, **Syllabic pronunciation is not supported**.
>
> | ID    | overall syllables                         | remark                                                                                        |
> |:------|:------------------------------------------|:----------------------------------------------------------------------------------------------|
> | 1     | zhi、chi、shi、ri                            | Overall reading: consonant consonant + apical back vowel [ʅ]                                  |
> | 2     | zi、ci、si                                  | Overall reading: flat tongue initial + apical front vowel [ɿ]                                 |
> | 3     | ye                                        | Overall reading: the zero-consonant syllable corresponding to the final ie                    |
> | 4     | yi、yin、ying、wu                            | Overall reading: the zero-consonant syllable corresponding to the final i/in/ing/u            |
> | 5     | yu、yue、yun、yuan                           | Overall reading: the zero-consonant syllable corresponding to the final consonant ü/üe/ün/üan |
> | 6     | a、o、e、ai、ao、an、ang、ou、ei、er、en            | Other: zero initial syllables corresponding to finals starting with a/o/e                     |

### prosodic notation format

Note the use of half-width (English) characters for brackets and colons.

 `0` after the colon means a negative meaning, a `1` means a positive meaning. For example: `(t:0)` means falling pitch, `(t:1)` means rising pitch, and so on.

| prosody scoring item  | format                                                                                                             | example          |
|:----------------------|:-------------------------------------------------------------------------------------------------------------------|:-----------------|
| meaning group pause   | (g:0) or (g:1) or (g:2)<br />`(g:0)`means no pause，`(g:1)` Indicates a short pause，`(g:2)` Indicates a long pause， | 今天(g:1)真热。       |
| rising tone           | (t:0) or (t:1)                                                                                                     | 是你(t:1)？         |
| sustained sound       | (e:0) or (e:1)                                                                                                     | 再见(e:1)！         |
