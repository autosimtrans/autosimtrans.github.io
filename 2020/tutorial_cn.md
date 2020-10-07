---
layout: main-anchor
title: Tutorial
order: 8 
collection: pages_2020_hide
permalink: /tutorial_cn
---


# A. 将训练好的模型打包成docker镜像
#### - [English](/tutorial)
#### - 中文
##### [1. 模型作者：用docker打包模型和代码](#1-想要将代码和模型打包到docker的模型作者)
##### [2. 测试用户：用docker作模型推理](#2-用docker镜像直接做推理的测试用户)


----

----

## 1. 想要将代码和模型打包到docker的模型作者
1. 利用[Dockerfile](https://github.com/autosimtrans/autosimtrans.github.io/raw/master/sp/Dockerfile_pt13.gpu)来建立docker镜像, 这里面将会用到`conda_specfile.txt`和`pip_requirement.txt`两个文件
```bash
conda activate <myenv>				# activate your virtual env
conda list --explicit > conda_specfile.txt 	# export packages installed via conda
pip freeze > pip_requirement.txt		# export packages installed via pip
```
2. 进入到工作目录，下载[Dockerfile](https://github.com/autosimtrans/autosimtrans.github.io/raw/master/sp/Dockerfile_pt13.gpu)(名为`Dockerfile_pt13.gpu`)
```bash
wget https://raw.githubusercontent.com/autosimtrans/autosimtrans.github.io/master/sp/Dockerfile_pt13.gpu
```
3. 将模型和推理代码**复制**到当前工作目录的一个文件夹内，例如命名为`<code folder>`。打开`Dockerfile_pt13.gpu`，编辑替换`OpenNMT-py`为你自己的代码和模型所在的文件夹`<code folder>`(将模型复制到当前工作目录的原因是docker配置文件的`CP`命令只支持相对路径)。本Dockerfile文件可以按需调整cuda/cudnn版本。
4. 创建docker镜像
```
docker build -t <ImageName:Tag> -f Dockerfile_pt13.gpu .
```
5. 创建本地文件并赋予写权限，用于挂载给docker镜像以便写入结果
```bash
mkdir decode && chmod 777 decode
```
6. 镜像创建完成后，运行推理以测试本镜像
```bash
nvidia-docker run -it -v <abs_path_to_your_data_dir>:/data -v <abs_path_to_your_local_decode_result_dir>:/decode <ImageName:Tag> bash
```
7. 现在已经进入到docker容器的bash进程中，本例中可以运行翻译脚本
```bash
python translate.py -model multi30k_model_step_100000.pt -src /data/wmt16-multi30k/test2016.en.atok  -tgt /data/wmt16-multi30k/test2016.de.atok  -replace_unk -verbose -output /decode/multi30k.test.pred.atok
```
8. 可以在`<abs_path_to_your_local_decode_result_dir>`(本地) or `/decode` (docker容器中)查看翻译结果并测试BLEU分数
```bash	
# in docker conatiner
perl tools/multi-bleu.perl /data/wmt16-multi30k/test2016.de.atok < /decode/multi30k.test.pred.atok
# result:
# BLEU = 35.50, 65.9/41.8/28.8/20.0 (BP=1.000, ratio=1.007, hyp_len=12323, ref_len=12242)
```

9. 注册用户后*将镜像上传到docker hub* **或者** *保存镜像到`tar`文件*
	- 注册一个DockerHub账户（dockerhub username), 创建一个新仓库（new repo），然后推送镜像
	```bash	
	docker tag <local-image:loacl-tagname> <dockerhub_username/new-repo:repo-tagname>
	docker login
	docker push <dockerhub_username/new-repo:repo-tagname>
	```
	- 保存镜像到`tar`文件，以便后续传送
	```bash
	# save image to `tar` file
	docker save -o <imageFile>.tar <local-image:loacl-tagname>
	# load `tar` file to image
	docker load < <imageFile>.tar
	```



## 2. 用docker镜像直接做推理的测试用户
1. 进入到工作目录，下载数据（用于test集盲测）
```bash
wget https://github.com/autosimtrans/autosimtrans.github.io/raw/master/sp/wmtdata.tar.gz
tar -zxvf wmtdata.tar.gz
```
2. 创建本地文件并赋予写权限，用于挂载给docker镜像以便写入结果
```bash
mkdir decode && chmod 777 decode
```
3. 运行GPU支持的docker，若本地没有会从线上抓取
```bash
sudo nvidia-docker run -it -v <abs_path_to_your_data_dir>:/data -v <abs_path_to_your_local_decode_result_dir>:/decode kaiboliu/onmt-py_en2de:torch1.3-gpu bash
```
4. 现在已经进入到docker容器的bash进程中，可以直接运行翻译脚本
```bash
python translate.py -model multi30k_model_step_100000.pt -src /data/wmt16-multi30k/test2016.en.atok -replace_unk -verbose -output /decode/multi30k.test.pred.atok
```
5. 可以在`<abs_path_to_your_local_decode_result_dir>`(本地) 或者 `/decode` (docker容器中)查看翻译结果并测试BLEU分数
```bash	
# in docker conatiner
perl tools/multi-bleu.perl /data/wmt16-multi30k/test2016.de.atok < /decode/multi30k.test.pred.atok
# result:
# BLEU = 35.50, 65.9/41.8/28.8/20.0 (BP=1.000, ratio=1.007, hyp_len=12323, ref_len=12242)
```

