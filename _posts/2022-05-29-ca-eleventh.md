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
last_modified_at: 2022-06-07
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

왼쪽: 레지스터 / 오른쪽: functional unit

검정색 라인을 통해 data를 rg에서 받고 연산한 결과를 파란색 라인을 타고 rg에 update

필요한 경우 mem acc 허용

핵심은 **scoreboard**: rg · FU 어떠한 상태인지 추적 → hazard 여부 확인에 도움

- WAR 해결
    - rg가 read될 때까지 wb 기다림
    - Read Operands stage에서만 rg를 읽을 수 있음
- WAW
    - hazard를 detect하면 다른 inst 끝날 때까지 해당 inst의 issue를 stall
- register renaming은 존재하지 않음 (Tomasulo에서는 지원)
- multiple instruction들을 execution phase에서, 즉 multiple instruction들을 실행해야 함 → multiple execution unit 지원
- scoreboard는 inst 간 dependency를 살펴보고 유지할 수 있다 ⇒ hazard를 회피할 수 있다
- scoreboard는 기존의 ID · EX · WB stage를 4개의 stage로 함 ← **ID를 2개로 나눔**

# 2. Scoreboard Example
