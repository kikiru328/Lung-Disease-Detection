# Model
해당 프로젝트는 
[CheXNet](https://stanfordmlgroup.github.io/projects/chexnet/) 모델을 활용하였습니다.  
선택 이유는 다음과 같습니다.

- DenseNet은 의료 영상에서 정보 손실을 줄이며
- 전이 학습이 잘 작동합니다.
- CheXNet은 흉부 영상에서 벤치마크 모델로 사용됩니다.
- 동일하게 Chest X-ray를 사용해서 14개의 질환을 분류한 모델로서 동일한 의미를 가짐.

## 모델 구성 및 학습 전략

DenseNet121 구조를 백본으로 하는 CheXNet을 기반으로 모델을 구성하였습니다.  
최상위 fully connected layer는 제거하고, 아래와 같이 프로젝트 목적에 맞게 커스터마이징하였습니다:

- `include_top=False` 설정으로 DenseNet121을 feature extractor로 사용
- `GlobalAveragePooling2D`를 통해 flatten 대신 공간 정보 평균화
- 출력층은 `Dense(units=7, activation='softmax')`로 구성하여 6개의 폐 질환 및 정상 클래스 분류
- `weights=None`: 사전 학습 없이 NIA 데이터를 기반으로 처음부터 학습

> ※ 초기에는 ImageNet 가중치를 활용하지 않고 학습하였으며, 이후 실험에서는 fine-tuning 유연성을 고려한 구조로 설계되었습니다.  

> ※ 또한 Unet 기반 segmentation을 통한 폐 영역 전처리도 시도했으나, 성능 향상에 유의미한 차이가 없어 최종 구현에서는 제외하였습니다.

![Image](https://github.com/user-attachments/assets/6e9cc9ab-8d2c-4196-8e5c-6ecb10ca1af4)

## 모델 성능 비교

다양한 구조에 대해 동일한 전처리 조건에서 F1-score를 비교하였으며, **CheXNet 최종 버전**이 가장 높은 성능을 기록하였습니다.

| 모델명 |F1-Score|dataset|
|:---:|:---:|:---:|
|CNN|0.117|Segmentation+Crop|
|VGG16|0.213|Segmentation+Crop|
|InceptionV3|0.321|Segmentation+Crop|
|DenseNet169|0.435|Segmentation+Crop|
|ResNet50|0.376|Segmentation+Crop|
|MobileNet|0.231|Segmentation+Crop|
|CheXNetV1|0.45|Segmentation+Crop|
|CheXNetV2|0.49|Bitwise Image(Segmentation)|
|CheXNetV3|0.48|Original Image + CLAHE|
|CheXNetV4|0.6|Crop Image|
|**CheXNet Final**|**0.94**|**Original Image + CLAHE**|


