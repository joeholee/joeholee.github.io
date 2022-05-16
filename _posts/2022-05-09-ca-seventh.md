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
last_modified_at: 2022-05-15
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

# 2. Direct Mapped Caches

<br>
