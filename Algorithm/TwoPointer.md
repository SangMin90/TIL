# 목차
## [1. 개념](#1-개념)
## [2. 시간복잡도](#2-시간복잡도)
## [3. 예제](#3-예제)
---
# 1. 개념
~~~
배열에서 두 개의 포인터를 이용해 위치를 기록하면서 연속된 특정 구간을 처리하는 기법
~~~
# 2. 시간복잡도
투 포인터의 시간 복잡도는 $O(N)$이며, 브루트 포스를 통해 문제를 해결하는 경우 $N$의 값이 크게 되면 시간 초과가 발생할 수 있기 때문에 투 포인터가 적절할 수 있다.

# 3. 예제
**문제 설명**
~~~
다음과 같이 5개의 자연수로 구성된 수열이 있다고 할 때,
합이 7인 부분 연속 수열의 개수를 구해보시오.
~~~
<p style="text-align: center;">
<img src="https://user-images.githubusercontent.com/62678386/194322675-968cb88b-4e30-4ab8-a840-0a0ebeaba7aa.png"
width="300" height="80">
</p>  

**제한 사항**  
~~~
시간 복잡도 : O(N)
~~~
<code style="background-color:#4D5357;">문제풀이</code>  
**i) 투 포인터 이동 원칙**  
~~~
① 시작점(start)과 끝점(end)의 인덱스를 0으로 가리킴  
② 현재 부분 합이 M과 같으면 카운트  
③ 현재 부분 합이 M보다 작거나 같으면 end를 1 증가  
④ 현재 부분 합이 M보다 크면 start를 1 증가  
⑤ end의 인덱스가 N이 될 때까지 ①~④의 과정을 반복  
~~~
**ii) 설명**  
① 초기 시작점(start)와 끝점(end)의 인덱스를 0으로 설정
![image](https://user-images.githubusercontent.com/62678386/194325770-8838a342-a947-4c1e-8114-1b72adbd4c8f.png)  
② 부분 합이 초기값인 $0(<M)$이므로 end를 $1$ 증가 
![image](https://user-images.githubusercontent.com/62678386/194326567-41578570-1ff9-4a1b-983b-2ebe89b4f78e.png)  
③ 부분 합이 $1(<7)$이므로 end를 $1$ 증가 
![image](https://user-images.githubusercontent.com/62678386/194327006-24175f7a-825d-487e-adf5-49661ed426c4.png)
④ 부분 합이 $4(<7)$이므로 end를 $1$ 증가 
![image](https://user-images.githubusercontent.com/62678386/194327006-24175f7a-825d-487e-adf5-49661ed426c4.png)
⑤ 부분 합이 $7(<=7)$이므로 count를 1 증가하고 end를 $1$ 증가 
![image](https://user-images.githubusercontent.com/62678386/194327382-72949bb8-b5bf-43d9-9e0e-f5f555088007.png)
⑥ 부분 합이 $9(>7)$이므로 start를 $1$ 증가 
![image](https://user-images.githubusercontent.com/62678386/194327857-fc39f98c-48fc-4f82-baf7-b64fbb13bfeb.png)
⑦ 부분 합이 $8(>7)$이므로 start를 $1$ 증가 
![image](https://user-images.githubusercontent.com/62678386/194328236-b65438b7-c95c-40b5-9a79-3b4b9fc27501.png)
⑧ 부분 합이 $5(<7)$이므로 end를 $1$ 증가 
![image](https://user-images.githubusercontent.com/62678386/194328648-7517f63e-0230-4f87-9311-842a2bc9eb4c.png)
⑨ 부분 합이 $7(<=7)$이므로 count를 1 증가하고 end 인덱스가 5이므로 종료
![image](https://user-images.githubusercontent.com/62678386/194329100-7fbf6996-086e-4eaa-afb2-288ad4408ac4.png)

따라서 합이 7이 되는 부분 수열의 개수는 2개