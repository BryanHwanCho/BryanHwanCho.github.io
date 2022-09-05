---
title: Orange3를 이용하여 데이터 분석 해보기-2탄
author: iHihi
date: 2022-08-30 22:08:00 +0900
categories: [포스트, AI공부]
tag: [data, orange, post]
comments: true
---

---  
## 오렌지3를 이용해서 데이터 분석을 해봅시다 (2탄)  
저번 시간에는 오렌지3가 무엇인지, 설치를 해보는 과정을 가져보았다.  
이번시간에는 오렌지3를 이용해서 과일의 데이터를 분석해보고 처리해보는 시간을 가져보도록 하겠다.  
  
---  

## 과일 데이터 확인하기
일단 임의로 과일 데이터를 구해주었다.  
혹시나 같은 데이터를 이용하고 싶은 사람은 캐글에서 fruits360을 이용하면 된다.  
![fruit360](/img/post_img/orange2/fruits360.PNG)  
데이터를 받으면 다양한 과일들이 다양한 각도로 촬영한 사진들이 많이 있는 것을 확인할 수 있는데,  
여기서 이 많은 데이터를 이용하기에는 무리가 있으니까 원하는 과일 5개를 골라서 각 과일마다 10개의 사진만 선별해서 따로 저장해주었다.  
![choose](/img/post_img/orange2/choose.PNG)  
이제 선별한 Orange3 프로그램을 들어가보자. 이때 관리자 권한으로 들어가주자.  
![main](/img/post_img/orange2/orangemain.PNG)  
여기서 NEW를 눌러줘서 새로운 오렌지파일을 만들어주고  
우리가 처리할 사진을 오렌지에 불러와줄건데 오렌지에서 이미지를 다루기 위해서는 Add-on에서 Image Analytics를 추가해줘야 된다.  
![addon](/img/post_img/orange2/analytics.PNG)  
오렌지 위의 메뉴 ```Options -> Add-on```으로 가서 검색창에 image-analytics를 검색한 뒤에 설치해주고 재실행하면 된다.  
재실행해주면 왼쪽에 Image-Analytics라는 항목이 새로 생긴 것을 확인 할 수 있는데, 여기서 Import Image를 클릭해주면 흰색 빈 바탕에 Import Images라는 아이콘이 추가 된 것을 확인 할 수 있다.  
아이콘을 클릭해주면 아래 화면처럼 파일을 추가하는 창이 뜨는데 여기서 우리가 선별했던 사진의 파일을 선택해보자.  
![filesel](/img/post_img/orange2/fileselectplz.PNG)  
선택해주면 No image set selected에서 50 images / 5 categories 로 바뀐 것을 확인할 수 있는데,  
50이미지 5개 카테고리를 찾았다는 것임을 의미한다.  
![select](/img/post_img/orange2/selected.PNG)  
이미지가 잘 불러와졌는지 확인해보자.  Image Viewer를 가져온 뒤에 아래 gif처럼 서로 연결해줄 수 있다.  
![viewer](/img/post_img/orange2/viewer.gif)  
연결해준 뒤에 뷰어를 눌러주면 사진들이 있는 것을 확인할 수가 있다.  
![fruits](/img/post_img/orange2/fruits.PNG)  
사진들을 데이터테이블화 시켜보자.  
![data](/img/post_img/orange2/connectdata.PNG)  
연결해주고  
![table](/img/post_img/orange2/data.PNG)  
눌러보면 테이블을 확인할 수 있다.  
  
---  
## Image Embedding 다루기  
이미지 Embedding은 우리가 이번에 해볼 Classification Model을 구현해보기 위해 거쳐야 하는 과정인데, 이미지 자체로는 기계학습을 하기에 어려움이 있는 unstructured data 이기 때문에 Embedding 과정을 통해 이미지를 수치화 시켜 structured data로 변환시켜 기계학습을 할 수 있도록 해줘야 한다.  
  
오렌지3에서 Image Analytics에서 Image Embedding 위젯을 가져와서 우리가 이용할 사진이 Import되어 있는 Import Images 위젯과 연결한 다음 아래 이미지처럼 Data Table을 연결시켜 Embedding을 통해 변환된 Data를 확인할 수 있도록 연결해보자.  
![embedding](/img/post_img/orange2/embedding.PNG)  
그렇게 Data Table을 열어 확인을 해보면 기존의 Table옆에 n0에서 n2047까지 convert된 data를 확인할 수가 있다.  
![n2047](/img/post_img/orange2/n02047.PNG)  
이제 이 data를 통해 Claasfication Model를 구현해보도록 하겠다.  
  
---  
## Classification Model 구현  
이제 Classification Model을 구현을 해보도록 하자.  
먼저 Embedding을 거친 Data에서 Model 항목에서 Logistic Regression 위젯을 가져와 Image Embedding을 연결해주자.  
![regression](/img/post_img/orange2/regression.PNG)  
이렇게 연결해주면 Logistic Regression 모델에서 학습을 하게된다.  
  
---  
## Classification Test  
이제 Test Data를 가지고 Classification Model이 잘 작동하는지 Test를 해보도록 하자.  
먼저 사전에 받아놨던 과일 이미지에서 선정했던 카테고리의 사진과 동일한 종류의 과일사진 1개씩을 가져와 Test를 위한 Data를 준비해주도록 하자.  
집에 똑같은 종류의 과일이 있다면 사진을 찍어서 테스트해봐라 필자는 집에 과일이 없어서 해보지는 않았다 ㅋㅋ.....  
![testdata](/img/post_img/orange2/testdata.PNG)  
선정해줬으면 오렌지3에서도 이미지를 Import해주고 똑같이 Embedding 해주도록 하자.  
![testimport](/img/post_img/orange2/testimport.PNG)  
이제 Prediction을 통해 결과값을 Predict해보도록 하자.  
Model 항목에 Prediction위젯을 가져와서 Logistic Regression에 연결하고 Test Data에 연결된 Image Embedding에 연결하면 확인할 수가 있다.  
아래 사진을 참고하여 연결해주자.  
![orange](/img/post_img/orange2/orange.PNG)  
전체적인 오렌지 화면이다.  
이렇게 연결되어있으면 정상적으로 결과값이 나오는 것을 확인할 수 있다.  
이제 결과값을 확인해보도록 하자.  
Prediction 위젯을 누르면,  
![predict](/img/post_img/orange2/prediction.PNG)  
Logistic Regression에 표시되어 있는 과일과 Test Data의 Categories의 과일이 잘 매칭되어 있는 것을 보았을 때,  
사진이 카테고리에 맞게 잘 분류되었다!  
  
---  
## 글을 마치며
이번 글에서는 Orange3를 이용하여 사진을 분류하는 모델을 구현해보았는데,  
복잡한 코드없이 간단히 드래그앤드롭으로 어렵지않은 난이도로 구현해볼 수 있었다는 것을 확인해볼 수 있었다.  
원래 저번 글 다음으로는 여행일지를 적으려고 했지만 어쩌다보니 오렌지3를 다루게 되었다 ㅋㅋ.....  
그리고 맥OS로 이주하면서 jekyll환경이나 각종 다양한 개발환경을 맞추느라 애를 먹은 덕분에,  
글 업로드가 늦어지긴 했다 (~~핑계거리~~)  
다음 글은 진짜루 여행일지로 뵙도록 하겠다.  
  
## 오늘도 긴 글 읽어주셔서 감사합니다!!
