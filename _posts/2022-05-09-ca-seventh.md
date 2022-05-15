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

# 2. Direct Mapped Caches

<br>
