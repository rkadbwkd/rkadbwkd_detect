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
  
  변수에는 .dcm 확장자를 가진 CT 슬라이스 정보가 저장됩니다
  그 후 공기부분의 픽셀 강도 값이 -2000이므로 -2000의 강도값을 0으로 업데이트 합니다







