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
last_modified_at: 2022-06-15
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


