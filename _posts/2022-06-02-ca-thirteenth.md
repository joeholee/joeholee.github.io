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
last_modified_at: 2022-07-18
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

## Register Renaming

output and anti dependencies는 register renaming으로 해결할 수 있다.

펑셔널 유닛은 renaming이 없으면 늘리는게 별 소용이 없다. 리네이밍을 하니까 효과가 4배 이상 나더라. 보통 8~32개로 늘린다

## Branch Prediction

Delayed branch slot-여러 명령어가 안에서 실행되는게 복구가 너무 복잡해서  잘 안함

Branch prediction should be used-Branch history is very useful

또 다른 superscalar

결과(commit)는 순서대로 처리되어야하고, branch prediction이 틀렸을 경우도 처리해야하기 때문에 마지막에 temporary storage가 필요하다.

Results need to be put into order (commit or retire)

- Results sometimes must be held in temporary storage until it is certain they can be placed in “permanent” storage.
    - either committed or retired/flushed
- Temporary storage requires regular clean up – overhead – done in hardware.

**하드웨어의 서포트 필요**

-Facilities to simultaneously fetch multiple instructions

 여러개 명령어 동시 패치

-Logic to determine true dependencies involving register values and Mechanisms to communicate these values

 의존성 확인

-Mechanisms to initiate multiple instructions in parallel

 병렬적으로 여러 명령어 초기화를 위한 매카니즘?

-Resources for parallel execution of multiple instructions

여러 명령어 실행을 위한 리소스(특히 functional unit)필요

-Mechanisms for committing process state in correct order

순서대로 끝나기 위한 매카니즘

# Vector Processors

## Flynn’s Taxonomy(멀티 프로세서의 분류 방법)

-SISD(single instruction on single data): Mips, 인텔 펜티움

-**SIMD**(single instruction on multiple data): vector processer

-MISD(multiple instruction on single data): 지금은 없음

-MIMD(multiple instruction on multiple data): Multicore, multithreaded processors

## SIMD/Vector Processors

간단 요약

장점: 동일한 명령어로 여러 데이터를 처리해서 비용이 준다. 프로그램 메모리 자체를 줄일 수 있다(가능만 하면) 메모리 데이터를 멀티플한걸 하나에 처리해서 메모리 접근에서 좋다. 특히 포문

단점: 스위치 문에서 약하다
