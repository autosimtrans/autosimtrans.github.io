---
layout: main-anchor
title: Shared Task
order: 3
collection: pages_2020
permalink: /shared
---



# Registration

Please register your team through this [Platform](https://aistudio.baidu.com/aistudio/competition/detail/18?lang=en).

---

# Challenge

Our challenge includes 4 tasks on Chinese-to-English translation (Zh->En) and English-to-Spanish translation (En->Es). Participants can choose to join one or more tasks. 

1. Zh->En Translation, input: streaming transcription
2. Zh->En Translation, input: streaming ASR<sup>[[1](#1-chinese-asr-by-baidu-speech)]</sup>
3. Zh->En Translation, input: audio file
4. En->Es Translation, input: streaming transcription

There are three types of inputs involved:

1. **Streaming transcription** provides the golden transcripts in streaming format, where each sentence is broken into lines whose length is incremented by one word until the end of the sentence.
2. **Streaming ASR** provides the realtime streaming ASR results<sup>[[1](#1-chinese-asr-by-baidu-speech)]</sup>. During the ASR, errors may occur, and the recognition result of one line may be modified compared with the previous ones. Note that there is no punctuation predicted during ASR. 
3. **Audio**: You can also choose to use your own ASR system with the audio as input.

An example of the three types of input is illustrated in Table 1.  We process input data into streaming format to evaluate the system delay (refer to [Evaluation](#evaluation)).

Streaming Transcript	|	Streaming ASR	|	Audio
-|-|-
大	|	大家	|	<audio controls="controls" style="height: 20px;width: 170px;"><source type="audio/mp3" src="assets/105-[AudioTrimmer.com].wav"></source><p>Your browser does not support the audio element.</p></audio>
大家	|	大家好	|
大家好	|	大家好欢迎	|	
大家好！	|	大家好欢迎大	|	
欢	|	大家好欢迎大家	|
欢迎	|	大家好欢迎大家关注	|	
欢迎大	|	大家好欢迎大家关注注	|	
欢迎大家	|	大家好欢迎大家关注祝英	|	
欢迎大家关	|	大家好欢迎大家关注祝unit	|	
欢迎大家关注	|	大家好欢迎大家关注祝unit对话性	|	
欢迎大家关注UNIT	|	大家好欢迎大家关注祝unit对话性和	|	
欢迎大家关注UNIT对	|	大家好欢迎大家关注祝unit对话性和高级	|	
欢迎大家关注UNIT对话	|	大家好欢迎大家关注祝unit对话性的高级可	|	
欢迎大家关注UNIT对话系	|	大家好欢迎大家关注祝unit对话性和高级课程	|	
欢迎大家关注UNIT对话系统	|	
欢迎大家关注UNIT对话系统的	|	
欢迎大家关注UNIT对话系统的高	|	
欢迎大家关注UNIT对话系统的高级	|	
欢迎大家关注UNIT对话系统的高级课	|	
欢迎大家关注UNIT对话系统的高级课程	|	
欢迎大家关注UNIT对话系统的高级课程。	|	

<div style="text-align: center;">
    Table 1. Illustration of three types of input
</div>

---

# Dataset

### Training set and Development set

##### Machine Translation Data
You need to train a baseline MT model using the text parallel corpus specified in the table below ( `CWMT19` for Zh->En and `UN`  for En->Es, respectively), because the amount of speech translation data we provide is insufficient to support the training of a large translation model.

|Lang | Training set | 
|:-:|:-:|
|Zh-&gt;En | [CWMT19](http://nlp.nju.edu.cn/cwmt-wmt) | 
|En-&gt;Es | [UN Parallel Corpus](https://conferences.unite.un.org/UNCORPUS/en/DownloadOverview#download) | 

##### Speech Translation Data
For Zh->En translation, our training set contains about 70 hours of Chinese speech audio, human transcripts, ASR results<sup>[[1](#1-chinese-asr-by-baidu-speech)]</sup> and English translations. To evaluate your system, we provide 16 talks with their corresponding streaming ASR and streaming transcripts as the development set. 

For En->Es translation, we don't provide additional speech translation dataset. You are required to use the UN dataset only to train your MT model. To evaluate your system, we will provide the streaming transcripts as the development set. 

As shown in Table 2, we would provide 7 parts of speech translation data, among which the highlighted 5 will be sent to participants by email.

<table style="text-align: center;">
    <thead>
        <tr>
            <th>Tracks</th>
            <th></th>
            <th>DataSource</th>
            <th>train</th>
            <th>dev</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        	<td>1</td>
            <td rowspan="3">Zh->En</td>
            <td>Audio</td>
            <td><a href="https://bj.bcebos.com/ibox-docpreview100/43319cc7679b4077cdd672319c590598?authorization=bce-auth-v1%2Ffbe74140929444858491fbf2b6bc0935%2F2020-02-19T08%3A06%3A24Z%2F1800%2F%2F268d4d15e644c059fd580621cd6a496a5b0f2e68824fd4c8f21f8411c8c2cf6e&responseContentDisposition=attachment%3Bfilename%3D%2220200219155334.zip%22" target="_blank">70 hours of speeches</a></td>
            <td><a href="http://bj.bcebos.com/v1/ai-studio-online/4e3fce487a3943f0a56e85f4c2b5f6535864ecd434164788a86677700e8118b6?responseContentDisposition=attachment%3B%20filename%3Ddevdata.zip&authorization=bce-auth-v1%2F0ef6765c1e494918bc0d4c3ca3e5c6d1%2F2020-02-19T08%3A00%3A16Z%2F-1%2F%2F98c5e852c7543b6386024fef611c0886fccf07c3855d5581025d368f1b1dd3a2" target="_blank">dev audio</a></td>
        </tr>
        <tr>
            <td>2</td>
            <td>ASR</td>
            <td style="background: yellow">✓</td>
            <td style="background: yellow">✓</td>
        </tr>
        <tr>
            <td>3</td>
            <td>Transcription</td>
            <td style="background: yellow">✓</td>
            <td style="background: yellow">✓</td>
        </tr>
        <tr>
            <td>4</td>
            <td>En->Es</td>
            <td>Transcription</td>
            <td>/</td>
            <td style="background: yellow">✓</td>
        </tr>
    </tbody>
</table>

<div style="text-align: center;">
    Table 2. Speech Translation Dataset provided
</div>


## Testing Data
Our testset will not be released. You are required to upload your whole system and environment. Within 24 hours after you submitting your system, we'll publish the evaluation results on the competition website.

At test time, the systems are expected to receive different file formats based on the system types. For text-to-text translation systems, the inputs are streaming source text (including gold transcripts and ASR results) and the outputs are corresponding simultaneous translation results. For speech-to-text translation systems, the inputs are speech audio files and the outputs are corresponding simultaneous translation results.


# <span id="evaluation">Evaluation</span>

### Output
For all the four tasks, you output only one text file containing source sentences and translations. The Table 3 is an example with streaming ASR input. Your system needs to decide when to translate given the input, and to write the translation after corresponding source. Your translations will be concatenated with **SPACEs** to evaluate BLEU. Note that the left part (streaming source) should **NOT** be modified in streaming ASR and streaming transcription tasks. 

Streaming ASR	|	Translation
-|-
大家	|	
大家好	|	
大家好欢迎	|	Hello everyone.
大家好欢迎大	|	
大家好欢迎大家	|	Welcome
大家好欢迎大家关注	|	to
大家好欢迎大家关注注	|	
大家好欢迎大家关注祝英	|	
大家好欢迎大家关注祝unit	|	
大家好欢迎大家关注祝unit对话性	|	unit
大家好欢迎大家关注祝unit对话性和	|	
大家好欢迎大家关注祝unit对话性和高级	|	dialog and 
大家好欢迎大家关注祝unit对话性的高级可	|	advanced
大家好欢迎大家关注祝unit对话性和高级课程	|	cources

<div style="text-align: center;">
    Table 3. Illustration of output file
</div>

For Zh-En translation with audio input, you also have to output this source-translation file, with the left part as your recognition source and right part as the corresponding translation. 

### Submit methods
You have two ways to submit your system:

1. **For AISTUDIO Project owner**: You can use the calculation resources for free (one V100 card for each participant) if your system ONLY RELIES ON PADDLEPADDLE as the deep-learning framework. The free resources are provided by AISTUDIO. In this case, you can submit your system by specifying your projectID on AISTUDIO. Note that using other deep-learning platforms (as Tensorflow or Pytorch) is forbidden by AISTUDIO. 
2. **For Other submitters**, you are required to submit your docker system, along with your own implementation of specific APIs for input and translation output. We will evaluate all the submissions on our environment. Please refer to the [tutorial page](https://autosimtrans.github.io/tutorial) if you need help to convert your model to docker image, or train in docker container.

There are some requirements for your uploaded system:

1. script <b>run.sh</b>: the interface to execute your translate program. 
For text-to-text tasks, use  
`sh run.sh < streaming_asr.txt > output_asr/source_translation.txt` or  
`sh run.sh < streaming_transcription.txt > output_transcript/source_translation.txt`;  
For audio-to-text task, use  
`sh run.sh < audioid.wav > output_audio/source_translation.txt` 

2. directory <b>output_xxx</b>: your environment should have a directory named `output_asr`, `output_transcript` or `output_audio`, depends on the task you involved in. You can also prepare multiple output directories of them, if you participate in multiple challenge tasks. 
3. file <b>output_xxx/dev_translation.txt</b>: we suggest you to put the source-translation result file of the development set under the corresponding task output directory, with the file name as `output_xxx/dev_translation.txt`. This is very helpful for us to eliminate the execution problems of your system.

Unless coming across system execution error, each participant has only one chance to submit on each task.


### Evaluation Metrics
Following previous work, we evaluate simultaneous translation results based on BLEU and [AL (average lagging)](https://github.com/SimulTrans-demo/STACL). BLEU is the measurement for translation quality and AL  measures system delays. The evaluation results of all teams will be plotted on BLEU-AL two-dimensional coordinates. 
##### BLEU
We use [multieval](https://github.com/moses-smt/mosesdecoder/blob/master/scripts/generic/mteval-v13a.pl) to calculate BLEU.

##### AL
We use `python gen_rw.py < output_xxx/source_translation.txt > sample_rw.txt && python metricAL.py` to measure system delays. 

1. **gen_rw.py** is used to count Read/Write (R/W) operations during system execution. For each generated partial translation fragment, we count the number of source words read before it. For example, the R/W result of Table 3 is "R R R R R W W R R W R R W R R R R R W R R R W W R W R W". 
2. **metricAL.py**. According to the generated R/W file, we calculate the system latency according to metricAL.py, the output is a single value as AL.

---

# Important Dates
- **January 2020**: release of train and dev data
- **March 1st 2020 - March 26th 2020**: evaluation period
- **April 6th 2020**: system description paper due
- **May 4th 2020**: review feedback
- **May 18th 2020**: camera-ready paper due

All submission deadlines are 11:59 PM GMT-12 (anywhere in the world) unless otherwise noted.

---

# Challenge Chair
- Ruiqing Zhang (zhangruiqing01@baidu.com)
- Kaibo Liu (kaiboliu@baidu.com)

# Committee
- Ying Chen (chenying04@baidu.com), Data
- Zhiming Huang (huangzhiming01@baidu.com), Data
- Junjie Li (lijunjie02@baidu.com), Data
- Zhi Li (lizhi02@baidu.com), Data
- Boxiang Liu (boxiangliu@baidu.com), Data
- Hairong Liu (liuhairong@baidu.com)
- Mingbo Ma (mingboma@baidu.com)
- Di Song (songdi@baidu.com), Platform
- Lei Sun (sunlei18@baidu.com), Platform
- Meng Wang (wangmeng09@baidu.com), Platform
- Shuxia Zhang (zhangshuxia01@baidu.com), Platform
- Wenxi Zhang (zhangwenxi@baidu.com), Platform
- Baigong Zheng (baigongzheng@baidu.com), Data
- Renjie Zheng (renjiezheng@baidu.com), Data

---

# Contact
For any questions regarding our shared task, please use our [twitter page](https://twitter.com/autosimtrans), [github issues](https://github.com/autosimtrans/AutoSimTrans-Shared-Task-2020/issues), or email to [autosimtrans.workshop@gmail.com](autosimtrans.workshop@gmail.com). We are here to answer your questions and looking forward to your submissions!

---

###### [1] Chinese ASR by Baidu Speech.
