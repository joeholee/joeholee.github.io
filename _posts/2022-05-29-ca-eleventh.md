---
title: "[CA] Module 4 - Lecture 11"
excerpt: "컴퓨터 아키텍쳐 13주차"

categories:
  - CS

author_profile: true
sidebar:
  nav: "main"

toc: true
toc_sticky: true

date: 2022-05-29
last_modified_at: 2022-06-06
---

# 1. Register Scoreboarding
### Out of Order Execution

멀티코어 · 멀티프로그래밍 위한 dynamic scheduling을 하드웨어가 어떻게 지원할 수 있나 살펴보자

**Scoreboarding** : instruction들을 OoO execution할 수 있도록 = dynamic하게 실행할 수 있도록 함. <br>
                    단, resource 충분히 있고 data dependency가 없어야 한다.
                    **WAR hazard**를 처리할 수 있다.

**Tomasulo Algorithm** : **WAR, WAW hazard**를 처리할 수 있다.
                         speculation handle 가능

scoreboard: 실행되고 있는 instruction들의 **resource**에 대한 **hazard**가 없는지 / **data dependency**가 없는지 살펴봄

⇒ 없으면 실행, 있으면 stall시키는 테크닉

오래된 테크닉 ∴ forwarding technique X / interrupt · exception model 현재에 비해 부족

💡 ***in-order issue, out-of-order execution, out-of-order commit*** 가능케 하는 테크닉

# 2. Scoreboard Example
