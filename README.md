# -algorithm-implementation
## 왕실의 나이트
```
row=int(input_data[1])
col=int(ord(input_data[0]))-int(ord('a'))+1
```
코딩에서 행열의 기준은 세로가 행(row), 가로가 열(col) 이다.

입력을 a2, c2 와 같이 입력받는다.

input_data[0]은 알파벳이고 input_data[1]은 숫자이다.

따라서 세로행은 그대로 입력받는다.

가로행은 알파벳을 아스키코드로 변환한후 그 값에서 a를 빼준다. 인덱스가 1부터 출발하므로 추가적으로 1을 더해주면 원하는 좌표 값을 얻을 수 있다.

```
for step in steps:
  next_row=row+step[0]
  next_col=col+step[1]
  if next_row>=1 and next_col>=1 and next_row<=8 and next_col<=8:
    count+=1
```

row가 세로이므로 좌표에서 값이 변하는건 x축이다 따라서 step(x,y)에서 첫 번째에 해당하는 

step[0]을 다음 스텝으로 더해간다. col도 마찬가지로 y축이므로 step[1]을 더해간다.

조건이 8x8 체스판이기 때문에 1과 8이하의 조건을 만족해야 경우의수를 누적할 수 있다.


## 게임 개발

#### 설명

1. 현재 위치에서 현재 방향을 기준으로 왼쪽 방향(서쪽) 부터 차례대로 갈 곳을 정한다

2. 캐릭터의 바로 왼쪽 방향에 아직 가보지 않은 칸이 존재한다면, 왼쪽 방향으로 회전한 다음 왼쪽으로 한칸을 전진한다. 왼쪽 방향에 가보지 않은 칸이 없다면, 왼쪽 방향으로 회전만 수행하고 1단계로 돌아간다.

3. 만약 네 방향 모두 이미 가본 칸이거나 바다로 되어 있는 칸인 경우에는, 바라보는 방향을 유지한 채로 한 칸 뒤로가고 1단계로 돌아간다. 단, 이때 뒤쪽 방향이 바다인 칸이라 뒤로 갈 수 없을 경우에는 움직임을 멈춘다.

----------

#### 입력
+ 첫째 줄에 맵의 세로 크기 n과 가로크기 m을 공백으로 구분하여 입력
+ 둘째 줄에 게임 캐릭터의 좌표 (x,y)와 바라보는 방향 d가 서로 공백으로 구분하여 주어진다. 방향 d의 값은 0: 북, 1: 동, 2: 남, 3: 서
+ 셋째 줄부터 맵이 육지인지 바다인지에 대한 정보 입력. 0은 육지 1은바다이며 맵의 외곽은 항상 바다로 되어있다
+ 처음에 게임 캐릭터가 위치한 칸의 상태는 항상 육지이다
#### 출력
+ 첫째 줄에 이동을 마친 후 캐릭터가 방문한 칸의 수를 출력

----------
#### 코드 
+ 리스트 컴프리헨션 문법을 사용하여 2차원 리스트 초기화
```
d=[[0]*m for _ in range(n)]
```
방문한 위치를 저장하기 위한 맵을 생성하여 0으로 초기화

+ 북,동,남,서 방향 정의
```
dx=[-1,0,1,0]
dy=[0,1,0,-1]
```

+ 왼쪽으로 회전
```
def turn_left():
  global direction
  direction -=1
  if direction == -1:
    direction=3
 ```
 서쪽이 3번이기 때문에 모든 방향을 탐색할 경우 다시 서쪽인 3번으로 초기화
 
 + 시뮬레이션 시작
 ```
 while True:
  turn_left
  nx=x+dx[direction]
  ny=y+dy[direction]
```
왼쪽으로 회전 후 현 위치에 이동할 좌표를 더해줌

+ 회전한 이후 정면에 가보지 않은 칸이 존재하는 경우 이동
```
if d[nx][ny]==0 and array[nx][ny]:
    d[nx][ny]=1
    x=nx
    y=ny
    count+=1
    turn_time=0
    continue
```
만약 이동할 좌표가 가보지않은 곳이고 바다가 아닐 경우 방문처리를 해주고 현 좌표를 변경해준다.

+ 회전한 이후 정면에 가보지 않은 칸이 없거나 바다인 경우
```
 else:
    turn_time+=1
```
+ 네 방향 모두 갈 수 없는 경우
```
 if turn_time==4:
    nx=x-dx[direction]
    ny=y-dy[direction]
    if array[nx][ny]==0:
      x=nx
      y=ny
    else:
      break
    turn_time=0
 ```
 뒤로 갈 수 있다면 이동하고 바다라면 멈춘다
