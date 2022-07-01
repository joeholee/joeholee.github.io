---
title: "[CA] Module 5 - Lecture 14"
excerpt: "컴퓨터 아키텍쳐 15주차"

categories:
  - CS

author_profile: true
sidebar:
  nav: "main"

toc: true
toc_sticky: true

date: 2022-06-13
last_modified_at: 2022-07-01
---

# 1. Multithreading

# **Multi-threading**

### 1. Multithreading

(1) Multithreading을 하는 이유

- ILP (Instruction level parallelism)나  DLP (data level parallelism)은 하나의 sequential한 프로그램에서 계속 extract 하는 것은 어려움이 있다.
- 프로세서를 thread 단위로 처리하는 TLP 사용
- TLP를 사용하여 multithreading하면 단일 프로세서의 utilization을 향상 가능

(2) single threading과 multithreading 비교
- T1 single thread의 경우 forwarding 없다고 가정하면 data dependancy로 인해 연속적인 stall 발생
- 서로 다른 4개의 thread의 instruction들을 교차하여 실행하는 multi threading의 경우 하나의 instruction은 같은 thread의 다음 instruction의 decode 전에 항상 writeback되기 때문에 자연스럽게 data dependancy가 해소된다.
- 8-way superscalar arcitecture에서 실제로 processor가 busy한 cycle은 평균적으로 20% 내외이므로 thread간 교차 실행으로 의미 있는 성능 향상을 기대할 수 있다.
  
(3) multithreading cost

multithreading을 위해서는 thread간의 dependancy를 없애기 위해 thread level의 program counter와 general purpose register가 필요하다.

- 각각의 page table base register와 exception  handling register가 필요하다.
- cache와 TLB의 capacity 향상이 필요하다.
- thread 관리를 위한 OS의 overhead

### 2. Granularity Multithreading

(1) multi-thread 방법들

- Coarse-grained multithreading

  - 매 100~1000 정도의 cycle마다 thread를 교차하여 실행하는 것

 - memory access로 인해 많은 cycle이 낭비될 때 유용

 - hardware support가 적다

- Fine-grained multithreading

 - 매 cycle마다 thread를 교차하는 것 (앞의 예제에서 사용한 방식)

 - data hazard나 cache miss의 발생시 유용

 - multi-issue arciectrure에서는 resource를 완벽히 활용하지 못함

- simultaneous multithreading

 - 하나의 cycle에서 여러 thread를 동시에 실행하는 것

 - register renaming과 dynamic scheduling을 이용

 - resource를 가장 최대로 활용

 - 많은 hardware support가 필요

3. CMP: Chip Multiprocessing

- 색칠된 부분에서 issue가 일어나지 않음
- 모든 issue width에서 issue가 일어나지 않는 completely idle cycle을 vertical waste라고 한다.
- 일부 issue가 일어나지 않는 partially filled cycle을 horizontal waste라고 한다.

- vertical multithreading

- cycle by cycle로 thread interleave

- vertical waste를 없애지만 horizontal waste는 남아있다.
