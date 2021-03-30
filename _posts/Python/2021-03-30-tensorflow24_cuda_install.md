---
layout: post
title:  "[Python] windows tensorflow2.4 / cuda 설치"
date:   2021-03-30
categories: [Python]
author : "Junny"
tags : [Python, Tensorflow, Tensorflow-gpu, cuda11, cuDNN8]
---
# [Python] Tensorflow 2.4 / cuda 버전 확인 및 설치
<br>
## 버전정보

|항목|OS|Python|Tensorflow|CUDA|cuDNN|
|------|--------|-----|-------|------|------|
|VERSION|windows 10|3.6.5|2.4.1|11.2.2|8.1.0|


>Tensorflow 2.4 버전은 cuda 11버전과 cuDNN 8버전을 사용한다

<br>
## 설치 정보 링크

각 Tensorflow 버전마다 설치 정보는 [여기](https://www.tensorflow.org/install/source_windows#tested_build_configurations)를 확인하면 된다.

CUDA는 [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive)에 접속하면 릴리즈된 Toolkit 버전별로 다운로드 받을 수 있다.

cuDNN도 [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive) 릴리즈된 버전별로 확인하여 다운로드할 수 있다.<br><br>

## CUDA 설치 후 확인

CUDA를 설치했으면 환경변수가 잡혀있는지 확인한다.

[제어판] - [시스템] - [고급 시스템 설정] - [환경변수]에 다음과 같이 잡혀있으면 된다.<br><br>
![cuda_env](/assets/image/python/cuda-install/cuda_env.png)

<br>
## cuDNN 설치

cuDNN을 다운로드 받았으면, cuDNN의 압축을 해제하여 CUDA 설치파일 경로에 덮어씌운다.

일반적으로 CUDA의 설치경로를 변경하지 않았으면 다음과 같이 위치한다. 해당 위치에 덮어쓰기하면 된다.<br>
```
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.2\
```

<br>
## Tensorflow 사용

Anaconda 혹은 python이 설치 되어있으면 확인이 편하다.

필자는 Jupyter notebook으로 진행했다.

```
! nvidia-smi
```

설치된 GPU의 상태를 확인하는 명령어이다. CUDA가 정상적으로 설치되었으면, 아래와 같은 그림이 나타난다<br>
![GPU_STATUS](/assets/image/python/cuda-install/nvidia_smi.png)

그래픽 카드가 2개 설치되어있어 2개가 나타나는 그림이다.

tf의 버전과 gpu가 사용가능한지 알아보는 방법은 다음과 같다.
```
import tensorflow as tf
from tensorflow import test
print(tf.__version__)
print(test.is_built_with_cuda() )
print(test.is_gpu_available())
```
```
2.4.1	# tensorflow version
True	# cuda 설치 여부
True	# gpu 사용 여부
```

tensorflow 2.x 버전부터는 gpu가 포함되어 설치되어 있으므로 tensorflow-gpu를 별도로 설치하지 않아도 된다.

설치된 device의 목록을 호출하여 확인하는 방법은 다음과 같다.
```
from tensorflow.python.client import device_lib 
print(device_lib.list_local_devices()) 
```

```
[name: "/device:CPU:0"
device_type: "CPU"
memory_limit: 268435456
locality {
}
incarnation: 9417018013122351439
, name: "/device:GPU:0"
device_type: "GPU"
memory_limit: 31753514624
locality {
  bus_id: 1
  links {
  }
}
incarnation: 14893248518782020408
physical_device_desc: "device: 0, name: Tesla V100-PCIE-32GB, pci bus id: 0000:00:06.0, compute capability: 7.0"
, name: "/device:GPU:1"
device_type: "GPU"
memory_limit: 31753514624
locality {
  bus_id: 1
  links {
  }
}
incarnation: 4355644207921533187
physical_device_desc: "device: 1, name: Tesla V100-PCIE-32GB, pci bus id: 0000:00:07.0, compute capability: 7.0"
]
```

이 상태로 모델링을 학습하게 되면 GPU를 사용하여 학습하게 된다.

![using gpu](/assets/image/python/cuda-install/using_gpu.png)

tensorflow 2.x 버전부터는 gpu가 포함되어 설치되어 있으므로 tensorflow-gpu를 별도로 설치하지 않아도 된다.