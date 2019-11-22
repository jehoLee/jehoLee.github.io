---
title: "Algorithm (undergraduate course)"
use_math: true
toc: true
---

알고리즘이 왜 중요할까?

내 생각은 이렇다. 타 학부생들과 경쟁하는 경진대회, 해커톤 등에 참여하면 항상 "알고리즘 마스터" 학생이 등장하여 높은 점수를 획득한다. 우리는 그런 학생들을 코딩천재로 바라보지만, 그들은 단순히 머리가 좋아서가 아니라 수 많은 알고리즘 문제를 풀어보고 코딩한 경험들에 의해 실력을 키웠을 것이다(물론 천재도 있겠지만). 주어진 Computer science task를 해결하기 위해 task가 무엇인지 정확히 파악하고 그에 따른 Solution (algorithm)은 무엇이 적합한지 고민하는 과정에서, 알고리즘 문제를 많이 접해본 사람은 훨씬 수월하게 해결할 것이다.

이처럼 알고리즘을 많이 접해본 사람들은 새로이 주어진 Task의 해결책이 되는 알고리즘이 무엇인지 생각해낼 수 있는 힘을 갖고 있다. 또 알고리즘 구현 경험이 많은 사람들은 Task가 가진 조건에 맞는 최적의 프로그램을 개발할 수 있는 능력을 갖고 있다.

알고리즘 학부 수업에서 배운 내용을 정리함으로써, 알고리즘에 대한 개략적인 흐름과 내용을 다시금 공부한다.
정리하려는 알고리즘 기법의 분류는 다음과 같다.

- **Divide-and-Conquer**
- **Dynamic programming**
- **Greedy approach**
- **Backtracking**
- **Branch-and-Bound**

-----

## 1. Divide-and-Conquer

Divide-and-Conquer의 대표적인 알고리즘은 Merge sort가 있다. Merge sort를 생각해보면 전체 배열을 잘게 나누고(Divide) 나뉜 배열들을 재귀적으로 정렬한 뒤(Conquer) 합치는데(Combine), 전형적인 Divide-and-Conquer의 방식이다. Merge sort의 pseudo code를 보면,

```pseudocode
Mergesort(A[0...n-1])
 If n > 1
  copy A[0..n/2-1] to B[0..n/2-1]
  copy A[n/2..n] to C[0..n/2-1]
	Mergesort(B[0..n/2-1])
	Mergesort(C[0..n/2-1])
	Merge(B,C,A)
```

Merge sort를 위해 추가적인 B, C 배열이 필요하므로 n size 만큼의 공간이 더 필요하다. 따라서 Merge sort는 정렬 알고리즘 중에서 in-place sorting이 아닌 알고리즘에 속한다.

시간 복잡도 측면에서 배열을 나누는데 logN time이 걸리고, 재귀적으로 정렬된 sub-array인 B와 C를 합치는데(Merge) 걸리는 시간은 linear time (n)이 걸린다. 따라서 Merge sort의 시간복잡도는 O(NlogN)이다.

**Divide-and-Conquer 알고리즘은 Merge sort와 같이 재귀적으로 나뉜 sub-problem들이 서로 겹치지 않을 때 가장 효율적이다.** 그렇지 않은 예를 보면 이해가 빠른데, Fibonacci numbers를 구하는 문제가 그러하다. 피보나치 수열을 구하는 알고리즘을 구현하라하면 누구나 재귀적인 방식을 먼저 떠올릴 것이다. 하지만 Fibonacci(5)를 구하기 위해 Fibonacci(4)와 Fibonacci(3)을 재귀적으로 호출하게 되면, Fibonacci(2)에 대한 sub-problem을 두 번 계산하게 된다. 만약 n이 커진다면? 중복되는 연산이 많아져 효율성이 매우 나빠질 것이다.

