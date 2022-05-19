---
title: "[CA] Module 3 - Lecture 7"
excerpt: "컴퓨터 아키텍쳐 9주차"

categories:
  - CS

author_profile: true
sidebar:
  nav: "main"

toc: true
toc_sticky: true

date: 2022-05-09
last_modified_at: 2022-05-19
---

# 1. Memory Hierarchy

가장 이상적인 메모리는 크고, 원하는 시간에 바로 엑세스가 가능한 메모리

하지만 메인 메모리의 latency(single access에 걸리는 시간)이 매우 큼.

(memory access시간이 processor cycle보다 몇십배 더 큼)

Bandwidth(주어진 시간에 필요한 Memory access)

→Bandwidth가 넓고(주어진 시간에 필요한 Memory access가 적고) latency는 작아야 함.

Moore’s Law에 따라 cpu의 성능은 매년 60%정도 향상

DRAM의 성능은 매년 7%정도의 향상

→해당 간극은 점점 더 넓어짐

데이터 접근은 무엇에 접근하냐에 따라 어마어마한 시간 차이가 날 수 있음

Physics: 용량이 큰 것이 느린 이유는 물리적인 영향이 크다.

Capacitance: CPU칩을 벗어 나는 순간 capacitance(전기용량) 몇개 이상의 차이가 남.

따라서 칩 안에서 작업 하는 것이 훨신 빠름.

다양한 메모리 레벨이 서로 다른 크기, 속도로 구성되어 있음.

locality를 이용해서 CPU가 매우 크고 빠른 메모리인것 처럼 착각하게 만드는 것

CPU와의 거리에 따라 속도, 가격 등이 달라짐.

핵심적인 내용 - 위의 그림과 비슷한 문맥임.

CPU: Register, Cache(Level 1)

Level2 Cache

Memory(Main Memory)

Disk

가장 이상적인 구조는 가장 큰 메모리를 가장 빠르게 접근하는 것

이를 가능하게 하는 것이 locality임.

Temporal locality(시간적)

- 최근에 access한 것이 빠른 시간 내에 access할 가능성이 높은 것
- for문, loop문 등

spatial locality(지역적, 공간적)

- 현재 access된 것의 주의에 있는 것이 access될 가능성이 높은 것
- 위의 코드의 a에 해당
- instruction들의 access도 해당

temporal locality는 동일한 메모리에 계속 access하는 것

Spatial locality는 주위에 있는 것들을 access하는 것

루프, subroutine, argument, vector, scalar 모두 locality를 찾아볼 수 있음.

최근 access, 근처에 있는 것들이 다시 access될 수 있기 때문에 이들을 Cache로 옮기면

작고 빠른 Cache로 크지만 느린 Memory를 빠르게 사용할 수 있음.

Cache가 가장 중요한 이유는 프로그램 안에서 가장 큰 역할을 차지하기 때문임.

- Cache line을 어디에 둘 것인가?
- Cache line을 어떻게찾아낼 것인가?
- Cache line을 어떻게 replacement할 것인가?
- write를 할 경우 memory와 sink를 어떻게 맞출 것인가?

제한점

- 나노초 단위에서 처리해야 하기 때문에 간단해야 한다.
- 여러가지 상황 속에서 시뮬레이션을 함.

# 2. Direct Mapped Caches

직접적으로 Mapping이 된다.

그림처럼 memory에 있는 line이 unique한 cache와 매칭

cache의 page라고 생각 한다면 memory에 있는 동일한 크기의 page는 모두 정해진 위치로 mapping

processer가 메모리에 접근하는 방법은 address임. 

→ n-bit physical address(Mips의 경우에는 32비트)

offset의 b길이는 각각의 cache line이 몇 bit인지 나타냄.

set index의 s길이는 set의 개수를 나타냄.

메모리에 access하기 위해서는 32비트만 필요함.

→offset은 cache line의 몇 번째 bit인지를 알려줌.

→set index는 어떤 cache line인지를 알려줌.

메모리는 cache보다 더 큼. 우리가 원하는 값이 cache안에 들어있는지를 확인해주는 것이 tag임.

→tag comparison을 통해 우리가 원하는 data가 해당 cache line 안에 있는지 확인할 수 있음.

S개 만큼, $S=2^s$ cache line이 있다는 그림.

tag와 비교를 해서 찾는 값이 cache에 있는지 매칭을 하게 됨.

valid는 처음에 의미 없는 데이터가 채워져 있을 경우에는 valid=0

의미 있는 데이터가 들어갈 때에는 valid=1로 바뀜.

보통 cache line을 모두 쓰는것이 아님.

→B bit를 이용해서 cache line안에 내가 access하고자 하는 word와 byte size를 접근

cache line은 더 큰 메인 메모리에 mapping되어 있음.

tag를 비교하여 데이터가 실제로 있는지 확인함.

main memory address를 가지고 cache에 어디에 있는지 확인할 수 있음.

2비트를 사용하는 이유는 cache가 4개이기 때문임. 남은 앞의 2비트는 tag임.

offset은 cache안의 우리가 원하는 data의 offset을 access 할 수 있는 정보

cache block=cache line

Mips에서는 1word가 4byte이므로 offset은 2개만 할당하면 4byte를 표현할 수 있다.

cache index에 8bit가 할당된 이유는 cache data가 1Kbyte에 1word가 4byte이기 때문임.

$1024byte/4byte=2^8$

