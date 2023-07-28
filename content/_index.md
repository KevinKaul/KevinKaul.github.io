---
title: 💜 Welcome to SpeechEvalPro! 
enableToc: false
---

## What is SpeechEvalPro?

Independent research and development of educational voice AI model, integrating voice evaluation, speech recognition and other core 

technologies, providing high-quality, multi-dimensional Chinese and English pronunciation evaluation API, helping customers create 

intelligent learning products for human-computer interaction.

## Get Started
> 📚 Step 1: [获取AppKey](setup/appkey.md)

> ✏️ Step 2: [获取Token](setup/token.md)

> 🔗 Step 3: [websocket 评测流程](setup/ws.md)

> 👀 Step 4: [查看golang example](setup/example.md)

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

| name                                                         | mode     | Audio duration limit | Reference text length limit |
|:-------------------------------------------------------------|:---------|:---------------------|:----------------------------|
| <a href="#/help?url=mode/en-basic/phoneme.md" target="_blank">phoneme</a> | phoneme  | 20 s                 | 100 characters              |
| <a href="#/help?url=mode/en-basic/word.md" target="_blank">word</a> | word     | 20 s                 | 100 characters              |
| <a href="#/help?url=mode/en-basic/sentence.md" target="_blank">sentence</a> | sentence | 40 s                 | 300 characters              |
| <a href="#/help?url=mode/en-basic/chapter.md" target="_blank">paragraph</a> | chapter  | 300 s                | 10000 characters            |

## Chinese question type

langType：zh-cmn-Hans-CN

| name                                                         | mode     | Audio duration limit | Reference text length limit |
|:-------------------------------------------------------------|:---------|:---------------------|:----------------------------|
| <a href="#/help?url=mode/en-basic/phoneme.md" target="_blank">phoneme</a> | phoneme  | 20 s                 | 100 characters              |
| <a href="#/help?url=mode/en-basic/word.md" target="_blank">word</a> | word     | 20 s                 | 50 characters               |
| <a href="#/help?url=mode/en-basic/sentence.md" target="_blank">sentence</a> | sentence | 40 s                 | 100 characters              |
| <a href="#/help?url=mode/en-basic/chapter.md" target="_blank">paragraph</a> | chapter  | 300 s                | 1000 characters             |



