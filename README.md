# 인공지능 스펙트럼 센싱 기반 실시간 저피탐 통신 탐지기 설계 및 구현

> 본 저장소는 프로젝트 소개 및 발표 자료 공유를 목적으로 구성되었으며, 소스 코드는 포함하지 않았습니다.

## 프로젝트 개요

본 프로젝트는 저피탐(Low Probability of Intercept, LPI) 통신 신호를 실시간으로 탐지하기 위한 인공지능 기반 스펙트럼 센싱 시스템을 설계하고 구현한 프로젝트입니다.

최근 자폭 드론 및 비인가 무선 기기의 확산으로 인해 저전력·주파수 호핑 특성을 가지는 무선 통신 신호를 조기에 탐지하는 기술의 중요성이 증가하고 있습니다. 하지만 기존 에너지 탐지 기반 스펙트럼 센싱 방식은 낮은 SNR 환경에서 신뢰성 있는 탐지가 어렵다는 한계가 있습니다.

본 프로젝트에서는 이러한 문제를 해결하기 위해 스펙트로그램 기반 주파수 탐지를 객체 탐지(Object Detection) 문제로 정의하고, YOLOv8 기반 인공지능 스펙트럼 센싱 파이프라인을 구성하였습니다.

## 핵심 아이디어

- RF 신호를 FFT 기반 스펙트로그램 이미지로 변환
- 신호 구간을 Bounding Box로 라벨링
- 주파수 탐지 문제를 객체 탐지 문제로 재정의
- YOLOv8n 모델을 Scratch 방식으로 학습
- ONNX 변환을 통해 Raspberry Pi 환경에서 온디바이스 추론 수행
- Flask 기반 대시보드를 통해 실시간 탐지 결과 시각화

## 실험

<p align="center">
  <img width="900" alt="Experiment setup" src="https://github.com/user-attachments/assets/d26886b5-194d-4ec6-beb5-3009cbccd41e" />
</p>

<p align="center">
  <b>Figure 1. 실험 구성도</b>
</p>

송신부는 Signal Generator를 이용하여 ms 단위의 주파수 호핑 신호를 낮은 전력으로 송출함으로써 LPI(Low Probability of Intercept) 환경을 구성하였습니다.  
수신부에는 Spectrum Analyzer와 제안 시스템의 탐지기를 동일한 위치에 배치하여, 상용 스펙트럼 분석기와 제안 시스템의 탐지 결과를 비교하였습니다.

<p align="center">
  <img width="600" alt="Receiving environment" src="https://github.com/user-attachments/assets/42249546-59e1-4736-8aed-c0bca6d898ac" />
</p>

<p align="center">
  <b>Figure 2. 수신 환경</b>
</p>

실험 환경은 다음 두 가지 조건으로 구성하였습니다.

| 조건 | 설명 | 목적 |
|---|---|---|
| **Analyzer Detectable Scenario** | Spectrum Analyzer에서 송신 신호가<br>육안으로 확인되는 조건 | 일반적인 수신 환경에서 <br>제안 시스템의 탐지 결과 확인 |
| **Analyzer Undetectable Scenario** | Spectrum Analyzer에서 송신 신호가<br>Noise Floor와 유사하여 육안 식별이 어려운 조건 | LPI 환경에서 제안 시스템의 탐지 성능 확인 |

## 실험 영상

 - Analyzer Detectable Scenario (https://youtu.be/VMXERdvfJ80?si=uXlyPM0fmPjn3rhp)
 - Analyzer Undetectable Scenario (https://youtu.be/O74QrTFrt00?si=IwmjsKMl51plVzkS)
