---
published: true
layout: post
author: me
title: Google AutoML Vision 사용법
category: AutoML
---
# How To Use Google AutoML Vision

AutoML Vision은 누구나 쉽게 Image Classification 및 Object Detection 커스터마이징 모델을 만들어 배포할 수 있습니다.<br>
온라인 배포 또한 가능하고 엣지 기기에서 사용할 수도 있습니다.

Google Cloud는 UI로 구성된 콘솔 이외에 Cloud Shell이라는 명령어 창을 사용할 수 있지만<br>
여기선 오직 콘솔로만 사용하는 방법을 기술했습니다.

## 1. Google Cloud 가입
가장 먼저 Google Cloud에 가입해야 합니다.

[Google Cloud AutoML](https://cloud.google.com/automl) 사이트에 들어가셔서<br>
구글 계정으로 로그인하시면 우측 상단에 콘솔 버튼이 있습니다.<br>
클릭합니다.

![automl1]({{site.baseurl}}/_posts/automl1.PNG)

![automl2]({{site.baseurl}}/_posts/automl2.PNG)

국가는 자신의 국가로 설정하고<br>
서비스 약관에 체크한 후 동의 및 계속하기를 누릅니다.

가입이 되었습니다.

## 2. 프로젝트 생성
Vision을 사용할 프로젝트를 하나 만듭니다.

![automl3]({{site.baseurl}}/_posts/automl3.PNG)

좌측 상단에서 프로젝트 선택을 누르면 창이 하나 뜹니다.<br>
새 프로젝트를 누릅니다.

![automl4]({{site.baseurl}}/_posts/automl4.PNG)

프로젝트 이름을 정하고 만들기를 누릅니다.

![automl5]({{site.baseurl}}/_posts/automl5.PNG)

우측에 다음과 같은 알림이 뜨면 성공입니다.<br>
프로젝트 선택을 누릅니다.

## 3. 협업을 위한 사용자 추가
이 프로젝트는 다른 사람들과 같이 사용하며 협업할 수 있습니다.

![automl6]({{site.baseurl}}/_posts/automl6.PNG)

탐색메뉴 > 홈 > 대시보드 > 프로젝트 정보 > 이 프로젝트에 사용자 추가를 누릅니다.

![automl7]({{site.baseurl}}/_posts/automl7.PNG)

새 구성원엔 추가할 사용자의 이메일을 적습니다.<br>
다양한 역할을 부여할 수 있습니다.<br>
여기선 편의를 위해 모든 권한을 가진 소유자로 주었습니다.<br>
알림 이메일을 전송할 수 있습니다.<br>
저장을 누르면 지정된 역할을 가진 사용자가 추가됩니다.<br>

![automl8]({{site.baseurl}}/_posts/automl8.PNG)

알림 이메일을 전송했다면 추가된 사용자는 다음과 같은 이메일을 받습니다.<br>
링크를 눌러 수락합니다.

![automl9]({{site.baseurl}}/_posts/automl9.PNG)

위 방법 이외에도 탐색메뉴 > ID 및 보안 > 액세스 > IAM 탭에서 사용자 추가 및 관리가 가능합니다.

## 4. 무료 평가판 활성화
Google Cloud는 기본적으로 유료 서비스기 때문에 무료 평가판을 사용할 것입니다.

![automl11]({{site.baseurl}}/_posts/automl11.PNG)

상단에 뜨는 무료 평가판 활성화 버튼을 누릅니다.

![automl12]({{site.baseurl}}/_posts/automl12.PNG)

약관에 동의하고 진행합니다.

![automl13]({{site.baseurl}}/_posts/automl13.PNG)

개인으로 사용할 것이기 때문에 개인으로 둡니다.<br>
주소를 입력한 후 진행합니다.

이후 결제 인증 정보를 입력합니다.<br>
유료 계정으로 전환하기 전까지는 크레딧을 전부 사용해도 결제가 되지 않으니 안심하세요.

모두 작성 후 무료 평가판 시작하기 버튼을 누르면 됩니다.

![automl14]({{site.baseurl}}/_posts/automl14.PNG)

## 5. AutoML API 사용

![automl10]({{site.baseurl}}/_posts/automl10.PNG)

탐색메뉴 > 인공지능 > Vision > 데이터 세트로 들어갑니다.

![automl15]({{site.baseurl}}/_posts/automl15.PNG)

AutoML 사용 설정을 누르고 기다리면 버튼이 시작하기로 바뀝니다. 눌러 시작합니다.

![automl16]({{site.baseurl}}/_posts/automl16.PNG)

새 데이터 세트 이름을 지정하고 모델 목표를 선택합니다.<br>
시험삼아 만드는 모델이기 때문에 단일 라벨 분류를 선택했습니다.

## 6. Dataset을 Cloud Storage에 업로드
학습에 사용할 Dataset을 업로드합니다.

![automl17]({{site.baseurl}}/_posts/automl17.PNG)

탐색메뉴 > 저장소 > Storage에 들어가 버킷 만들기를 누릅니다.

버킷은 고유한 이름을 가져야 합니다. 그룹이름_모델이름으로 하면 대부분 됩니다.

데이터 저장 위치는 Region에서 us-central1(아이오와)로 둡니다.

(잘은 모르겠지만 한국 지역에선 학습이 안됩니다.)

기본 스토리지 클래스 및 객체 액세스 제어 방식은 기존대로 놔두고 만들기를 눌러 계속합니다.

![automl18]({{site.baseurl}}/_posts/automl18.PNG)

파일 업로드를 눌러 학습할 사진을 업로드 합니다.

![automl19]({{site.baseurl}}/_posts/automl19.PNG)

같은 클래스에 해당하는 사진은 묶어 한 번에 이름을 변경해 위와 같이 지정해 주는 것이 좋습니다.

## 7. Dataset 라벨링 정보를 업로드
라벨링 정보를 주기 위해 엑셀 파일을 엽니다.

첫 행에는 set, image_path, label 순으로 적습니다.<br>
여기서 set과 label열은 없어도 됩니다.

![automl20]({{site.baseurl}}/_posts/automl20.PNG)

set은 학습용 TRAIN set, 검증용 VALIDATION set, 테스트용 TEST set을 사용합니다.<br>
AutoML은 사용자가 세트를 지정해주지 않으면 임의로 지정해주기 때문에 굳이 정해주지 않아도 됩니다.

image_path는 데이터 셋 사진의 경로입니다.<br>
만들어준 버킷의 이름을 <bucket_name>에 넣으시면 됩니다.

label은 라벨 이름입니다.

![automl21]({{site.baseurl}}/_posts/automl21.PNG)

위에서 학습용 사진 이름을 똑같이 지정했다면 다음과 같이 라벨링 데이터를 만들 수 있습니다.

![automl22]({{site.baseurl}}/_posts/automl22.PNG)

전부 완료했다면 CSV (쉼표로 분리) (*.csv) 형태로 저장합니다.

저장한 csv 파일을 6번과 동일 스토리지에 업로드 합니다.

[학습 데이터 준비](https://cloud.google.com/vision/automl/docs/prepare?hl=ko) 페이지를 참고했습니다.

## 8. Dataset 학습

![automl23]({{site.baseurl}}/_posts/automl23.PNG)

5에서 만든 Vision 데이터세트로 돌아와 스토리지에 csv로 저장된 라벨링 정보를 가져옵니다.

계속을 누르면 이미지 탭에 업로드한 학습용 사진들이 불러와집니다. (양에 따라서 로딩이 5 ~ 30분 정도 걸립니다.)

![automl24]({{site.baseurl}}/_posts/automl24.PNG)

모든 이미지가 준비되면 위 사진처럼 보입니다.<br>
라벨링이 제대로 되었는지 확인하고 학습을 진행합니다.

![automl25]({{site.baseurl}}/_posts/automl25.PNG)

csv 파일에 set열을 제외하고 넣었기 때문에<br>
AutoML이 임의로 학습용/검증용/테스트용 사진을 나눈 것을 확인할 수 있습니다.<br>
학습을 진행합니다.

![automl26]({{site.baseurl}}/_posts/automl26.PNG)

Google Cloud 온라인 예측을 사용하려면 Cloud hosted를, 엣지 모델로 배포하려면 Edge를 선택합니다<br>
텐서플로우 라이트 모델로 배포할 것이기 때문에 Edge를 선택하였습니다.<br>
높은 정확성을 원한다면 Higher accuracy를 선택하고, 빠른 인식을 원한다면 Faster predictions를, 균형잡힌 모델을 원한다면 Best tradeoff 를 선택합니다.<br>
학습시간을 AutoML이 권장해줍니다. AutoML은 단위시간당 8개의 노드를 동시에 사용합니다.<br>
따라서 8 node hour는 약 1시간입니다.<br>

![automl]({{site.baseurl}}/_posts/automl27.PNG)
![automl28]({{site.baseurl}}/_posts/automl28.PNG)

학습이 완료되면 여러 평가 항목들을 볼 수 있습니다.<br>
라벨별 테스트 세트의 참양성/거짓양성/거짓음성 결과 또한 확인할 수 있습니다.

![automl29]({{site.baseurl}}/_posts/automl29.PNG)

테스트 및 사용에서는 다양한 환경에서 사용할 수 있는 모델을 배포할 수 있습니다.
