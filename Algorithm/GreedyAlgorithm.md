# 목차
## [1. 개념](#1-개념)
## [2. 장단점](#2-장단점)
## [3. 적용 조건](#3-적용-조건)
## [4. 알고리즘 수행 과정](#4-알고리즘-수행-과정)
## [5. 예제](#5-예제)
---
# 1. 개념
    각 단계에서 최적의 선택이라고 생각되는 것을 택하여 문제를 해결해나가는 알고리즘
# 2. 장단점
## 2.1 장점
계산 속도가 빠름
## 2.2 단점
지역적으로 최선의 선택을 했다고 하여 전체적으로 최적의 선택을 했다고 보장하지 않음
# 3. 적용 조건
Greedy Algorithms이 잘 작동하는 문제는 대부분 탐욕스런 선택(greedy choice property)과 최적 부분 구조(optimal substructure)이라는 두 가지 특성을 가진다.
- 탐욕스런 선택(greedy choice property)  
이전 단계에서의 선택이 현재 단계에서의 선택에 영향을 미치지 않음
- 최적 부분 구조(optimal substructure)
문제(problem)에 대한 최적해가 부분 문제(sub-problems)에서도 최적해임
# 4. 알고리즘 수행 과정
1. 해 선택  
현재 상태에서 가장 최선이라고 생각되는 해를 선택
2. 적절성 검사  
현재 선택한 해가 전체 문제의 제약 조건에 벗어나지 않는지 검사
3. 해 검사  
현재까지 선택한 해 집합이 전체 문제를 해결할 수 있는지 검사하며, 전체 문제를 해결하지 못하면 1. 으로 돌아가 같은 과정을 반복
# 5. 예제
## [동전 개수의 최솟값 구하기](https://www.acmicpc.net/problem/11047)
**문제설명**  
~~~
준규가 가지고 있는 동전은 총 N종류이고, 각각의 동전을 매우 많이 가지고 있다.
동전을 적절히 사용해서 그 가치의 합을 K로 만들려고 한다. 이때 필요한 동전 개수의 최소값을 구하는 프로그램을 작성하시오
~~~
**제한사항**  
~~~
1 ≤ N ≤ 10
1 ≤ K ≤ 100,000,000  
~~~
**입력**
~~~
첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)
둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. (1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)
~~~
**출력**
~~~
첫째 줄에 K원을 만드는데 필요한 동전 개수의 최솟값을 출력한다.
~~~
<code style="background-color:#4D5357;">문제풀이</code>  
**① 그리디 알고리즘 활용 조건**  
입력값에서 뒤의 동전 가격 $A_i$가 이전 가격 $A_{i-1}$의 배수라는 조건에 의해 크기가 작은 동전들의 합은 큰 동전으로 대체되기 때문에 각 단계에서 무조건 큰 동전을 사용하는 것이 동전 개수를 최소화하는데 최적의 선택임  

**② 풀이 과정**  
i. K보다 작거나 같은 동전들 중 최댓값을 가지는 동전 탐색  
ii. 해당 동전의 합이 K보다 작거나 같을 때까지 반복  
iii. 해당 동전의 합이 K보다 작다면 나머지 값을 K로 갱신하여 나머지 값이 0이 될 때까지 ①, ② 과정을 반복하여 실행  

**③ 구현 코드**  

```java
import java.util.Scanner;

public class MinimumNumberOfCoins {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int K = sc.nextInt();
        int[] coins = new int[N];
        for (int i = 0; i < N; i++) {
            coins[i] = sc.nextInt();
        }
        int answer = 0;
        while (K != 0) {
            for (int i = N - 1; i >= 0; i--) {
                if (coins[i] <= K) {
                    answer += K / coins[i];
                    K %= coins[i];
                }
            }

        }
        System.out.println(answer);
    }
}
```

# 참고 문헌
- 김종관. 『Do it! 알고리즘 코딩 테스트: 자바 편』, 이지스퍼블리싱(2022), p196
- https://en.wikipedia.org/wiki/Greedy_algorithm