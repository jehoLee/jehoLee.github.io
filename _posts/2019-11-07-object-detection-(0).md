---
title: "Tensorflow Object Detection API를 활용한 object identification (0)"
categories:
 - Object detection
toc: false
---

**Object detection**은 Deep learning을 활용하여 영상 또는 이미지에 존재하는 Target object에 대해 Classification(분류)하고 Localization(위치 파악)을 이루어 내는 Computer vision problem 중 하나이다. 자율주행차는 여러 센서와 카메라를 통해 확보한 데이터로 현 상황을 파악하여 주행한다. 자동차 주변의 상황이나 물체에 대해 파악하기 위해, 물리적인 센서의 데이터만으로는 한계가 있으며 영상 스트림을 처리하는 작업이 필수적이다. 이와 같이, 모바일/임베디드/IoT 등의 시스템을 통해 특정 문제를 해결하려 할때 Object detection을 포함한 Computer vision techniques는 매우 중요하다고 볼 수 있다.

우리는 Tensorflow를 통해 구현된 Object detection model을 쉽게 학습시키고 (가용한 GPU가 있어야 하겠지만..) 다양한 Application에 적용할 수 있다. Tensorflow는 유명한 Object detection model인 Faster R-CNN과 SSD model을 다양한 버전으로 제공하고 있지만, SSD와 더불어 빠른 예측 속도를 자랑하는 [YOLO](https://pjreddie.com/darknet/yolo/)는 제공하지 않는다.

Tensorflow Object Detection API와 관련된 포스트에서는 API를 사용하는 방법과 과정, 그리고 이 API를 통해 실제 문제에 응용하는 과정에서 알아낸 정보를 공유하고 기록하려 한다.

--------

**관련 블로그 포스트는 학부생이 약 2달 간의 연구 프로젝트를 통해 알아낸 정보를 바탕으로 작성하며, 다음과 같은 조건하에 특정 문제를 해결하려는 사람들에게 추천한다.**

1. 자신만의 이미지 또는 영상을 갖고 있으며, 해당 데이터를 통해 Object detection model을 학습시키려 한다.
2. Google cloud GPU가 아닌, 본인의 GPU (server 혹은 in-desktop)를 보유하고 있다.
3. Tensorflow Object detection API에서 제공하는 모델들의 성능을 정확도와 속도 측면에서 비교/분석하고, 자신의 데이터셋 또는 도메인에 적합한 모델을 선정하고 학습시키려 한다.

