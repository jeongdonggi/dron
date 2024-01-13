# 2022 미니드론 경연 대회
이미지 처리 및 드론 제어

## 프로젝트 소개
크로마키 내부에 있는 원을 통과 후 나오는 표식에 따라 드론은 제어

## 개발 기간
* 2022.07.04~2022.07.14

## 멤버 구성
팀장: 임재욱 - <https://github.com/jaeuklim><br>
팀원: 김주연 - <https://github.com/zukite><br>
팀원: 정동기

## 개발 언어
![MATLAB](https://img.shields.io/badge/MATLAB-FC6D26?style=flat&logo)

## Github Repository
#### Github - <https://github.com/jaeuklim/Jangsu> (private)

## 주요 기능
#### 1. frame의 rgb값을 hsv로 변경
색상 검출이 좀 더 쉬움
#### 2. 픽셀의 합을 통하여 드론 위치 변경
픽셀 값이 치우쳐저 있는 방향으로 움직여 드론이 크로마키 중간에 올 수 있도록 위치 조정
#### 3. 크로마키와 동일 선상에 있을 수 있도록 각도 조정
frame에서 검출한 크로마키의 왼쪽 모서리의 x값의 차를 통해 각도 조정
#### 4. 거리에 따른 이동 거리 지정
크로마키와 멀 수록 멀리 보냄
#### 5. 원 검출 및 중심 찾기
크로마키 내부에 있는 원을 찾은 후 통과를 위해 중심점을 찾아 드론 위치 조정
#### 6. 표식 확인
표식 색상에 따라서 드론이 각도를 조정하거나 착륙

## 원의 중심 검출 테스트 결과
<img width="1009" alt="test" src="https://github.com/jeongdonggi/dron/assets/100845304/49e838af-1db9-4995-9837-e738c9f014d9">

위의 사진과 같이 빨간색 점으로 원의 중심이 찾아진 모습을 볼 수 있다.

## 개인 내용

전체적인 코드 업데이트는 [정동기] 파일에 있다.

전체적으로 개인 코딩으로 코드를 전체적으로 구현한 후 모여서 업데이트를 하였다.

전체 코드에서 개인적으로 혼자서만 구현한 코드가 있다.
### 3. 크로마키와 동일 선상에 있을 수 있도록 각도 조정
이 부분은 개인의 힘으로 구현하였다.
#### pgonCorners - <https://kr.mathworks.com/matlabcentral/fileexchange/74181-find-vertices-in-image-of-convex-polygon>
![pgoncorners](https://github.com/jeongdonggi/dron/assets/100845304/f9bd3ac3-a3f1-41e2-ae27-9cc87357a83e)

여기서 pgonCorners란 다각형 이미지의 모서리를 구하는 함수이다.

#### 코드 업데이트
1. 코너를 구한 후 4개가 구해지지 않으면 드론을 위로 보내고 뒤로 보낸다.
   - 카메라가 아래에 있기 때문에 전체적인 사진을 찾기 위해 드론을 이동하였으나 그럼에도 구하지 못하는 경우가 생겼다.
  
2. 코너를 구한 후 4개의 코너를 구했을 때 2개 이하가 검출되면 드론을 위로 보내고 뒤로 보낸다. 3개만 검출된 경우 구해지지 않은 코너의 위치 값을 카메라의 끝 부분으로 지정하고 그 값과 옆에 있는 모서리 의 y값의 차를 이용하여 값을 구하였다.
   - 아래 사진에서 맨 아래 빨간 점의 y축의 차를 통해 좌우로 드론의 각도를 움직이면서 코너가 4개가 찍힐 수 있도록 해준다.
<img width="545" alt="image" src="https://github.com/jeongdonggi/dron/assets/100845304/ac435d2c-7142-4ea3-a726-8d407257d1d1">
 - 값을 돌리더라도 만약 드론이 가깝다면 결국 결과가 나오지 않게 된다.

4.  코너를 구한 후 크로마키 왼쪽 변의 두 개의 모서리가 나오지 않는다면 드론을 뒤에서 위로 보내고, 만약 구해진다면 두 점의 x축의 차의 값이 정해진 값보다 작아질 때까지 왼쪽 또는 오른쪽으로 드론이 이동 시킨다.
   - 이 방법을 통하여 가까울 때에도 값이 제대로 나올 수 있도록 하였다. 실제로 테스트 시 제대로 드론이 이동하는 모습을 보여주었다.

## 결과 및 느낀점

#### 대회 결과
본선 전 날에 리허설에서는 3번까지 통과를 하였기에 본선은 충분히 통과할거라 생각하였다. 하지만 대회가 코로나로 인해 코드만 github에 올려서 따로 코드가 어떤식으로 돌아가고 어느 부분에서 오류가 나는지 모르겠지만 본선에서 드론이 제대로 문제를 수행하지 못하는 일이 발생하였다.

#### 느낀점
초면의 팀원들과의 팀 프로젝트는 처음이었다. 또한 MATLAB이라는 언어도 처음 보는 언어였기 때문에 실제로 공부를 해야하는 부분이 꽤 많았다.

팀 프로젝트를 진행하면서 팀원들 간의 의견을 조율하는 방법과 협업을 어떤 식으로 한지 작게나마 느낄 수 있었던 것 같다.

실제로 내가 본선에서 구현한 코드는 [정동기] 파일에 들어가 있다.
