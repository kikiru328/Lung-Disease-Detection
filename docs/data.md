# Data Detail

프로젝트에 사용된 경진대회 dataset과 전처리 과정을 설명합니다.

## 데이터 구성

- Chest X-ray: 총 4,000장 (정상 + 6개 질병, multi-class)

### classs 비율

| 질병명 | 이미지 개수| 비율|
|:---:|:---:|:---:|
|정상|1,000|25%|
|폐렴|1,000|25%|
|신생아 호흡곤란 증후군|640|16%|
|흉막삼출|484|12.1%|
|공기누출|409|10.23%|
|무기폐|343|8.58%|
|과다팽창|124|3.1%|
|**계**|4,000|100%|

## 전처리 과정

1. CLAHE 명암 향상

![Image](https://user-images.githubusercontent.com/60537388/146228675-cb7026b0-b91f-437a-8e60-1f02594f094c.png)

2. UNet Segmentation 학습 및 적용

![Image](https://user-images.githubusercontent.com/60537388/146231178-4fbab414-04f6-41d3-944a-1d7b544e10b7.png)

3. 폐 개수 2개 이하 이미지 삭제
4. Image Augmentation (4배 증강)
5. class weight 설정

※ 초기에는 Unet 기반 세그멘테이션 전처리도 실험하였으나,  
모델 성능 개선에 유의미한 영향을 주지 않아 최종 구현에서는 제외하였습니다.
