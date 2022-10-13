# 목차
## [1. 개념](#1-개념)
## [2. 적용 조건](#2-적용-조건)
## [3. 알고리즘 수행 과정](#3-알고리즘-수행-과정)
## [4. 예제](#4-예제)
---
# 1. 개념
    두 개의 포인터로 문제에서 주어진 제약조건에 해당하는 범위(window)를 지정한 다음, 그 범위를 유지한 채로 이동(sliding)하여 문제를 해결하는 방식
# 2. 적용 조건
- 계산을 위한 범위가 고정적이어야 함
# 3. 알고리즘 수행 과정
1. **초기 결과값 계산**  
시작 위치에서 고정된 범위에 대한 초기 결과값 계산
2. **범위를 유지한 채로 이동하면서 결과값 계산**   
고정된 범위를 1씩 이동하면서 문제의 제약조건을 위배하지 않을 때까지 결과값 계산

# 4. 예제
**문제설명**  
~~~
크기가 N인 정수 배열이 있다고 할 때, K개의 연속적인 원소들의 최대 합을 구하여라
~~~
**입력**
~~~
첫째 줄에 N과 K가 주어진다.
둘째 줄에 N개의 정수가 주어진다.
~~~
**출력**
~~~
첫째 줄에 k개의 연속적인 원소들의 최대 합을 출력하라.
~~~
<code style="background-color:#4D5357;">문제풀이</code>  
**① 풀이 과정**  
i. 처음 K개의 연속적인 원소들의 합을 계산  
ii. 오른쪽으로 1만큼 이동하여 이전 단계에서 산출한 합에서 범위에 새로 포함된 원소의 값을 더하고 제외된 원소의 값을 빼서 새로운 합을 산출   
iii. 이전 구간에서의 합과 현재 구간에서의 합을 비교하여 더 큰 값으로 갱신  
iv. 배열의 범위를 벗어나지 않을 때까지 i~iii 번의 과정을 반복

**② 구현 코드**  

```java
import java.util.Scanner;

public class SlidingWindow {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int K = sc.nextInt();
        int[] A = new int[N];

        for (int i=0;i<N;i++) {
            A[i] = sc.nextInt();
        }

        System.out.println(getMaxSum(N, K, A))
    }

    static int getMaxSum(int n, int k, int[] A) {
        int maxSum = 0;

        // 초기 합 계산
        for (int i=0;i<k;i++) {
            maxSum += A[i];
        }

        int windowSum = maxSum;
        // 배열의 범위를 벗어나지 않을 때까지 반복 계산
        for (int i=k;i<n;i++) {
            windowSum = windowSum + A[i] - A[i - k];
            if (maxSum < windowSum) {
                maxSum = windowSum;
            }
        }
        return max;
    }
}
```

# 참고 문헌
- 김종관. 『Do it! 알고리즘 코딩 테스트: 자바 편』, 이지스퍼블리싱(2022), p67
- https://www.geeksforgeeks.org/window-sliding-technique/