나머지는 tag로 사용됨. 우리가 원하는 데이터의 tag와 cache에 있는 tag를 비교함.

또한 valid bit를 이용해서 유효한 데이터인지 확인

cache의 가장 큰 특성은 locality임.

- 그 중 spatial locality(공간 지역성)을 키우는 방법 중 하나는 block size(cache line)를 키우는 것임.
- block의 크기를 크게 할 수록
    - main memory에서 가져올 수 있는 데이터의 양이 크고
    - memory access횟수를 줄일 수 있음.
    - locality가 있는 데이터를 cache에 많이 올려놓을 수 있음.

32bit의 physical address가 있음.

multiword block direct mapped cache는 block이 여러개 있는 구조

→어떤 block에 접근할 것인지에 대한 데이터가 필요하다.

cache line을 decoding해서 우리가 원하는 line을 어떻게 아는 것인가

- 1word는 4byte
- index를 통해 어느 cache line인지
- block offset을 통해 어떤 block이 우리가 원하는 block인지 확인
- byte offset을 통해 block 안의 data에 접근
- tag를 서로 비교해서 우리가 원하는 데이터인지 확인
- valid를 비교해서 유효한 값인지 확인하는 과정도 있음

16kb는 4096 word로 구성됨.

block(line)이 4 개의 word로 구성됨

→1024개의 block

32bit에서 10개는 block을 찾는 데이터, 4개는 block안에서 byte를 찾는 데이터(2개로 word, 2개로 byte)

각각의 block은 128bit의 데이터와 18bit의 태그, 1bit의 valid bit이 있으므로, 

18.4KB의 용량을 가진다.

cache는 $2^s$개의 block을 갖는다.

각각의 cache block은 $2^b$의 offset(2bit는 word내에서 데이터를 찾는데 사용)

해당 식으로 정리할 수 있음.

장점

- 간단하다
- 빠르게 계산할 수 있다.

약점

- thrashing에 대해 위험하다.

### Thrashing Example

thrashing은 하드디스크의 입출력이 너무 많아져서 잦은 페이지 부재로 마치 작업이 멈춘 것 같은 상태를 말함

→memory의 access가 너무 빈번히 일어남.

서로 같은 block에 mapping된다면 replacement가 발생하기 때문에 overhead가 크다.

x접근→x[0]~x[3]이 cache에 로딩

→y접근→y[0]~y[3]이 cache에 로딩

→x와 y를 번갈아 접근한다면 x[0]~x[3]과 y[0]~y[3]을 번갈아 cache에 로딩하기 때문에 thrashing이 발생함.

Cache Operation

메인 메모리를 access하기 위해서 cache를 decoding해서 cache address를 access하는 것

CPU에서 n-bit physical address

block을 선택해서 tag와 data를 읽게 됨.

tag comparison → 태그가 일치하면 hit

read or write      → read면 데이터를 읽음. write면 block에 데이터를 씀

▶Write Through란?

CPU가 데이터를 사용하면 캐시에 저장되게 되는데, 데이터가 캐시 됨과 동시에 주기억장치 또는 디스크로 기입되는 방식을 지원하는 구조의 캐시이다. 즉, 캐시와 메모리 둘다에 업데이트를 해버리는 방식이다.장점 : 캐시와 메모리에 업데이트를 같이 하여, 데이터 일관성을 유지할 수 있어서 안정적이다.단점 : 속도가 느린 주기억장치 또는 보조기억장치에 데이터를 기록할 때, CPU가 대기하는 시간이 필요하기 때문에 성능이 떨어진다.

데이터 로스가 발생하면 안되는 상황에서는 Write Through를 사용하는 것이 좋다.

▶Write Back이란?

CPU 데이터를 사용할 때 데이터는 먼저 캐시로 기록되는데, 캐시 내에 일시적으로 저장된 후에 블록 단위에 캐시로부터 해제되는 때(캐시안에 있는 내용을 버릴시) 에만 주기억장치 또는 보조기억장치에 기록되는 방식이다. 즉, 데이터를 쓸 때 메모리에는 쓰지 않고 캐시에만 업데이트를 하다가 필요할 때에만 주기억장치나 보조기억장치에 기록하는 방법이다.장점 : Write Through보다 훨씬 빠르다.단점 : 속도가 빠르지만 캐시에 업데이트 하고 메모리에는 바로 업데이트를 하지 않기 때문에, 캐시와 메모리가 서로 값이 다른 경우가 발생할 때가 있다.

빠른 서비스를 요하는 상황에서는 Write Back을 사용하는 것이 좋다.

만약 tag comparison이 실패한다면 

- read
    - 가용한 block이 없을 경우 victim cache, valid block을 replace 시켜야 함.
    - 그렇지 않을 경우에는 memory access가 필요함.
- write
    - 메모리에서 읽을 수 있다면 write-allocate방법
    - 메모리에서 읽을 수 없다면 write-around방법을 사용함.

write back/write through

패널티를 줄일 수 있는 가장 좋은 방법은 cache를 크게 만들거나 좋은 design을 사용하는 것

다른 방법은 multy level로 구성하는 것

- 동일한 access를 가지고 있는 메모리라도 다른 level을 통해 miss rate를 매우 작게 구성할 수 있음
- 1 level cache에서는 hit time을 optimize시키고
- 2 level cache에서는 miss rate를 optimize시키는 것이 multy level cache를 통해 성능을 향상시킬 수 있는 좋은 방법임


<br>
