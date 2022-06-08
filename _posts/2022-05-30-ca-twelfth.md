---
title: "[CA] Module 4 - Lecture 12"
excerpt: "컴퓨터 아키텍쳐 13주차"

categories:
  - CS

author_profile: true
sidebar:
  nav: "main"

toc: true
toc_sticky: true

date: 2022-05-30
last_modified_at: 2022-06-08
---

# 1. Tomasulo Algorithm
> **Dependency** : a property of programs
> 

Dependency가 존재한다? ⇒ Hazard 발생 가능성 有

(실제 hazard) & (stall의 길이) : pipeline의 property

> **Data Dependencies**의 중요성
> 
1. hazard 발생할 가능이 있다는 것 나타냄(indicate)
2. 결괏값이 어떤 순서로 계산되어야하는지 결정
3. 얼마나 병렬화가 실행될 것인지 upper bound를 세움 (병렬적으로 처리하고 싶은데 data dependency 있으면 어려우니까)

<aside>
✔️ hazard 피하기 위해 **Hardware schemes** 살펴보기

</aside>
