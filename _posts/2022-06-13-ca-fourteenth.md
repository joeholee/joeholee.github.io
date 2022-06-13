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
last_modified_at: 2022-06-13
---

# 1. Multithreading

# **Multi-threading**

### 1. Multithreading

(1) Multithreading을 하는 이유

- ILP (Instruction level parallelism)나  DLP (data level parallelism)은 하나의 sequential한 프로그램에서 계속 extract 하는 것은 어려움이 있다.
- 프로세서를 thread 단위로 처리하는 TLP 사용
- TLP를 사용하여 multithreading하면 단일 프로세서의 utilization을 향상 가능
