---
title: "[CA] Module 5 - Lecture 13"
excerpt: "컴퓨터 아키텍쳐 14주차"

categories:
  - CS

author_profile: true
sidebar:
  nav: "main"

toc: true
toc_sticky: true

date: 2022-06-02
last_modified_at: 2022-07-09
---

# 1. Superscalar Architecture

## Superscalar Organization

슈퍼 스칼라 구조: 독립적인 명령어들을 병렬 실행하는 구조.

RISC(명령어 적은) 구조에 유리(cisc는 명령어마다 길이가 달라서 Fetch전에 조금 decode해서 파악해야한다. superscalar에 별로임.)

base machine: pipeline만

superpipelined: 4개를 8개인 것처럼 처리하여 0.5단계에서 당기는

superscalar: pipeline+명령어 병렬 실행

2개의 정수 ALU 파이프라인, 2개의 소수 ALU 파이프라인, 1개의 메모리 파이프 라인 

-stall이 발생하면 2배 이상의 안 좋은 영향을 받는다(특히 procedural dependency)

dependency에 의한 stall이 없어야 superscalar의 degree가 깊어질 수 있다. 더 효율적으로 실행될 수 있다

## Out-of-order Completion

inorder issue, OoO executione, completion을 수퍼스칼라에서 어떻게 지원하는가

-issue order(Order in which instructions are fetched)

-execution order(Order in which instructions are executed)

-completion order(Order in which instructions update registers and memory values)

가정

I1 requires 2 cycles to execute(실행에 2 사이클 필요)

I3 & I4 conflict for the same functional unit(excute 병렬 불가)

I5 depends upon value produced by I4

I5 & I6 conflict for a functional unit(excute 병렬 불가)

In-Order Issue / In-Order Completion: 8사이클

In-Order Issue / Out-of-Order Completion: 7사이클

Out-of-Order Completion일 때 한 사이클이 준다
