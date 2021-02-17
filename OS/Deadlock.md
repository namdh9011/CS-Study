# 데드락(Deadlock, 교착 상태)이란?

------

  ### 데드락(Deadlock)

![deadlock-1](https://github.com/Songwonseok/CS-Study/blob/main/OS/images/deadlock-1.PNG)



![deadlock-2](https://github.com/Songwonseok/CS-Study/blob/main/OS/images/deadlock-2.jpg)

  운영체제에서 데드락(교착상태)이란, 시스템 자원에 대한 요구가 뒤엉킨 상태입니다.

  즉, **둘 이상의 프로세스가 다른 프로세스가 점유하고 있는 자원을 서로 기다릴 때 무한 대기에 빠지는 상황**을 일컫습니다.

------

  ### 데드락(Deadlock)의 발생조건

  데드락이 발생하기 위한 조건은 크게 4가지로 말할 수 있습니다.

  - 상호 배제
    - **한 번에 프로세스 하나만 해당 자원을 사용할 수 있다**. 사용 중인 자원을 다른 프로세스가 사용하려면 요청한 자원이 해제될 때까지 기다려야 한다.
  - 점유 대기
    - 자원을 최소한 하나 보유하고, 다른 프로세스에 할당된 자원을 점유하기 위해 대기하는 프로세스가 존재해야 한다.
  - 비선점
    - 이미 할당된 자원을 강제로 빼앗을 수 없다(비선점).
  - 순환 대기
    - 대기 프로세스의 집합이 순환 형태로 자원을 대기하고 있어야 한다.

------

  ### 데드락(Deadlock)의 해결법

  데드락의 해결법을 크게 3가지로 분류할 수 있습니다.

  - 데드락이 발생하지 않도록 **예방**(prevention) 하기
  - 데드락 발생 가능성을 인정하면서도 적절하게 **회피**(avoidance) 하기
  - 데드락 발생을 허용하지만 데드락을 **탐지**(detection)하여, **데드락에서 회복**하기

------

  ### 데드락 예방(Prevention)

  **데드락의 발생조건 4가지 중 하나라도 발생하지 않게 하는 것**이 데드락을 예방하는 방법입니다. 즉, 각각의 조건을 방지(부정)하여 데드락 발생 가능성을 차단합니다.

  - 자원의 상호 배제 조건

    방지 : 한 번에 여러 프로세스가 공유 자원을 사용할 수 있게 합니다.

    - 그러나 추후 동기화 관련 문제가 발생할 수 있습니다.

  - **점유 대기 조건 방지** : 프로세스 실행에 필요한 모든 자원을 한꺼번에 요구하고 허용할 때까지 작업을 보류해서, 나중에 또다른 자원을 점유하기 위한 대기 조건을 성립하지 않도록 합니다.

  - **비선점 조건 방지** : 이미 다른 프로세스에게 할당된 자원이 선점권이 없다고 가정할 때, 높은 우선순위의 프로세스가 해당 자원을 선점할 수 있도록 합니다.

  - **순환 대기 조건 방지** : 자원을 순환 형태로 대기하지 않도록 일정한 한 쪽 방향으로만 자원을 요구할 수 있도록 합니다.

  이러한 조건을 방지해서 데드락을 예방하는 방법은 **시스템의 처리량이나 효율성을 떨어트리는 단점**이 발생할 수 있습니다.

  다음에 살펴볼 데드락 **회피법**은 예방법보다는 **조금 덜 제한적인 방법**으로 예방법의 단점을 일부 해결할 수 있습니다.

------

  ### 데드락 회피(Avoidance)

  데드락 회피법에서는 **Safe sequence, Safe state** 등이 키워드입니다.

  시스템의 프로세스들이 요청하는 모든 자원을, 데드락을 발생시키지 않으면서도 차례로 모두에게 할당해 줄 수 있다면 **안정 상태**(safe state)에 있다고 말합니다.

  그리고 이처럼 특정한 순서로 프로세스들에게 자원을 할당, 실행 및 종료 등의 작업을 할 때 **데드락이 발생하지 않는 순서를 찾을 수 있다면**, 그것을 **안전 순서**(safe sequence)라고 부릅니다.

  반면 **불안정 상태**는 안정 상태가 아닌 상황을 말합니다. 즉, **데드락 발생 가능성이 있는 상황**이며, **교착 상태(데드락)는 불안정 상태일 때 발생**할 수 있습니다. 불안정 상태가 교착 상태보다 좀 더 큰 집합입니다.(즉, 교착 상태가 불안정 상태의 부분집합)

  이처럼 회피 알고리즘은 **자원을 할당한 후에도 시스템이 항상 Safe state에 있을 수 있도록 할당을 허용**하자는 것이 기본 특징입니다.

  이러한 특징을 살린 알고리즘으로 유명한 것이 `은행원 알고리즘` 입니다.

  #### 은행원 알고리즘(Banker’s Algorithm)

  다익스트라가 제안한 기법으로, 어떤 자원의 할당을 허용하는지에 관한 여부를 결정하기 전에, **미리 결정된 모든 자원들의 최대 가능한 할당량을 가지고 시뮬레이션 해서 Safe state에 들 수 있는지 여부**를 검사합니다. 즉 대기중인 다른 프로세스들의 활동에 대한 교착 상태 가능성을 미리 조사하는 것입니다.

  어떤 자원 한 가지에 대해서 은행원 알고리즘을 시뮬레이션 해보고자 합니다.

  **처음에 시스템이 총 12개의 자원을 가지고 있다고 가정**해 보겠습니다.

| (t=t0) | Max  | Allocation | Need | Available |
| :----: | :--: | :--------: | :--: | :-------: |
|   P0   |  10  |     5      |  5   |           |
|   P1   |  4   |     2      |  2   |           |
|   P2   |  9   |     2      |  7   |           |

  P0~P2는 프로세스이고, `Max`는 각 프로세스마다 최대 자원 요청량, `Allocation`은 현재 프로세스에 할당 중인 자원의 양, `Need`는 남은 필요한 자원의 양(Max-Allocation) 입니다.

  현재 t0일 때 **프로세스에 할당된 자원의 합은 5+2+2=9개** 입니다. 따라서 현재 **Available 자원**은 12 - 9 = **3개** 입니다.

  여기서 Safe sequence를 찾아보려고 합니다. 순서가 `` 일 때 안전 순서를 만족합니다.

  - `P1`은 2개가 이미 할당되어 있고, 2개를 추가적으로 할당받기를(`Need`) 기다리고 있습니다. 현재 **Available 자원은 3개**이므로, 이 중에 2개를 P1에게 할당해 줍니다. => **현재 Available은 3 - 2 = 1개**
  - 실행이 끝난 `P1`은 자신에게 할당되어 있던 자원 4개를 모두 반납합니다. => **현재 Available은 1 + 4 = 5개**
  - 현재 Available 자원이 5개이고, 이를 **P0에게 모두 할당해 주면** P0도 실행 가능해집니다. => **현재 Available은 5 - 5 = 0개** 가 됩니다.
  - 실행이 끝난 `P0`은 자신에게 할당되어 있던 자원 10개를 모두 반납합니다. => **현재 Available은 0 + 10 = 10개**
  - 마지막으로 `P2`에게 자원 7개를 할당해 줍니다. => **현재 Available은 10 - 7 = 3개**
  - 실행이 끝난 `P2`는 자신에게 할당되어 있던 자원 9개를 모두 반납합니다. => **현재 Available은 3 + 9 = 12개**

  이렇게 자원의 부족함 없이 올바르게 할당하여 모든 프로세스가 실행을 할 수 있었습니다.

  만약 여기에서 P2 프로세스가 처음에 자원을 하나 더 할당받고 있었다면(즉, 2개가 아니라 3개) 운영체제가 가지고 있는 Available 자원은 12 - (5+2+3) = **2개** 였을 것입니다.

  이 상황에서는 처음에 P1에게 2개를 모두 주고, P1이 실행이 끝나고 자원을 모두 반납해도 **Available 자원은 2 + 2 = 4개 뿐**이므로, 이 자원으로는 나머지 P0이나 P2 프로세스를 해결해 줄 수 없습니다. (모두 4개보다 많은 양의 자원을 필요로 하고 있으므로)

  따라서 P0, P2는 자원을 할당받기를 계속 기다려야 할 것입니다.

  운영체제가 사전에 P2 프로세스가 자원을 하나 더 요청했을 때 할당해 주지 않고, P1이 먼저 끝나게 한다면 데드락이 발생하지 않았을 것입니다. 그러므로 은행원 알고리즘을 사용해서 **자원 할당량을 사전에 파악하고 데드락을 회피**할 수 있도록 하면 될 것입니다.

  그러나 은행원 알고리즘의 경우, **이처럼 미리 최대 자원 요구량을 알아야 하고, 할당할 수 있는 자원 수가 일정해야 하는 등 사용에 있어 제약조건**이 많고, 그에 따른 자원 이용도 하락 등 단점도 존재합니다.

------

  ### 데드락 탐지(Detection) 및 회복(Recovery)

  먼저 시스템이 데드락 예방이나 회피법을 사용하지 않았을 때, 데드락이 발생할 수 있으니 여기에서 회복하기 위해 **데드락을 탐지하고, 회복하는 알고리즘**을 사용합니다.

  - 탐지 기법

    - Allocation, Request, Available 등으로 시스템에 **데드락이 발생했는지 여부를 탐색**합니다. 즉, 은행원 알고리즘에서 했던 방식과 유사하게 현재 시스템의 자원 할당 상태를 가지고 파악합니다.
    - 이 외에도 **자원 할당 그래프를 통해 탐지**하는 방법도 있습니다.

  - **회복 기법**

    데드락을 탐지 기법을 통해 발견했다면, **`순환 대기`에서 벗어나 데드락으로부터 회복하기 위한 방법**을 사용합니다.

    - 단순히 프로세스를 1개 이상 중단시키기
      - **교착 상태에 빠진 모든 프로세스를 중단시키는 방법** : 계속 연산중이던 프로세스들도 모두 일시에 중단되어 부분 결과가 폐기될 수 있는 부작용이 발생할 수 있음
      - **프로세스를 하나씩 중단 시킬 때마다 탐지 알고리즘으로 데드락을 탐지하면서 회복시키는 방법** : 매번 탐지 알고리즘을 호출 및 수행해야 하므로 부담이 되는 작업일 수 있음
    - 자원 선점하기
      - 프로세스에 할당된 자원을 선점해서, 교착 상태를 해결할 때까지 그 자원을 다른 프로세스에 할당해 주는 방법



### 참고

https://jhnyang.tistory.com/3

https://includestdio.tistory.com/12

https://chanhuiseok.github.io/posts/cs-2/

https://brownbears.tistory.com/46 - 간단정리