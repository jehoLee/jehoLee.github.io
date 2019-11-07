---
title: "Tensorflow Object Detection API를 활용한 object identification (1)"
categories:
 - Object detection
toc: true

---

모든 API를 사용하기 위해 환경설정이 필요하듯, Tensorflow Object Detection API를 사용하기 위한 환경설정 과정을 설명하려 한다. 설치는 **리눅스** 환경에서 진행한다.

###Setup Tensorflow Object Detection API

먼저 Object detection을 위해 가상 환경(Virtual envirionment)를 설정한 뒤 셋업/인스톨을 진행하기를 추천한다 (저는 컴퓨터에 이미 설치된 Python, Tensorflow 환경과 발생하는 충돌을 해결하기 위해 많은 시간을 썼습니다...). 설치와 환경설정에 대한 공식 문서는 [여기](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md) 를 참고하길 바란다.

###Installation via command line

가상 로컬 환경에 필요한 라이브러리를 설치하기 전에, 나는 다음과 같은 라이브러리/모듈을 전체 환경에 설치하였다.

1. Python (3.6.1)
2. Protobuf (3.5.1)
3. Cuda
4. Cudnn

Cuda, Cudnn은 GPU 사용을 위한 필수 라이브러리이다.

다음으로 가상 로컬 환경을 설정하기 위해 Virtualenv 라는 라이브러리를 설치해야하며, 파이썬 라이브러리를 설치하기 위해 **pip** 패키지를 사용한다.

```
pip3 install --user virtualenv
```

```
cd <your_working_dir>
```

```
virtualenv venv
```

venv는 가상 환경의 디렉토리 이름이다.

```
source venv/bin/activate
```

위 명령어를 입력하면 terminal의 working directory 형식이 (venv) 로 시작하게 되고 이는 가상 환경에 진입했음을 의미한다. 또한 가상 환경에서 벗어나려면 간단히 deactivate를 입력하면 된다.

가상 환경에 진입한 뒤, 필요한 라이브러리를 설치한다.

```
pip3 install tensorflow-gpu==1.12.0
```

tensorflow는 cpu, gpu 버전으로 나뉘며, 본 프로젝트에서는 gpu 1.12.0 버전을 사용했다.

```
pip install Cython
pip install contextlib2
pip install pillow
pip install lxml
pip install jupyter
pip install matplotlib
```

공식 홈페이지에서는 command에 --user flag가 있지만, 우리는 가상 환경에서 설치를 진행하므로 해당 flag는 필요없다.







