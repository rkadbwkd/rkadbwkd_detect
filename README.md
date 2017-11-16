# H1 Nodule Dection 


## introduction
  
   여러 슬라이스로 구성된 CT 이미지를 이미지연산을 통하여 폐 결절 부분을 검출합니다. 
   CT이미지는 횡단 이미지로 촬영되기에 여러 장의 슬라이스 파일이 있고 dicom package를 사용하여 각 슬라이스의 번호를 알 수 있습니다.
   CT 스캔을 읽은 후 결절 영역이 폐 내부에 있다는 것이 명백하기에 폐 구조를 세분화 .



## 개발환경 및 패키지

  - Python
  - numpy
  - scikit-image
  - scikit-learn
  - keras (tensorflow backend)
  - matplotlib
  - pydicom
  - SimpleITK
  
  
 
  

## Step 1 : CT 슬라이스 이미지 읽기 

  
  각 CT 스캔은 DICOM 형식으로 여러개의 2차원 슬라이스로 구성됩니다.
  첫번째 해야 될 일은 DICOM 패키지를 사용하여 CT 슬라이스의 정보를 확인 하고 시각화 하는 것입니다.
  CT 슬라이스를 시각적으로 직접 확인 할 수 있습니다.  
  
  DICOM 의 사용방법은 아래와 같습니다.

    변수 = dicom.read_file('파일경로')
    
    
![solarized palette](https://github.com/rkadbwkd/rkadbwkd_detect/blob/master/CT_Slice_Image.PNG)


========

  
  변수에는 .dcm 확장자를 가진 CT 슬라이스 정보가 저장됩니다
  그 후 공기부분의 픽셀 강도 값이 -2000이므로 -2000의 강도값을 0으로 업데이트 합니다
  
![solarized palette](https://github.com/rkadbwkd/rkadbwkd_detect/blob/master/Air_delect.PNG)
  
  
  
## Step 2 : Mask Image 만들기 / 폐의 분할

  CT 슬라이스를 dicom으로 읽으면 폐가 더 어두운 영역임을 확인 할 수 있습니다.
  폐의 밝은 부분은 혈관이나 공기입니다. Mask 이미지 만들기는 총 7단계로 진행 됩니다
  
### Step 2 - 1 : 이진화

  이미지처리에서 이진화란 어느 임계값을 기준으로 임계값보다 값이 큰 경우 0
  작은 경우 255의 값으로 만들어주어 흑/백색으로 이미지를 만듭니다.
  임계값은 604의 값을 사용하고 실험에서 발견 된 값으로 사용하였습니다.
  
  ![solarized palette](https://github.com/rkadbwkd/rkadbwkd_detect/blob/master/Binary.PNG)


### Step 2 - 2 : 이미지 테두리에 연결된 얼룩 제거

이진화 된 결과를 살펴 보게 되면 아래 부분에 유난히 튀는 부분이 있습니다.
이 부분을 제거 하기 위하여 clear_border라는 패키지를 사용하여 얼룩을 제거합니다




	  변수  = clear_border(input 변수)
	  
	  ![solarized palette](https://github.com/rkadbwkd/rkadbwkd_detect/blob/master/border.PNG)



### Step 2 - 3 : 이미지 레이블링

얼룩을 제거 한 후 이미지 레이블링을 합니다. 
이미지 레이블링이란 인접한 화소에 모두 같은 번호(Label)를 붙이고 연결되지 않은 다른 성분에는 다른 번호를 붙이는 것입니다.


![solarized palette](https://github.com/rkadbwkd/rkadbwkd_detect/blob/master/labeling.PNG)




### Step 2 - 4 : 레이블링 된 3개의 영역을 2개의 영역으로 축소

이미지 레이블링을 진행 후 레이블링 된 이미지를 다시 두개의 영역으로 구분합니다.

![solarized palette](https://github.com/rkadbwkd/rkadbwkd_detect/blob/master/border.PNG)





### Step 2 - 5 : 침식 및 닫힘 연산으로 hole 채우기


침식 연산은 테두리나 선 부분들이 얇아 지게 하는 연산입니다.
침식 연산 진행 후 닫힘 연산을 진행하여 작은 Hole을 채우는 작업입니다.

![solarized palette](https://github.com/rkadbwkd/rkadbwkd_detect/blob/master/step6.PNG)



### Step 2 - 6 :  원본 이미지에 Mask 입히기


위의 연산 결과로 만든 Mask 이미지를 원본 이미지에 씌웁니다


![solarized palette](https://github.com/rkadbwkd/rkadbwkd_detect/blob/master/SuperImpose.PNG)


## Step 3 : 3차원으로 확인 후 혈관 부분 제거




## Step 4 : 최종 결과 확인


















  
  

  







