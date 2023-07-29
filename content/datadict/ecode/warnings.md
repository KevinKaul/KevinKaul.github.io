---
title: "Warnings"
weight: 1
---


| Type             | Code  | Message                 | Tips Developers                                                                             | Remark                                                                                                                                                   |
|:-----------------|:------|:------------------------|:--------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------|
| Audio            | 35003 | audio length is 0       | Check the audio data length                                                                 | If the audio duration is 0, the warning callback  returns the evaluation result                                                                          |
| Audio            | 35102 | audio length exceeded   | Control the user's recording time on the interactive interface to avoid excessive recording | For details, please refer to the Introduction to Questions document                                                                                      |
| Audio            | 35001 | audio data is too short | Control the user's recording time on the interactive interface to avoid recording too short | 0<Audio duration<240ms                                                                                                                                   |
| Audio            | 35002 | audio volume is too low | Check the recording for correctness                                                         | The volume is too low （When the audio is short and the volume is low, the priority is to return `The volume is too low`）                                 |
