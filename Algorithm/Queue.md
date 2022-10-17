# 1. 개념
~~~ 
선입선출(FIFO, First In First Out) 방식으로 요소를 삽입, 삭제할 수 있는 자료구조
~~~
# 2. 구조
![image](https://user-images.githubusercontent.com/62678386/196106775-f44030ab-34b8-4637-ac4c-ac48d59495d7.png)
- rear : queue 자료 구조에서 가장 끝에 있는 데이터를 가리키는 영역
- front : queue 자료 구조에서 가장 앞에 있는 데이터를 가리키는 영역
# 3. 특징
- 삽입 연산은 rear에서 발생하며, 삭제 연산은 front에서 일어남
- 선입선출 자료구조이므로 가장 먼저 삽입된 값이 가장 먼저 삭제됨

# 4. 연산
## 4.1 add()
- queue의 rear에 새로운 요소를 삽입하는 연산
## 3.2 poll()
- queue의 front에 있는 요소를 삭제하는 연산으로 삭제되는 요소의 값을 반환하며, queue가 비었다면 null을 반환한다.
## 3.3 peek()
queue의 front에 있는 요소를 제거하지 않고 조회만 하는 연산으로 해당 요소를 반환하며, queue가 비었다면 null을 반환한다.
## 3.4 empty()
queue가 비어있는지 확인하는 연산으로 boolean 타입의 결과값을 반환한다.

# 4. 예제
**문제 설명**
~~~
N장의 카드가 있다. 각각의 카드는 차례로 1부터 N까지의 번호가 붙어 있으며, 1번 카드가 제일 위에, N번 카드가 제일 아래인 상태로 순서대로 카드가 놓여 있다.

이제 다음과 같은 동작을 카드가 한 장 남을 때까지 반복하게 된다. 우선, 제일 위에 있는 카드를 바닥에 버린다. 그 다음, 제일 위에 있는 카드를 제일 아래에 있는 카드 밑으로 옮긴다.

예를 들어 N=4인 경우를 생각해 보자. 카드는 제일 위에서부터 1234 의 순서로 놓여있다. 1을 버리면 234가 남는다. 여기서 2를 제일 아래로 옮기면 342가 된다. 3을 버리면 42가 되고, 4를 밑으로 옮기면 24가 된다. 마지막으로 2를 버리고 나면, 남는 카드는 4가 된다.

N이 주어졌을 때, 제일 마지막에 남게 되는 카드를 구하는 프로그램을 작성하시오.
~~~

**제한 사항**  
- 시간 제한 : 2초

**입력**  
- 첫째 줄에 정수 N(1 ≤ N ≤ 500,000)이 주어진다.

**출력**  
첫째 줄에 남게 되는 카드의 번호를 출력한다.

<code style="background-color:#4D5357;">문제풀이</code>  
**풀이 과정**  
1) queue의 front에 있는 요소를 삭제   
2) 그 다음 queue의 front에 있는 요소를 삭제하고, 삭제한 값을 queue에 새로운 요소로 추가 
3) 남는 카드가 1장이 될 때까지 1)~2)를 반복

**ii) 설명**  
입력값이 N = 6인 경우, 다음과 같이 진행된다.
![image](https://user-images.githubusercontent.com/62678386/196111318-13eaf75d-2cde-4650-85b5-68e36d83c942.png)

**iii) 구현 코드**  

```java
import java.util.LinkedList;
import java.util.Scanner;

public class Card2 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int N = sc.nextInt();

        System.out.println(getLastCard(N));
    }

    private static int getLastCard(int N) {
        LinkedList<Integer> queue = new LinkedList<>();

        for (int i = 1; i <= N; i++) {
            queue.add(i);
        }

        while (queue.size() > 1) {
            queue.poll();
            queue.add(queue.poll());
        }

        return queue.poll();
    }
}

```

# 참고 문헌
- 김종관. 『Do it! 알고리즘 코딩 테스트: 자바 편』, 이지스퍼블리싱(2022), p91-p93
- https://docs.oracle.com/javase/8/docs/api/