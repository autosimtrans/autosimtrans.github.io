---
layout: main-anchor
title: Shared Task
order: 3
collection: pages_2020
permalink: /shared
---



# Important Dates
- **January 2020**: release of train and dev data
- **March 2020**: evaluation period
- **April 6th 2020**: system description paper due
- **May 4th 2020**: review feedback
- **May 18th 2020**: camera-ready paper due

All submission deadlines are 11:59 PM GMT-12 (anywhere in the world) unless otherwise noted.

---

# Data
#### Training Data
##### 1. Speech Translation Data
The training set consists of two different language directions: (1) Chinese-to-English translation (Zh->En), which contains about 70 hours of Chinese speech audio, human transcripts, ASR results[1] and English translations, and (2) English-to-Spanish translation (En->Es), which includes about 50 hours of English speech audio, human transcripts, ASR results[2] and Spanish translations. 

[1] Chinese ASR by Baidu Speech.  
[2] English ASR  by Google's Speech Recognition API.

##### 2. Machine Translation Data
We suggest using large-scale corpus ([WM19](http://www.statmt.org/wmt19/translation-task.html) Zh->En and [Europarl](http://www.statmt.org/europarl) for En->Es) to train your machine translation system. You can further finetune the model on our speech translation dataset.

#### Development Data 
We provide 12 talks for Zh->En and En->Es speech translation tasks, 6 for each, to evaluate your system. Each talk is presented with its audio file, gold transcript, ASR transcript, and reference translations. 

#### Testing Data
Our testset will not be released. You are required to upload your docker system, with useful information available on the [tutorial](https://autosimtrans.github.io/tutorial) page. Within 24 hours after you submit your docker file, we'll publish the evaluation results on the competition website.

---

# System
As our competition offers two translation directions and three types of input data, there are six tracks all together:

1. Zh->En Translation, input: incremental clean transcription
2. Zh->En Translation, input: incremental ASR transcription
3. Zh->En Translation, input: streaming audio
4. En->Es Translation, input: incremental clean transcription
5. En->Es Translation, input: incremental ASR transcription
6. En->Es Translation, input: streaming audio

At test time, the systems are expected to receive different file formats based on the system types. For text-to-text translation systems, the inputs are streaming source text (including gold transcripts and ASR results) and the outputs are corresponding simultaneous translation results. For speech-to-text translation systems, the inputs are speech audio files and the outputs are corresponding simultaneous translation results.

#### Platform

Please redirect to [Baidu AI Studio](https://aistudio.baidu.com/aistudio/competition/detail/18?lang=en) for dataset and submission.

#### Tutorial for docker submission

It's not trivial to evaluate a simultaneous system as we cannot release the test data like offline translation tasks. Participants are required to upload the systems as a Docker image, along with their own implementation of specific APIs for input and translation output. We will evaluate all the submissions on our environment. We will provide an example implementation which will also serve as the baseline system.

Please refer to the [tutorial](https://autosimtrans.github.io/tutorial) page if you need help to convert your model to docker image, or train in docker container.

<script src="https://cdnjs.cloudflare.com/ajax/libs/mermaid/8.0.0/mermaid.min.js"></script>
<script>
mermaid.initialize({startOnLoad:true});
</script>

<div class='mermaid' align="center"> 
graph TD
WS(AutoSimTrans)
WS-->A(text-to-text)
WS-->B(speech-to-text)

A-->AA(gold transcript)
A-->AB(ASR outputs)
AA-->AA1(incremental input)
AB-->AB1(incremental input)
AA1-->|input|AA2{SimMT model}
AA2-->|output|AA3(step-wised translation)
AB1-->|input|AB2{SimMT model}
AB2-->|output|AB3(step-wised translation)
AA3-->|eval|AA4(BLEU-AL)
AB3-->|eval|AB4(BLEU-AL)

B-->B1(speech audio)
B1-->B2(incremental input)
B2-->|input|B3{"cascaded models<br>(ASR + MT)<br>or end-to-end model"}
B3-->|output|B4(step-wised translation)
B4-->|eval|B5(BLEU-AL)

classDef green fill:#9f6,stroke:#333,stroke-width:2px;;
classDef orange fill:#f48c42,stroke:#f66,stroke-width:2px;
class AA2,AB2,B3 orange
class AA,AB,B1 green
</div>

---

# Evaluation

Following previous work, we evaluate simultaneous translation results based on BLEU and AL (average lagging). BLEU is the measurement for translation quality and AL measures system delays. The evaluation results of all teams will be plotted on BLEU-AL two-dimensional coordinates. 


---

# Challenge Chair
- Ruiqing Zhang (zhangruiqing01@baidu.com)
- Kaibo Liu (kaiboliu@baidu.com)

# Committee
- Ying Chen (chenying04@baidu.com), Data
- Junjie Li (lijunjie02@baidu.com), Data
- Zhi Li (lizhi02@baidu.com), Data
- Boxiang Liu (boxiangliu@baidu.com), Data
- Hairong Liu (liuhairong@baidu.com)
- Mingbo Ma (mingboma@baidu.com)
- Di Song (songdi@baidu.com), Platform
- Lei Sun (sunlei18@baidu.com), Platform
- Meng Wang (wangmeng09@baidu.com), Platform
- Wenxi Zhang (zhangwenxi@baidu.com), Platform
- Baigong Zheng (baigongzheng@baidu.com), Data
- Renjie Zheng (renjiezheng@baidu.com), Data

---

# Contact
For any questions regarding our shared task, please use [Github issues](https://github.com/autosimtrans/AutoSimTrans-Shared-Task-2020/issues), or email to [autosimtrans.workshop@gmail.com](autosimtrans.workshop@gmail.com). We are here to answer your questions and looking forward to your submissions!
