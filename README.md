# Lung Disease Detection

본 프로젝트는 [AI 모델 개발 경진대회: 소아흉부 폐질환 진단 및 분류](http://aemasue.co.kr/layout/res/home.php?mid=40&go=pds.list&pds_type=1&start=0&num=11&s_key1=&s_que=) 경진대회에 참가하면서 시작되었습니다.  

소아 흉부 X-ray 영상을 기반으로 폐질환을 분류하는 모델을 개발하였고, 이후 성능 향상과 실사용성 확보를 위해 프로젝트를 지속적으로 개선해왔습니다.

다양한 이미지 데이터 처리를 통해 데이터셋을 구축하고, `CheXNet` 기반 모델에 학습하여 경진대회를 마무리, 2위를 수상하였습니다.

또한 실사용 `End-to-End` 서비스를 개발하기 위해 [RSNA 오픈 데이터셋](https://www.kaggle.com/c/rsna-pneumonia-detection-challenge)을 활용해 추가 학습을 진행하였고 `PyQt` 기반 GUI 까지 통합하여 프로젝트를 마무리했습니다.

<br/>

## 프로젝트 배경 및 목적

소아 폐 질환은 조기 진단이 생명과 직결되는 고위험 질환입니다. 어린이는 폐 기능이 미성숙하고 증상 표현이 어려워 질병 악화 속도가 빨르기 때문입니다. 또한 X-ray 영상 품질과 병변의 모호함으로 의료진의 정확한 진단이 어려운 경우가 있습니다.

이에 따라 본 프로젝트는 다음과 같은 배경을 해결하고자 경진대회에 참가, 개발하게 되었습니다.

- 소아 X-ray 영상의 해상도, 움직임, 병변 작음 등으로 영상 진단이 어려움
- 정확하고 빠른 AI 기반 진단 체계의 필요성

<br/>

## 기술 개요

- Dataset 1: Chest X-ray 경진대회 dataset
- Dataset 2: (추가) [RSNA Pneumonia Challenge dataset](https://www.kaggle.com/c/rsna-pneumonia-detection-challenge) 사용
- 전처리: CLAHE, UNet
- Model: CheXNet (DenseNet121 base)
- GUI: PyQt5 Desktop App

<br/>

### 데이터 처리 요약

- Chest X-ray 경진대회 dataset 사용
- [RSNA Pneumonia Challenge dataset](https://www.kaggle.com/c/rsna-pneumonia-detection-challenge) 사용
- 전체 데이터 구성 및 전처리: [자세히 보기](docs/data.md)

<br/>

### 모델 구조 요약

- Base: DenseNet121 (ImageNet pretraied)
- Output: 7-classes softmax (정상 + 6개 질환)
- 모델 세부 구조: [자세히 보기](docs/model.md)

#### CheXNet 모델 선택 근거:
- CheXNet은 DenseNet121 기반 모델로, 의료 영상에서 안정적인 성능을 입증한 구조.
- DenseNet 은 매 층의 feature map을 직접 전달받아 학습이 안정적.
- 학습 파라미터 수 대비 높은 성능, 파인튜닝에 적합한 구조라 생각, 선택

#### 모델 성능

- NIA Dataset Only
    - train: F1-score 0.94
    - test: F1-score 0.63

<br/>

## [GUI]
제작한 모델을 가지고 PyQT5를 이용하여 GUI를 제작했습니다. 제작된 내용은 다음과 같습니다. 시연영상은 위와 동일합니다.
![image](https://user-images.githubusercontent.com/60537388/146233852-82d176b9-8cd0-4a7b-8d02-b76c68f89e31.png)

<br/>

## 기술 스택
- python 3.10+
- Tensorflow
- OpenCV, PIL
- PyQt5
- Matplotlib, Seaborn, OpenCV

<br/>

# 수상
- **2021 소아흉부 폐질환 진단 및 분류 2위**
  
[내용증명] : [공모전수상.pdf](https://github.com/Pleasant-riot/Lung-Disease-Detection/files/7764519/default.pdf)  
![image](https://user-images.githubusercontent.com/60537388/147138310-e8096107-e371-4191-a792-998fa5c3b0ea.png)  

<br/>

# Contribute
본 프로젝트는 개인 연구 및 포트폴리오 목적으로 작성되었으며,
기여(코드, 이슈, 피드백) 모두 환영합니다.