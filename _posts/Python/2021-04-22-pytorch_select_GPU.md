---
layout: post
title:  "[Python]Pytorch GPU 선택하기"
date:   2021-04-22
categories: [Python]
author : "Junny"
tags : [Python, Pytorch, gpu]
---
# [Python]Pytorch GPU 선택하기
<br>
## 버전정보

|항목|OS|Python|Pytorch|CUDA|cuDNN|
|------|--------|-----|-------|------|------|
|VERSION|windows 10|3.6.5|1.6.0|11.2.2|8.1.0|


> cuda 11, cuDNN 8을 기본적으로 설치했다는 가정하에 포스팅을 작성했습니다.

<br>
## nvidia-smi

nivida-smi 명령어를 사용하면 현재 GPU의 상태를 확인할 수 있다.

![nvidia-smi](/assets/image/python/nvidia-smi/gpu_status.png)

현재 GPU 2개가 있으며, GPU 번호는 0/1번이 있고 1번은 현재 사용중이다.

## Pytorch 명령어

Pytorch에서 cuda(GPU)를 사용할 때 유용한 명령어들이 있다.

```
import torch

print(torch.cuda.is_available())
print('Available devices ', torch.cuda.device_count())	# 사용 가능한 cuda(GPU) device의 갯수를 나타냄
print('Current cuda device ', torch.cuda.current_device())	#현재 사용중인 cuda의 device 번호를 알려줌
```
```
True
Available devices  2
Current cuda device  0
```

torch.cuda.set_device(number) 명령어를 통해 사용할 GPU의 번호를 변경할 수 있다.

```
torch.cuda.set_device(1)

print('Current cuda device ', torch.cuda.current_device())
```
```
Current cuda device  1
```


torch.cuda.get_device_name() 명령어를 통해 현재 사용중인 GPU의 모델명을 확인할 수 있다.

```
device = torch.device("cuda:0")

print(torch.cuda.get_device_name(device))
```
```
Tesla V100-PCIE-32GB
```



