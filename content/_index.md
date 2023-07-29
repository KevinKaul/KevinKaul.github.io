---
title: 💜 Welcome to SpeechEvalPro! 
enableToc: false
---

## What is SpeechEvalPro?

Independent research and development of educational voice AI model, integrating voice evaluation, speech recognition and other core 

technologies, providing high-quality, multi-dimensional Chinese and English pronunciation evaluation API, helping customers create 

intelligent learning products for human-computer interaction.

## Get Started
> 👀 Way 1: [Quick Start](setup/quick_start.md)

> ✏️ Way 2: Usage Guides
> - step 1: [Generate JWT token](setup/usage/token.md)
> - step 2: [Websocket streaming evaluation](setup/usage/ws.md) 

## Supported audio formats

| parameter          | opus_raw | pcm      | wav      | mp3      |
|:-------------------|:---------|:---------|:---------|:---------|
| number of channels | Mono     | Mono     | Mono     | Mono     |
| bit depth          | N/A      | 16 bit   | 16 bit   | N/A      |
| sample rate        | 16000 Hz | 16000 Hz | 16000 Hz | 16000 Hz |


> opus_raw : It is the original opus encoding format that has not been encapsulated by the ogg container, which can maximize the retention of effective voice information while reducing the transmission bandwidth


## Supported question type introduction
### English question type

langType：en-US

| name                                   | mode      | Audio duration limit  | Reference text length limit  |
|:---------------------------------------|:----------|:----------------------|:-----------------------------|
| [phoneme](mode/en-basic/phoneme.md)    | phoneme   | 20 s                  | 100 characters               |
| [word](mode/en-basic/word.md)          | word      | 20 s                  | 100 characters               |
| [sentence](mode/en-basic/sentence.md)  | sentence  | 40 s                  | 300 characters               |
| [paragraphs](mode/en-basic/chapter.md) | chapter   | 300 s                 | 10000 characters             |

### Chinese question type

langType：zh-cmn-Hans-CN

| name                                   | mode      | Audio duration limit  | Reference text length limit  |
|:---------------------------------------|:----------|:----------------------|:-----------------------------|
| [phoneme](mode/zh-basic/phoneme.md)    | phoneme   | 20 s                  | 100 characters               |
| [word](mode/zh-basic/word.md)          | word      | 20 s                  | 50 characters                |
| [sentence](mode/zh-basic/sentence.md)  | sentence  | 40 s                  | 100 characters               |
| [paragraphs](mode/zh-basic/chapter.md) | chapter   | 300 s                 | 1000 characters              |
