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
