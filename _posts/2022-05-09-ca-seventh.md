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
last_modified_at: 2022-05-18
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

<br>
