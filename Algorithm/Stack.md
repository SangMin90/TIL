# 1. 개념
~~~ 
후입선출(LIFO, Last In First Out) 방식으로 요소를 삽입(push), 삭제(pop)할 수 있는 자료구조
~~~
# 2. 특징
- 삽입과 삭제 연산이 한 쪽 끝(top)에서만 일어남
- 후입선출 자료구조이므로 가장 최근에 삽입된 값이 가장 먼저 삭제됨

# 3. 연산
## 3.1 push()
- stack의 top에 새로운 요소를 삽입하는 연산
- 빈 stack에 A, B, C라는 요소들을 삽입한다고 가정하면 다음 그림과 같다.
![image](https://user-images.githubusercontent.com/62678386/196026743-f0c5c8b4-de26-4fca-9437-54d002201e43.png)  
나중에 넣은 순서대로 각각 A, B, C가 stack의 top이 됨을 볼 수 있다.
## 3.2 pop()
- stack의 top에서 요소를 삭제하는 연산으로 top에 있는 요소의 값을 반환하며, stack이 비었다면 null을 반환한다.
- A, B, C를 포함하는 stack에서 top에 있는 요소를 제거한다고 가정하면 다음 그림과 같다.
![image](https://user-images.githubusercontent.com/62678386/196026870-e5310e48-f2d6-4b9a-92ee-0cc81c56273c.png)  
top에 있던 C가 삭제되면서 B가 top이 됨을 볼 수 있다.
## 3.3 peek()
stack의 top에 있는 요소를 제거하지 않고 조회만 하는 연산으로 top에 있는 요소를 반환하며, stack이 비었다면 null을 반환한다.
## 3.4 empty()
stack이 비어있는지 확인하는 연산으로 boolean 타입의 결과값을 반환한다.

# 4. 예제
**문제 설명**
~~~
1부터 n까지의 수를 스택에 넣었다가 뽑아 늘어놓음으로써, 하나의 수열을 만들 수 있다. 이때, 스택에 push하는 순서는 반드시 오름차순을 지키도록 한다고 하자. 임의의 수열이 주어졌을 때 스택을 이용해 그 수열을 만들 수 있는지 없는지, 있다면 어떤 순서로 push와 pop 연산을 수행해야 하는지를 알아낼 수 있다. 이를 계산하는 프로그램을 작성하라.
~~~

**제한 사항**  
- 변수 조건
$1 ≤ n ≤ 100,000$
- 시간 제한 : 2초

**입력**  
- 첫째 줄에 n이 주어진다. 둘째 줄부터 n개의 줄에는 수열을 이루는 1이상 n이하의 정수가 하나씩 순서대로 주어진다. 물론 같은 정수가 두 번 나오는 일은 없다.

**출력**  
입력된 수열을 만들기 위해 필요한 연산을 한 줄에 한 개씩 출력한다. push연산은 +로, pop 연산은 -로 표현하도록 한다. 불가능한 경우 NO를 출력한다.

<code style="background-color:#4D5357;">문제풀이</code>  
**풀이 과정**  
1) stack의 top에 있는 요소 ≤ 수열의 현재 값  
두 값이 같을 때까지 1씩 증가시키면서 stack에 삽입(push)하고 "+"를 문자열에 추가한다. 두 수가 같아지면 삭제(pop)한다.
2) stack의 top에 있는 요소 > 수열의 현재 값  
입력에서 주어진 수열을 생성할 수 없으므로 문자열을 "NO"로 초기화하고 출력하여 종료
3) 2)의 경우가 아닌 경우 오름차순 수열을 만들 수 있는 경우이므로 1) 과정을 통해 저장된 문자열을 출력

**ii) 설명**  
입력값이 n = 8, 수열 A = {4, 3, 6, 8, 7, 5, 2, 1}로 주어진 경우, 다음과 같이 진행된다.
![image](https://user-images.githubusercontent.com/62678386/196030178-4b6aa790-3ff3-44a3-bf21-09ef91c76294.png)

**iii) 구현 코드**  

```java
import java.util.ArrayDeque;
import java.util.Deque;
import java.util.Scanner;

public class StackSequence {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] A = new int[n];

        for (int i = 0; i < A.length; i++) {
            A[i] = sc.nextInt();
        }

        StackSequence sample = new StackSequence();
        System.out.println(sample.solution(n, A));

    }

    private String solution(int n, int[] A) {
        Deque<Integer> stack = new ArrayDeque<>();
        StringBuilder sb = new StringBuilder();

        int num = 1;
        for (int a : A) {
            if (num <= a) {
                while (num <= a) {
                    stack.push(num++);
                    sb.append("+\n");
                }
                stack.pop();
                sb.append("-\n");
            } else {
                if (stack.peek() == a) {
                    stack.pop();
                    sb.append("-\n");
                } else {
                    return "NO";
                }
            }
        }
        return sb.toString();
    }
}
```

# 참고 문헌
- 김종관. 『Do it! 알고리즘 코딩 테스트: 자바 편』, 이지스퍼블리싱(2022), p81-p85
- https://www.baeldung.com/cs/stack-data-structure\