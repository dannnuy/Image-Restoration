# Image-Restoration
주어진 데이터를 훈련 및 최적화하여 Descanning 성능이 높은 모델을 개발합니다. 하지만, gpu의 한계로 모델 파라미터 10M 미만으로 overfitting 및 underfitting 되지 않도록 모델의 목잡도를 잘 조절하며, test data 없이 학습을 시키는 것이 목적입니다.

## 1. 프로젝트 동기 (Motivation)

### 
- 저해상도 이미지를 고해상도로 변환하는 슈퍼 해상도(SR)
- 흐릿한 이미지를 선명하게 만드는 디블러링(Deblurring)
- 노이즈가 심한 영상에서 깨끗한 이미지를 복원하는 디노이징(Denoising)
- 의료 영상, 위성 영상, 감시 카메라 영상의 화질 개선

## 2. 모델 설명
# KBNet: Adaptive Image Restoration Model

### 📌 Introduction  
KBNet은 Supervised Learning(지도 학습) 방식으로 학습되는 이미지 복원 모델로, 손상된 입력 이미지를 고품질 이미지로 변환하는 것을 목표로 합니다. 기존 CNN 기반의 이미지 복원 모델은 고정된 필터(Fixed Filter)를 사용하여 모든 영역에 동일한 커널을 적용하는 반면, KBNet은 적응형 필터(Adaptive Filter)를 동적으로 생성하여 적용하는 방식으로 더 유연한 복원이 가능합니다.  

---

### 🔍 Model Architecture  

#### 1. Kernel Basis Attention Module (KBAM)
KBNet의 핵심은 Kernel Basis Attention Module(KBAM)으로, 입력 이미지에서 **Enhanced Feature Map**을 추출한 후, 픽셀별로 최적의 필터를 생성하는 구조를 갖습니다.  

#### 2. Adaptive Kernel Generation
- 여러 개의 학습 가능한 기본 커널(W)을 정의  
- 각 픽셀마다 **Fusion Coefficients(F)를 학습하여 적절한 필터 가중치를 동적으로 조합  
- 특정 영역에서는 노이즈 제거 필터, 다른 영역에서는 블러 제거 필터를 선택적으로 적용  

---

### 🎯 Learning Process  
KBNet은 입력 이미지(손상된 이미지)와 정답 이미지(고화질 원본 이미지) 간의 차이를 최소화하는 방식으로 학습됩니다.  

- Loss Function: L1 Loss 또는 Mean Squared Error(MSE) Loss  
- Optimization: 정답 이미지와 복원된 이미지의 차이를 줄이는 방향으로 학습  

이 방식은 전형적인 Supervised Learning으로, 모델이 고화질 이미지의 특징을 학습하여 복원 성능을 최적화합니다.  

---

### 🚀 Applications  
KBNet은 다양한 이미지 복원 작업에 활용될 수 있습니다.  
- 📈 Super-Resolution: 저해상도 이미지를 고해상도로 변환  
- 🛠 Denoising: 이미지 내 노이즈 제거  
- 🔎 Deblurring: 블러 처리된 이미지 복원  

---

### 📌 Conclusion  
KBNet은 기존 CNN 기반 모델보다 더욱 정밀한 복원이 가능하며, **적응형 필터 학습을 통해 이미지의 각 영역별 최적의 필터를 적용하는 방식으로 높은 성능을 제공합니다. 🚀  

## 3. 평가지표: Y 채널 기반 MAE(Mean Absolute Error)

이 프로젝트의 평가지표는 디스캐닝된(복원된) 이미지의 Y 채널 값의 평균에 대한 MAE(Mean Absolute Error)입니다.  

MAE는 예측값 \( \hat{Y}_i \)와 실제값 \( Y_i \)의 절대 차이의 평균으로 정의됩니다.  

<img width="500" alt="image" src="https://github.com/user-attachments/assets/0260f255-04bd-439b-896a-d90ea9e37d07" />


여기서 \( N \)은 전체 픽셀 수, \( Y_i \)는 원본 이미지의 Y 채널 값, \( \hat{Y}_i \)는 복원된 이미지의 Y 채널 값입니다.  

MAE 값이 낮을수록 원본과 복원된 이미지가 더 유사하며, 모델의 성능이 우수함을 의미합니다.




