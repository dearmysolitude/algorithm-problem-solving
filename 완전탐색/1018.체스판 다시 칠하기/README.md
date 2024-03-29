# 1018. 체스판 다시 칠하기

https://www.acmicpc.net/problem/1018

## 문제

지민이는 자신의 저택에서 MN개의 단위 정사각형으로 나누어져 있는 M×N 크기의 보드를 찾았다. 어떤 정사각형은 검은색으로 칠해져 있고, 나머지는 흰색으로 칠해져 있다. 지민이는 이 보드를 잘라서 8×8 크기의 체스판으로 만들려고 한다.

보드가 체스판처럼 칠해져 있다는 보장이 없어서, 지민이는 8×8 크기의 체스판으로 잘라낸 후에 몇 개의 정사각형을 다시 칠해야겠다고 생각했다. 당연히 8*8 크기는 아무데서나 골라도 된다. 지민이가 다시 칠해야 하는 정사각형의 최소 개수를 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N과 M이 주어진다. N과 M은 8보다 크거나 같고, 50보다 작거나 같은 자연수이다. 둘째 줄부터 N개의 줄에는 보드의 각 행의 상태가 주어진다. B는 검은색이며, W는 흰색이다.

## 출력

첫째 줄에 지민이가 다시 칠해야 하는 정사각형 개수의 최솟값을 출력한다.

## 풀이

브루트 포스를 사용한 최소값 산출 문제. for 문을 중복 사용하여 안 될 것 같았는데 68ms로 통과가 된다... 다른 부분은 읽어 보면 쉽게 알 수 있으므로 다음 부분만 살펴보자:

```python
        w_index = 0
        b_index = 0

        for a in range(i, i + 8): # 사각형 내부 확인하기
            for b in range(j, j + 8):

                if (a + b) % 2 == 0: # 사각형 내부 인덱스 합이 짝수의 경우 
                    if rock[a][b] != 'W':
                        w_index += 1
                    else:
                        b_index += 1
                else: # 홀수인 경우
                    if rock[a][b] != 'W':
                        b_index += 1
                    else:
                        w_index += 1

        cnt.append(w_index)
        cnt.append(b_index)
```

사각형(8 X 8) 내부에서 얼마나 색칠 할 수 있는지 확인하는 코드이다. 사각형 내부의 돌들을 살펴보는데,

- 내부 좌표의 합이 짝수/홀수인지 나누면 체스판 패턴으로 체스판의 돌들을 둘로 나눌 수 있다.
- w_index는 첫 돌이 흰색이어야 하는 경우에 칠해야 하는 돌의 갯수를
- b_index는 첫 돌이 검은색이어야 하는 경우에 칠해야 하는 돌의 갯수를 나타낸다.

좌표의 합이 짝수인 경우 / 홀수인 경우에 대하여, 각각 흰색/검은색인지 확인하여 칠해야 하는 경우 이 변수들에 1을 더한다. 첫 돌이 흰색인 경우/첫 돌이 검은색인 경우 모두에 대해서 산출하여 답 후보에 추가하는 것이다. 이후 과정에서 이 후보들 중 가장 작은 값을 출력한다.