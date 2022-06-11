---
title: "[CA] Module 4 - Lecture 13"
excerpt: "컴퓨터 아키텍쳐 14주차"

categories:
  - CS

author_profile: true
sidebar:
  nav: "main"

toc: true
toc_sticky: true

date: 2022-06-02
last_modified_at: 2022-06-11
---

# 1. Superscalar Architecture

## Superscalar Organization

슈퍼 스칼라 구조: 독립적인 명령어들을 병렬 실행하는 구조.

RISC(명령어 적은) 구조에 유리(cisc는 명령어마다 길이가 달라서 Fetch전에 조금 decode해서 파악해야한다. superscalar에 별로임.)

base machine: pipeline만

superpipelined: 4개를 8개인 것처럼 처리하여 0.5단계에서 당기는

superscalar: pipeline+명령어 병렬 실행
