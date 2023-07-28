---
title: "English special label format"
weight: 1
---


In different English question types, the reference text (refText) supports the input of multiple annotation formats to meet the requirements of specific reading methods.

When passing in parameters, use the corresponding annotation format directly in the `refText` field, for example:


```json
{
    "mode": "sentence",
    "refText": "It's mine, isn't it(t:1)?"
}
```

Question type is supported, which means that parameters are passed in according to the specified format, and scoring will be performed according to this format.

> **Notice**
>
> If a label format is passed in an unsupported question type, the scoring result will not be affected.

### rhythm annotation format

Note the use of half-width (English) characters for brackets and colons.

 `0` after the colon means a negative meaning,  `1` means a positive meaning. For example: `(t:0)` means falling tone, `(t:1)` means rising tone, and so on.

| Item                  | supported mode  | format          | example                 | remark                                                                                                                 |
|:----------------------|:----------------|:----------------|:------------------------|:-----------------------------------------------------------------------------------------------------------------------|
| stress pronunciation  | word、sentence   | (s:0) or (s:1)  | Hello(s:1) everyone.    | `hello` stress pronunciation                                                                                           |
| rising tone           | sentence        | (t:0) or (t:1)  | What's your name(t:0)?  | `name` rising tone                                                                                                     |
| meaning group pause   | sentence        | (g:0) or (g:1)  | Are you(g:1) ok?        | there is a pause between you and ok                                                                                    |
| continuous reading    | sentence        | (c:0) or (c:1)  | Stand(c:1) up.          | The two words stand and up are read together                                                                           |
| stress&Rising tone    | sentence        | (s:1,t:1)       | Are you ok(s:1,t:1)?    | ok means stress pronunciation and rising tone at the same time, and the marking symbols need to be separated by commas |

### phoneme annotation format

When a word has multiple pronunciations, the incoming phonetic symbol is used to specify one or more pronunciations.

| Item                     | format     | example                      | remark                                                                                        |
|:-------------------------|:-----------|:-----------------------------|:----------------------------------------------------------------------------------------------|
| SpeechEvalPro scheme     | (z:xx xx)  | It's a live(z:l ay v) show.  |                                                                                               |
| Standard phonetic scheme | (p:xx xx)  | It's a live(p:l aɪ v) show.  | If the phonetic symbols correspond to multiple standards, the processing priority is: `KK>DJ` |

When specifying multiple pronunciations, separate them with vertical bars, such as `live(z:l ay v|l ih v)` 。
