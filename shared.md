---
layout: main-anchor-2021
title: Shared Task
order: 3
collection: pages_2021
permalink: /shared
---

### About the challange
- [Registration](#registration)
- [Schedule](#schedule)  
- [Participants and requirements](#participants-and-requirements)
- [Entry method and rules](#entry-method-and-rules)
- [Award](#award)
- [More welfare](#more-welfare)
- [Supplement](#supplement)
- [Anti-cheating instructions](#anti-cheating-instructions)
- [Chair and Committee](#challenge-chair)  
- [Contact](#contact)  

### About the tasks
- [Dataset](#dataset)  
- [Task classification](#task-classification)
- [Task Input](#task-input)
- [Task Output](#task-output)
- [Baseline System](#baseline-system)
- [Submission Guidance](#submission-guidance)
- [Announcements](#announcements)
- [Evaluation Metrics](#evaluation-metrics)


---


# Registration

Please register your team through this [AI Studio](https://aistudio.baidu.com/aistudio/competition/detail/62?lang=en) Platform.

---

# Schedule

Time | Schedule
-|-
2020/12/28 00:00:00 | Registration and Release of data
2021/01/31 23:59:59 | End of registration
2021/02/20 00:00:00 | System Submission
2021/03/07 23:59:59 | System submission close
2021/03/15 00:00:00 | System Description Due
2021/04/15 00:00:00 | Notification of Acceptance
2021/04/26 00:00:00 | Camera-ready Papers Due

All submission deadlines are 11:59 PM GMT-12 (anywhere in the world) unless otherwise noted.


---
# Participants and requirements
##### Participants
This competition is opened to the whole society, and has no restriction on age, identity and nationality. Individuals, institutions of higher learning, research institutions, enterprises and start-up teams in related fields can register for this competition. Those who have access to the task and data in advance cannot participate in the competition. Other employees can participate in the ranking of the competition but cannot receive any award.

##### Requirements
Individual or team participation is supported. The maximum number of participants in each team is 5. Cross-unit team is allowed, but each person can only join one team.


# Entry method and rules

1. All contestants must register on the Baidu Brain AI Studio platform;  
1. All contestants must ensure that the information submitted during registration is accurate and valid. All eligibility and bonus payment is based on the information submitted;  
1. All contestants can form a team on the “My Team” page after registration. Each team must designate a team leader, and the total number of team members shall not exceed 5; Note: The list of team members is not allowed to be changed after the registration deadline. Please select each team member carefully;  
1. The names of the teams shall not be set in violation of Chinese laws and regulations or public order and good customs, and the names of the participating teams shall not be used as “Baidu Official”, “Paddle official”, “official baseline” or other words. If the offending team fails to change its name after receiving a warning from the competition organizer, the competition organizer has the right to dismiss the team;  
1. Each contestant can only join one team. Once a contestant is found to have joined more than one team by registering multiple accounts, the relevant team will be disqualified;  
1. All contestants must not use the marked data from any other channel except the data set provided by the organizer;  
1. The participating teams can upload the predicted results of the test set at any time during the competition. Each team has only one chance to submit the predicted results. All teams are requested to submit the predicted results cautiously;  
1. QQ group: 744528691.  

---
# Award

There are 3 tracks in this competition, and each track will generate one first, one second and one third prize as follows:

Award |  Quantity | Bonus
-|-
First prize  |1  | $1,000
Second prize |1  | $800
Third prize  |1  | $500

##### Notes
1. All the above bonus are pre-tax amounts;
1. Excellent contestants will have the opportunity to share or publish their papers at NAACL Workshop.


# More welfare

1. Free computing power
    - Baidu Brain AI Studio will provide free 100h Tesla V100 GPU power card for all contestants. You can get the application address of the power card on the datasets tab after registration.
    - You can get 10h GPU computing power every day by running project in AI Studio, and can get up to 70h GPU computing power every week.
1. Official baseline
    - PaddlePaddle will provide an official baseline for all contestants, which can be obtained on the datasets tab after registration.

# Supplement
**Fair competition**: competitors are not allowed to copy others’ works, exchange answers or use more than one trumpet in the competition. If found guilty, the results will be cancelled and dealt with seriously.

**Organization statement**: the organizing committee reserves the right to adjust and modify the rules of the competition, the arrangement of the competition, the right to judge and deal with cheating in the competition, and the right to withdraw or refuse awards to the participating teams that affect the organization and fairness.

**Baseline model**: the baseline model is for the reference of competitors, and can be improved upon. Competitors cannot directly submit the prediction structure of the baseline model; If the submission structure is highly similar to the predicted results of the baseline model, the result will be cancelled.

**Property**: entries (including, but not limited to algorithm, model, etc.) the intellectual property rights owned by the competitors, the organizing committee reserves the right to the entries, work related, team information used for propaganda materials, publications, designated and authorized media release, the official web site to browse and download, exhibitions (including tour) activities such as projects, the priority right to cooperation organization unit.

# Anti-cheating instructions
1. Participants are forbidden to register for multiple accounts, and their scores will be cancelled and seriously dealt with if found.
1. Participants are prohibited from using rules loopholes or technical loopholes outside the scope of the assessment of technical ability to improve the performance ranking. If found, the performance will be cancelled and seriously dealt with.
1. For those who have access to relevant data of the competition, their submitted works will not be included in the rankings and awards.
1. AI Studio will collect contestants’ information, codes, models and system reports for performance evaluation, competition notification and other relevant competition matters.

---

# Dataset

### Training set and Development set

For Chinese-to-English translation, we provide Baidu’s BSTC data set:
1. Training data: 70h of Chinese speech videos, manual transcription results and English translation data for training model;
1. Development data: 16 speeches and their corresponding streaming transcription results, for evaluating the effectiveness of your model.

For English-to-Spanish translation, we provide the following data sets:
1. Training data: UN data set for training model;
1. Development data: the streaming transcription results corresponding to UN data, for evaluating the performance of your model.


### Testing Data
Our testset will not be released. You are required to upload your whole system and environment. Within 24 hours after you submitting your system, we'll publish the evaluation results on the competition website.

At test time, the systems are expected to receive different file formats based on the system types. For text-to-text translation systems, the inputs are streaming source text of gold transcripts and the outputs are corresponding simultaneous translation results. For speech-to-text translation systems, the inputs are speech audio files and the outputs are corresponding simultaneous translation results.

---


# Task classification

Our challenge includes 3 tasks on Chinese-to-English translation (Zh->En) and English-to-Spanish translation (En->Es). Participants can choose to join one or more tasks. 

1. Zh->En Translation, input: streaming transcription
2. Zh->En Translation, input: audio file
3. En->Es Translation, input: streaming transcription

### Task Input

There are two types of inputs involved:

1. **Streaming transcription** provides the golden transcripts in streaming format, where each sentence is broken into lines whose length is incremented by one word until the end of the sentence.
<span hidden>2. **Streaming ASR** provides the realtime streaming ASR results<sup>[[1](#1-chinese-asr-by-baidu-speech)]</sup>. During the ASR, errors may occur, and the recognition result of one line may be modified compared with the previous ones. Note that there is no punctuation predicted during ASR. </span>
2. **Audio**: You can also choose to use your own ASR system with the audio as input.

An example of the three types of input is illustrated in Table 1.  We process input data into streaming format to evaluate the system delay (refer to [Evaluation](#evaluation)).

Streaming Transcript	|	Audio
-|-
大	|	<audio controls="controls" style="height: 20px;width: 170px;"><source type="audio/mp3" src="assets/105-[AudioTrimmer.com].wav"></source><p>Your browser does not support the audio element.</p></audio>
大家	|	
大家好	|	
大家好！	|	
欢	|
欢迎	|	
欢迎大		|	
欢迎大家		|	
欢迎大家关		|	
欢迎大家关注		|	
欢迎大家关注UNIT		|	
欢迎大家关注UNIT对		|	
欢迎大家关注UNIT对话		|	
欢迎大家关注UNIT对话系		|	
欢迎大家关注UNIT对话系统	|	
欢迎大家关注UNIT对话系统的	|	
欢迎大家关注UNIT对话系统的高	|	
欢迎大家关注UNIT对话系统的高级	|	
欢迎大家关注UNIT对话系统的高级课	|	
欢迎大家关注UNIT对话系统的高级课程	|	
欢迎大家关注UNIT对话系统的高级课程。	|	

<div style="text-align: center;">
    Table 1. Illustration of two types of input
</div>

---

# <span id="evaluation">Evaluation</span>

### Task Output
For all the three tasks, you output only one text file containing source sentences and translations. The Table 2 is an example with streaming transcript input. Your system needs to decide when to translate given the input, and to write the translation after corresponding source. Your translations will be concatenated with **SPACEs** to evaluate BLEU. 

Note that:
1. the left part (streaming source) should **NOT** be modified in streaming transcription tasks. 
1. For Zh-En translation with audio input, you also have to output this source-translation file, with the left part as your recognition source and right part as the corresponding translation. 

Streaming Transcript    |   Translation
-|-
大家  |   
大家好 |   
大家好！    |   Hello everyone!
欢   |
欢迎  |   
欢迎大     |   
欢迎大家        |   Welcome
欢迎大家关       |   
欢迎大家关注      |   to
欢迎大家关注UNIT      |   
欢迎大家关注UNIT对     |   unit
欢迎大家关注UNIT对话        |   
欢迎大家关注UNIT对话系       |   
欢迎大家关注UNIT对话系统  |   
欢迎大家关注UNIT对话系统的 |   dialog system
欢迎大家关注UNIT对话系统的高    |   
欢迎大家关注UNIT对话系统的高级   |   
欢迎大家关注UNIT对话系统的高级课  |   
欢迎大家关注UNIT对话系统的高级课程 |   
欢迎大家关注UNIT对话系统的高级课程。    |   advanced courses.

<div style="text-align: center;">
    Table 2. Illustration of output file
</div>



---

### Submission Guidance
##### A. System Submission

You have two ways to submit your system:

1. **For AISTUDIO Project owner**: You can use the calculation resources for free (one V100 card for each participant) if your system ONLY RELIES ON PADDLEPADDLE as the deep-learning framework. The free resources are provided by AISTUDIO. In this case, you can submit your system by specifying your projectID on AISTUDIO. Note that using other deep-learning platforms (as Tensorflow or Pytorch) is forbidden by AISTUDIO. 
2. **For Other submitters**, you are required to submit your docker system, along with your own implementation of specific APIs for input and translation output. We will evaluate all the submissions on our environment. Please refer to the [tutorial page](https://autosimtrans.github.io/tutorial) if you need help to convert your model to docker image, or train in docker container.

There are some requirements for your uploaded system:

1. script <b>run.sh</b>: the interface to execute your translate program. 
For text-to-text tasks, use  
<span hidden>`sh run.sh < streaming_asr.txt > output_asr/source_translation.txt` or  </span>
`sh run.sh < streaming_transcription.txt > output_transcript/source_translation.txt`;  
For audio-to-text task, use  
`sh run.sh < audioid.wav > output_audio/source_translation.txt` 

2. directory <b>output_xxx</b>: your environment should have a directory named `output_transcript` or `output_audio`, depends on the task you involved in. You can also prepare multiple output directories of them, if you participate in multiple challenge tasks. 
3. file <b>output_xxx/dev_translation.txt</b>: we suggest you to put the source-translation result file of the development set under the corresponding task output directory, with the file name as `output_xxx/dev_translation.txt`. This is very helpful for us to eliminate the execution problems of your system.

Unless coming across system execution error, each participant has only one chance to submit on each task.


##### B. Paper Submission

Scientific and system description papers will be submitted through [**this Link**](https://www.softconf.com/naacl2021/AutoSimTrans2021) by Monday, March 15, 2021, 11:59pm [UTC-12h]. Paper should be formatted according to the [NACCL 2021 format guidelines](https://2021.naacl.org/calls/papers/) and be of 4 to 8 pages of content plus additional pages of references. Accepted papers will be published on-line in the NACCL 2021 proceedings and will be presented at the conference either orally or as a poster.

### Announcements

There is only one chance for each team to submit this contest. Please submit your prediction carefully.



---

### Evaluation Metrics
Following previous work, we evaluate simultaneous translation results based on BLEU and [AL (average lagging)](https://github.com/SimulTrans-demo/STACL). BLEU is the measurement for translation quality and AL  measures system delays. The evaluation results of all teams will be plotted on BLEU-AL two-dimensional coordinates. 
##### BLEU
We use [multieval](https://github.com/moses-smt/mosesdecoder/blob/master/scripts/generic/mteval-v13a.pl) to calculate BLEU.

##### AL
We use `python gen_rw.py < output_xxx/source_translation.txt > sample_rw.txt && python metricAL.py` to measure system delays. 

1. **gen_rw.py** is used to count Read/Write (R/W) operations during system execution. For each generated partial translation fragment, we count the number of source words read before it. For example, the R/W result of Table 2 is "R R R R R W W R R W R R W R R R R R W R R R W W R W R W". 
2. **metricAL.py**. According to the generated R/W file, we calculate the system latency according to metricAL.py, the output is a single value as AL.

##### Baseline System

Here is a baseline system for the Simultaneous Machine Translation based on [PaddlePaddle](https://github.com/paddlepaddle/paddle) and [STACL](https://arxiv.org/abs/1810.08398):
- [**souce code**](https://github.com/autosimtrans/SimulTransBaseline) on github
- [**notebook**](https://aistudio.baidu.com/aistudio/projectdetail/315680) with running environment, covering pretrained models and eval scripts
- [**docker image**](https://hub.docker.com/r/autosimtrans/stacl_paddle) with environment, pretrained models and eval scripts

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
- Renjie Zheng (renjiezheng@baidu.com), Data

---

# Contact
For any questions regarding our shared task, please use our [twitter page](https://twitter.com/autosimtrans), [github issues](https://github.com/autosimtrans/AutoSimTrans-Shared-Task-2020/issues), or email to [autosimtrans.workshop@gmail.com](autosimtrans.workshop@gmail.com). We are here to answer your questions and looking forward to your submissions!

---

