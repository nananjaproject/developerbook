[OS] 운영체제에서 Process란? - OS 공부 1

Process란?
Process(프로세스)가 무엇일까요? 프로세스는 간단하게 말하면 현재 실행 중인 프로그램이라고 할 수 있습니다. 
그렇다면 프로그램은 무엇일까요? 프로그램은 Disk에 저장되어있는 실행 가능한 것이라고 볼 수 있습니다.
컴퓨터는 이러한 프로그램을 메모리에 Load 하고 이를 CPU에서 처리합니다. 

Multiple processes 
Mechanism은 필요한 기능을 구현하는 low-level 메서드나 프로토콜입니다. 
즉 간단하게 말하면 어떻게 할 것이냐에 관한 것입니다. Policy(정책)는 Mechanism 위에 존재하는 정책으로 어떤 종류의 결정을 내리는 알고리즘
CPU 가상화를 위한 Policy(정책)를 알아보겠습니다. CPU 가상화를 위한 정책에는 Scheduling 정책이 있습니다. 아까 Time-sharing과 같은 메커니즘에서 사용자는 마치 프로그램이 동시에 실행되는 것 처럼 보이지만 실제로는 동시에 일어나지 않습니다. 위의 예에선 0.001초씩 번갈아가며 실행되기 때문에 CPU입장에선 어떤 프로세스를 먼저 실행할지 고민이 될 수 있습니다. 
이러한 고민을 해결해주는 것이 Scheduling 정책

rogram Counter, Stack Pointer 등이 있습니다. Memory에서는 주소 공간을 필요

Process API
이러한 프로세스를 사용하기 위해 많은 API가 있지만 OS마다 종류가 다를 수 있습니다. 그러므로 여기에서는 모든 OS에서 공통적으로 가져야 하는 API에 대해 살펴보겠습니다.

Create
새로운 프로세스를 만듭니다.
Destory
프로세스를 제거합니다.
Wait
프로세스가 실행 중 잠시 멈출 일이 생길 때 사용합니다.
Miscellaneous Control
잘못 동작하고 있는 프로세스를 종료할 때 사용합니다.
Status
프로세스ID, 프로세스가 얼마 동안 실행됐는지 등에 대한 상태에 대한 정보를 알고 싶을 때 사용합니다.
Process API
Load
Dynamic allocation
Initialization
Jump to entry point : main()

프로그램을 실행시키는 방법

Load
Dynamic allocation
Initialization
Jump to entry point : main()

Load 단계 - Disk에 있는 프로그램을 DRAM과 같은 메모리에 프로세스로 적재시키는 것입니다. 예전에 만든 OS는 프로그램이 실행되기 전에 이러한 로드 작업을 한 번에 수행
OS는 프로그램 실행에 필요한 데이터만 로드합니다. 이러한 것은 paging, swapping 방법으로 가능
Dynamic allocation-tack공간에는 지역변수, 함수 매개변수 그리고 return address를 저장합니다. Heap 공간에는 동적 할당 하는 데이터가 저장되며 이는 C언어에서 malloc(), free()로 관리
Initialization -file descriptor(input, output, error), I/O와 같은 부분을 처리

Process States
Running, Ready, Blocked
![image](https://github.com/nanandive/developerbook/assets/117037428/370c61ce-5832-48e2-ac61-3935b6266243)


Running (실행 중)

Running 상태는 프로세스가 프로세서에 의해 실행되고 있는 상태를 말합니다. 즉 실행중인 명령을 뜻하는 것이죠.
Ready (준비 완료)

아까 위에서 본 프로그램을 프로세스로 만드는 방법을 모두 수행해서 이제 실행할 준비가 된 상태입니다. 하지만 아직 OS의 스케줄링 정책에서 선택 받지못해 실행은 되지 않은 상태라고 볼 수 있습니다.
Blocked (대기)
프로그램을 실행 중 먼저 실행해야하는 것이 생기거나 I/O 요청이 들어오면 실행중인 프로세스를 잠깐 멈출 수 있는데 그렇게 멈춰진 상태를 뜻합니다.

Ready 상태로 대기하게 됩니다. 만약 OS의 스케쥴링 정책에 의해 자신이 실행될 차례가 되어 dispatch 되는 것을 Scheduled
I/O가 발생하거나 다른 프로세스를 먼저 실행해야 하는 경우가 생기면 Blocked 상태가 되고 해당 이슈를 해결하면 다시 Ready상태가 되어 스케쥴링
실행 중 Time-sharing 기법에 의해 주어진 실행시간이 끝나게 되면 Ready상태로 다시 돌아간다.

프로그램을 실행시키는 방법
그럼 이제 프로그램을 실행시켜 프로세스로 만드는 방법에 대해 좀 더 자세히 알아보도록 하겠습니다. 우선 간단히 단계적으로 나타내면 다음과 같습니다.

Load
Dynamic allocation
Initialization
Jump to entry point : main()


Process States
그럼 이제 프로그램을 실행시켜 프로세스로 만드는 방법도 알았으니 실행된 프로세스의 상태에 대해 알아보겠습니다. 
우선 프로세스 상태에는 크게 3가지가 있으며 이는 Running, Ready, Blocked 상태


Running (실행 중)
Running 상태는 프로세스가 프로세서에 의해 실행되고 있는 상태를 말합니다. 즉 실행중인 명령을 뜻하는 것이죠.

Ready (준비 완료)
아까 위에서 본 프로그램을 프로세스로 만드는 방법을 모두 수행해서 이제 실행할 준비가 된 상태입니다. 하지만 아직 OS의 스케줄링 정책에서 선택 받지못해 실행은 되지 않은 상태라고 볼 수 있습니다.

Blocked (대기)
프로그램을 실행 중 먼저 실행해야하는 것이 생기거나 I/O 요청이 들어오면 실행중인 프로세스를 잠깐 멈출 수 있는데 그렇게 멈춰진 상태를 뜻합니다.


Process States Examples
프로세스는 총 2개(Process0, Process1)가 존재합니다. 1~4초까지는 Process0이 스케줄링되어 Running 상태인 것을 볼 수 있습니다. 4초에 할 일이 끝나게 되어 프로세스가 종료되고 OS의 스케줄러는 Process1을 스케줄링하여 프로세스 상태가 Ready에서 Running 상태로 변하게 됩니다.
8초에는 Process1까지 실행을 끝내고 프로세스를 종료하게 됩니다.

Process Control Block
PCB에는 프로세스 상태, 프로세스 ID, Program Counter, 메모리 관리 정보, CPU 스케줄링 정보, 등이 저장되어있으며 Context Switch에 사용되는 정보도 저장

 


