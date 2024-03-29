# 면접

- 메모리란?
    - 운영체제(OS)는 메모리(RAM)에 프로그램을 위한 공간을 할당해줌
    - Code, Data, Stack, Heap 영역이 있음
    - Code
        - 우리가 작성한 소스 코드가 기계어 형태로 저장되는것
        - 컴파일 타임에 결정되고 중간에 코드가 변경되지 않도록 Read-Only형태로 저장
    - Data
        - 전역변수, static 변수 저장됨
        - 프로그램 시작과 동시에 할당되고 종료되어야 메모리가 해제 됨
        - 실행 도중 변수값이 변경될 수 있으니 Read-Write로 저장
    - Heap
        - 프로그래머가 할당,해제 해주는 영역
        - malloc,calloc으로 힙에 동적 할당할 수 있음
        - 사용 후 해제 해주지 않으면 메모리 누수 발생함
        - 유일하게 런타임시 결정되어 데이터 크기가 확실하지 않을때 사용
        - 클래스 인스턴스, 클로저 같은 참조 타입의 값
        - ARC를 통해 힙에 할당된 메모리가 더 이상  쓸모 없게 되면 자동으로 해제 해줌
    - Stack
        - 함수 호출시 함수의 지역변수, 매개변수, 리턴 값 등등이 저장되고 함수 종료되면 메모리 해제
        - 컴파일 타임에 결정되기 때문에 무한히 할당 할 수 없음
        - CPU에 의해 관리되고 최적화 되서 속도가 매우 빠름
- 힙과 스택의 차이점?
    - 스택은 메모리가 한정되어 있어 너무 큰 메모리 할당할 수 없음
    - 데이터의 크기를 모르거나 너무 크다 싶으면 힙에 할당해야 함
- 스택 오버 플로우란?
    - 스택에 너무 많은 메모리를 할당하게 되면 스택 오버 플로우가 발생하고 앱이 죽음
    - 힙과 스택은 같은 메모리영역을 공유함
    - 힙은 낮은 메모리 주소, 스택은 높은 메모리 주소부터 할당

- iOS에서는 힙부분을 어떻게 관리하나요?
    - ARC를 이용하여 관리합니다.
- ARC는 무엇인가요?
    - Auto Reference Count로 힙에 할당된 인스턴스의 메모리를 자동으로 관리해주는 것입니다.
    - RC를 계산하여 참조횟수가 0이면 더이상 사용하지 않는 메모리로 판단하여 해제함
- RC는 무엇인가요?
    - Reference Count로 참조 횟수를 나타냅니다.
    - 컴파일 시점에 언제 참조되고 해제되는지 결정되어 런타임 떄 그대로 실행하게 됩니다.
    - 개발자가 참조 해제 시점을 파악할 수 있습니다.
    - 런타임 시점에 추가 리소스가 발생하지 않습니다.
    - 순환 참조가 발생하게 되면 영구히 메모리가 해제 되지 않을 수 있습니다.
- RC가 증가할때는 언제인가요?
    1. 인스턴스를 생성할때
    2. 기존 인스턴스를 다른 변수에 대입할때
- RC가 감소할때는 언제인가요?
    1. 인스턴스를 가리키던 변수가 메모리에서 해제될때
    2. nil이 지정되었을때
    3. 변수에 다른 값을 대입했을 경우
    4. 프로퍼티의 경우, 속해 있는 클래스 인스턴스가 메모리에서 해제되었을 때

- 프로세스란?
    - 운영체제로부터 시스템 자원을 할당 받는 작업의 단위
    - 각각 독립된 영역(Code,Data,Stack,Heap)을 각자 할당받음
    - 프로세스끼리는 서로의 변수나 자료구조에 대해 절대 접근 못하고 IPC(프로세스간 통신)을 사용해야 함
- 멀티 프로세스란?
    - 하나의 프로그램을 여러개의 프로세스로 구성하여, 각 프로세스마다 하나의 작업씩 처리하는 것
    - 독립된 영역을 지니는 프로세스 이기에 안정성이 높다
    - Context Switching 시 CPU 부담이 커지고 오버헤드가 발생하게 됨
    - 프로세스간 자원 공유가 어렵다
- Context Switching란?
    
    CPU에서 프로세스를 메모리 영역에 올리고 내리고 하는 것
    
- 쓰레드란?
    - 한 프로세스 내에서 동작되는 여러 실행의 흐름
    - Code,Data,Heap영역은 공유, Stack영역 독립적임
- 멀티 쓰레드란?
    - 하나의 프로그램을 여러개의 쓰레드로 구성하여 , 각 쓰레드마다 하나의 작업을 처리하도록 하는 것
    - Code,Data,Heap 영역을 공유하기 때문에 Context Switching이 빠름
    - Stack영역을 빼고 공유하기 때문에 설계까 까다로움
    - A쓰레드가 접근하려는 힙 영역의 자원을 B가 갑자기 접근해서 바꿀때 자원 공유 문제가 발생
    - 공유하고 있기 때문에 하나의 쓰레드에서 문제가 발생하면 전체 쓰레드가 영향 받음

- 동기 sync 란?
    - Thread에서 보낸 작업이 끝날때 까지 현재 스레드는 다른 작업을 하지 않고 기다린다.
    - 단일 작업에서 요청에 대한 응답이 동시에 이뤄진다는 뜻
    - 해당 작업이 끝날때 까지 스레드는 다른 작업을 하지 않고 Block상태를 유지한다.
    - 설계가 간단하고 직관적이나, 결과가 주어질때까지 대기해야한다.
    - 하나의 작업이 Queue에서 빠져나갈때 까지 기다리기 때문에  Serial 이나 Concurrent나 차이가 없다.
- 비동기 Async란?
    - 보낸 작업이 끝나는 것을 기다리지 않고 현재 스레드는 다른 작업을 시작.
    - 설계가 복잡하지만 자원을 효율적으로 사용할 수 있는 장점
    
- 직렬 Serial 란?
    - 큐에 들어온 작업들을 순차적으로 실행시키는 것
    - 작업을 동기화 할때 사용함
    - GCD - MainQueue → MainThread
- 동시 Cocurrent란?
    - 내 큐에 들어온 작업들을 동시다발적으로 실행 시키는 것
    - 한번의 여러 Task 를 실행
    - GCD - GlobalQueue, CustomQueue
- Async와 Concurrent 차이점
    
    Sync와 Async 큐로 보내고 현재의 스레드는 다른 작업을 할 수 있게 할지 말지 결정
    
    Serial와 Concurrent는 큐로 들어온 작업들을 순차적으로 처리할지 순서 상관없이 실행할지 결정 
    
- 동기화란?

- 애플에서 제공하는 멀티 스레딩 API
    - GCD(Grand Central Dispatch)라는 C언어의 저수준 API
    - NSOperation이라는 Obj-C 기반으로 만들어진 고수준 API
    - async/await라는 Swift 5.5에서 생긴  API
- GCD에는 어떤 것들을 지원하나요?
    - main Queue
    - global Queue
    - Custom Dispatch Queue
- main Queue란?
    
    메인 스레드에서 사용 되는 Serial 큐로 모드 UI 처리는 메인스레드에서 처리
    
- global Queue란?
    
    Concurrent 큐
    
- Custom Dispatch Queue란?
    
    Serial,Concurrent 큐 정의 생성가능, default는 Serial
    
- Operation Queue API는요?
