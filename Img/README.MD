# 플레이어 블루 프린트
## Begin 이벤트
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/Sbegin.png)

Begin Play는 본격적인 게임을 시작하면서 일어나는 블루 프린트이다. 게임을 시작하기에 앞서서 체력과 총알을 배정하주고, 체력, 보호막, 총알을 보여주는 UI를 설정한다. 모든 설정이 끝나면 인벤토리를 확인할 수 있는 Widget도 추가한다.

## MAP
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/Smap.png)

M버튼을 누르게 되면 지도를 UI에 맵을 표시해 주는 기능이다. 플레이어는 현재 자신이 속한 층을 알고 있고 그 층에서 쓰게 되면 그 때의 층에서의 맵을 보여주게 된다. 이와 같은 방법은 인벤토리 I, 아이템들 그리고 튜토리얼을 보여주는 T에서도 같이 사용이 된다.

## 아이템 습득시
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/SItem.png)

현재 블루프린트는 HP아이템을 먹을 때의 예시이다. 아이템을 먹고 있으면 체력을 회복을 하고 그 다음 UI를 업데이트 해준다.

## 총 변경
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/Sgun.png)

총을 변경할 때도 마찬가지로 UI를 업데이트를 해주게 된다.

## 데미지 이벤트
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/SDamage.png)

플레이어가 공격 당했을 때의 이벤트이다. 만약 보호막을 가지고 있다면 보호막이 먼저 데미지를 받게 되고 보호막이 없으면 체력이 깍이게 된다.




# 인공지능 블루프린트

## 지역 순환
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/ERotation1.png)
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/ERotation2.png)

대부분의 적들은 미로에서 지정된 범위를 순찰을 하게 된다. 디테일을 통하여서 현재의 적의 위치를 정해 주게 된다. 이는 그 후 OverLap이 일어나면 Patrol 1번과 2번을 계속 돌게 된다. 그리고 그 지역으로 이동을 할 때에는 Walk Animation으로 적이 걷는 기본적인 애니메이션을 실행한다.

## 플레이어 발견
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/EPlayer.png)

플레이어를 발견하게 되면 플레이어를 따라오도록 설정을 한다. Pawn을 플레이어의 위치로 설정을 하게 된다. 그리고 각자 적 마다 플레이어를 발견하게 되면 하는 행동이 다르기 때문에 FindPlayer 함수를 만들어서 각자 하고 싶은 행동을 할 수 있게 하고 걸어서 올 수 있도록 애니메이션을 설정한다.

## 플레이어에게 공격 받을 때
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/EAtt.png)
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/EAtt2.png)

플레이어에게 공격을 받을 때의 상황이다. 현재의 체력을 기준으로 적의 행동이 나눠지게 됩니다. 공격 받아 더 이상 체력이 부족 할 경우 스파크와 함께 게임에서 소멸이 됩니다. 하지만 남은 체력보다 많을 경우 두 가지의 실행을 동시에 합니다. 플레이어에게 어디서 맞았든 플레이어를 즉시 발견하게 되고 플레이어를 발견 한 후의 행동을 시작합니다. 또 한가지는 플레이어에게 총알을 맞았으므로 맞았을 때의 애니메이션과 함께 잠시 멈추는 행동을 합니다. 그리고 다시 속도를 돌려 줘서 추적을 할 수 있도록 합니다.


## 사운드 감지
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/ESound.png)

적은 플레이어를 발견할 때만이 아니라 플레이어의 소리나 적이 플레이어를 발견했다는 소리를 듣게 되면 따라오게 됩니다. Noise를 발견하면 그 때 그 위치로 달려가게 됩니다.


## 상속된 적
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/EPar.png)

1번부터 4번까지는 모든 적에게는 기본 사항이 됩니다. 지금부터 적 마다 가지고 있는 특성을 부여하고자 합니다. 가장 먼저 Begin Play를 실행 하더라도 부모의 Begin Play을 실행 한 후에 실행을 할 수 있도록 합니다. 그리고 적 마다 의 애니메이션과 최대 속력을 설정을 할 수 있습니다.

## 노이즈 생성
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/ENoise.png)

SoundEnemy가 가지고 있는 특성입니다. 이 적은 플레이어를 발견을 하게 되면 그 위치에서 소리를 발생 시켜서 근처에 있는 모든 적을 부를 수 있습니다. 실행은 두 가지의 방식으로 할 수 있는데 가장 먼저 소리를 발생을 시킨 후 애니메이션을 실행합니다. 발견 할 때 마다 실행이 되 소리가 겹칠 수 있으므로 한번만 실행을 합니다. 또한 노이즈를 발생시킵니다. 노이즈는 적이 하면 인식을 하지 않으므로 플레이어가 노이즈를 생성한 것으로 판단하기 위해 FirstPersonCharacter에 노이즈를 발생할 위치 값을 보낸 후에 노이즈를 발생 시킵니다.

## 데미지를 주었을 때
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/EDam.png)

플레이어에게 공격 당했을 때 UI이다. 총의 종류마다 UI는 바뀌게 된다. 1번과 2번 총은 일반 총이기 때문에 십자가 모양이 나오지만 3번 총에게 맞으면 흰색 공들이 튀기게 된다.


# 플레이어 애니메이션

## 플레이어 애니메이션 이벤트 그래프
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/Pani.png)

플레이어로부터 계속적으로 변수를 받아서 사용이 된다. 플레이어의 변수를 받을 때마다 애님그래프가 바뀌게 된다.

## 애님그래프
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/Pani2.png)

플레이어의 애님그래프이다. 플레이어가 어떤 상태인지에 따라 변수를 받으면 어디로 가야되는 지 결정이 된다.



# 그 외 블루프린트
## 박스 콜린더 충돌 블루 프린트
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/Xbox.png)

플레이어가 문 앞에 있을 때의 상황에 문제를 풀거나 새로운 층에 올라가게되면 시간에 따라서 문을 움직일 수 잇도록 하는 블루프린트 이다.

## 아이템
![image](https://github.com/SmiteFLame/Unreal-3D-Game-19.1/blob/master/Img/Xitem.png)

아이템을 먹게 되면 Item마다 자신의 함수를 부른 후 플레이어의 변수값을 변동을 하게 된다. 그리고 아이템인 것처럼 보이기 위해서 계속 아이템은 돌고 있게 된다.