이때 우리는 재귀적으로 Top-down approach를 적용하는대신, Bottom-up approach를 적용하여 중복되는 연산을 피할 수 있을 것이다. 이러한 경우 sub-problem을 먼저 해결하고 그 결과값을 따로 저장하여 중복 연산을 피할 수 있는 Dynamic programming을 사용할 수 있다.



## 2. Dynamic programming

우리는 피보나치 수열을 재귀적으로 풀기 위해, 


$$
Fibonacci(n) = Fibonacci(n-1)+Fibonacci(n-2)
$$


위 Recurrence relation (재귀식 혹은 점화식)을 구했고 알고리즘 구현에도 그대로 적용할 수 있다. 

Divide-and-Conquer는 위 재귀식을 그대로 사용하여 recursive한 방식으로 코드를 작성하기 때문에 sub-problem이 겹칠 수 있다. 하지만 Dynamic programming은 재귀식에 가장 하위의 instance부터 대입하여 풀어낸 뒤, 그 결과를 추가적인 table에 저장해두고 다음 instance의 결과를 구할 때 참조하는 방식을 취한다. 즉 Fibonacci(0)부터 풀어내고 그 결과를 배열에 따로 저장해둔 뒤, 다음 instance의 결과를 구할 때 이전에 구해둔 결과값을 참조하여 중복 연산을 피할 수 있는 것이다. 

이처럼 Dynamic programming은 Divide-and-Conquer와 마찬가지로 재귀식을 도출하여 특정 logic을 일반화시키는 것으로 시작하지만 재귀식을 그대로 코드에 적용하지 않고, 재귀식을 iterative 방식으로 구현함으로써 Bottom-up approach를 취할 수 있다.

다양한 알고리즘 기법을 적용할 수 있는 대표적인 문제인 Knapsack problem을 통해 Dynamic programming에 대해 자세히 설명하겠다.

- ***Knapsack problem***

  n개의 item이 주어지고, 각 item은 $$w_i$$ 만큼의 weight와 $$v_i$$의 value를 갖고있다.
  담을 수 있는 Knapsack의 총 용량은 W이다.

  이때, Knapsack의 용량 W를 넘지 않고 총 value가 최대인 item의 subset을 구하여라.

문제의 정의는 간단하다. 가장 쉽게 생각해볼 수 있는 해결 방안은 value가 가장 높은 item부터 순서대로 넣는 방법(Greedy)이 있지만 이 방법은 항상 최적의 해결책을 내놓지 못할 수 있다. Dynamic programming을 통해 Knapsack problem을 어떻게 해결할까? 

### 2-1. Knapsack problem solving by Dynamic programming

Knapsack problem을 Dynamic programming으로 해결하기 위해 먼저 Recurrence relation (재귀식)을 정의해야 한다. 이때 smaller instance의 결과를 larger instance가 참조할 수 있도록, 재귀식은 모든 instance에 대해 결과를 도출할 수 있는 형태이어야 한다. 즉, 현재 instance에서 *i*번째 item을 넣은 경우와 넣지 않은 경우 중 더 큰 값을 가진 경우를 결과값으로 채택하는 재귀식을 세워야한다.

재귀식을 구하기 위해 먼저, 특정 instance가 첫번째 item부터 *i* 번째 item까지, 그리고 *j* 만큼의 용량 (j <= W)으로 정의되고, 해당 instance의 최적의 결과값을 *F[i,j]*라고 하자. 

1. 현재 instance에서 *i*번째 item의 무게($$w_i$$)가 전체 용량(*j*) 보다 큰 경우 해당 item은 어떠한 경우에도 넣을 수 없으므로, 재귀식은 $$F(i-1, j)$$ 이다.
2. 현재 instance의 마지막 item인 *i*번째 item를 포함시키는 경우와 포함시키지 않는 경우 중 최적의 결과값을 취하는 재귀식, *max{*$$F(i-1,j-w_i)+v_i$$, $$ F(i-1, j)$$*}*

따라서 다음과 같이 나타낼 수 있다.


$$
F(i, j) =
\begin{cases}
\text{max}\{ F(i-1,j-w_i)+v_i,F(i-1,j) \}, & \text{if }j \ge w_i \\
F(i-1,j), & \text{if }j < w_i
\end{cases}
$$


Dynamic programming으로 Knapsack problem을 해결하기 위한 재귀식을 구했으니, 이제 알고리즘을 구현할 차례이다. 이 알고리즘은 위 재귀식을 사용하여 모든 instance의 결과값을 구하고 table에 따로 저장해야한다. 이렇게하여 모든 instance 마다 최적의 해를 구할 수 있을 뿐더러 그 과정에서 하위 instance의 결과값을 참조함으로써 시간 복잡도를 줄일 수 있을 것이다.

### 2-2. Memory Function

지금까지 Dynamic programming의 장점을 봤다. 하지만 Knapsack problem에서 *F(m, n)*, 즉 m개의 item과 n만큼의 용량에서 얻을 수 있는 최대 value를 구하기 위해 Dynamic programming은 $$m \times n$$ 개의 instance 결과값을 모두 구한다. 실제로는 모든 instance의 결과를 구할 필요는 없는데도, Dynamic programming은 solution을 구하기 위해 필요없는 instance의 결과도 계산한다. 이는 Bottom-up approach로 iterative (0부터 n까지 반복문)하게 알고리즘을 구현하기 때문이다. 이러한 단점을 보완하기 위해, 우리는 **Memory function** 기법을 적용하여 시간 복잡도를 좀 더 줄일 수 있다.

Memory function은 Recursive 방식으로 Top-down approach를 취하되, 계산한 instance의 결과값을 table에 저장하는 Dynamic programming의 장점도 취하는 방식이다. 다시 말해, 원하는 solution을 구하기 위해 top-down (recursively)으로 필요한 instance만 계산하고, 중복되는 계산이 없도록 instance 결과값을 table에 유지한다. Memory function을 사용하면 worst case의 경우 최종 결과를 얻기 위해 모든 instance를 봐야할 수 있으므로 기존 Dynamic programming과 복잡도가 동일하지만, 평균적으로 더 빠른 시간에 문제를 해결할 수 있다.

코드로 보면 이해가 쉬운데 Knapsack problem을 Memory function으로 해결하는 알고리즘은 다음과 같다.

```c
MFKnapsack(i,j)
  // F[]의 모든 요소는 -1로 초기화 되어있음
  if F[i,j] < 0 // 아직 결과값을 계산하지 않은 instance에 대해
    if j < Weights[i] 
      value = MFKnapsack(i-1, j)
    else
      value = max(MFKnapsack(i-1, j-Weights[i] + Values[i]), 
                  MFKnapsack(i-1, j))
				
    F[i,j] = value //instance의 결과값 table에 저장
  return F[i,j]
```

재귀적으로 구현하여 코드도 간단해지고, solution을 구하는 과정에서 중복된 연산 (recursive의 단점)과 필요없는 연산 (Dynamic programming의 단점)을 제거함으로써 시간 복잡도를 줄일 수 있다.



## 3. Greedy Algorithm

위 Knapsack problem을 해결하는 방안으로 가장 쉽게 떠오르는 idea는 가장 큰 value를 가진 item부터 순서대로 포함시키는 것이다. Greedy algorithm은 Dynamic programming과 마찬가지로 보통 Optimization problem을 해결하는데 적용되지만, 문제를 세부적으로 나누어 보지 않는다. 그리고 각 단계에서 최선의 선택을 하는 일련의 과정을 통해 solution을 얻는데, 이러한 방식은 구현하기 쉽지만 모든 문제에 대해 최적의 해결책을 내놓지 못 할수도 있다. 

반면에, Minimum Spanning Tree (MST)와 Shortest path problem은 Greedy approach를 적용하여 항상 Optimal solution을 도출하는 문제로 알려져있다.

![minimum-spanning-tree](/assets/minimum-spanning-tree.png)











































