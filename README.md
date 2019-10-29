# DA-TSA

# EEG Time Sereies Data Analysis

## 연구목적

피험자 50명의 7개 eeg 채널(FP1, FP2, F3, Fz, F4, O1, O2)과 2개의 eog채널 (vertical, horizontal) 데이터를 수집을 했다. 
각 피험자가 3가지 영상(유튜브동영상, 2가지의 광고)을 시청하는 동안의 뇌파를 측정했다. 
모든 피험자가 같은 유튜브동영상 1개와 광고 2개(전기차 광고, 유니세프 광고)를 시청한다. 유튜브동영상의 길이는 약 6분정도이고 전기차 광고와 유니세프 광고는 각각 30초 가량이다. 
모든 피험자가 검은 화면 7초, 전기차광고 30초, 유튜브동영상 순서로 시청하는데, 50명 중 절반은 유니세프 광고를 유튜브동영상의 약 1분 30초 지점에서 유니세프 광고를 시청하고 나머지 절반은 유튜브동영상의 약 4분 30초 지점에서 유니세프 광고를 시청했다. 
즉, 피험자들을 두 그룹으로 나누어 중간광고 삽입 위치를 다르게 하였다. 그룹 A는 유튜브동영상의 전반부(1분 30초지점)에서 중간광고를 시청하고, 그룹 B는 유튜브동영상의 후반부(4분 30초지점)에서 중간광고를 시청했다. 
이 실험의 목적은 중간광고의 위치에 따라서 광고효과가 어떻게 변하는지 알고자 하는 것이다. 
광고효과를 피험자가 광고에 얼마나 집중하는지(집중도)와 광고에 얼마나 긍정적으로 반응했는지(동기)로 정의하고, EEG alpha파를 이용해 집중도와 동기를 측정하고자 한다. 

## 측정방법

Morgan Cerf와 Manuel Garcia-Garcia(2017)가 Consumer NeuroScience에서 제시한 방법을 따라서 집중도(Attention Index)와 동기(Approach/Withdrawal Index)를 측정했다. 
Attention Index(AI)는 한 피험자의 left frontal alpha값을 제곱한 값을 평균낸 값에 -1을 곱해서 사용한다. 
#### AI = -{(FP1 alpha)^2 + (F3 alpha)^2}/2로 정의했다. 이 AI값이 클수록 집중도가 높은 것이다.  
이 Attention Index는 사람이 무언가에 집중할때 left frontal alpha 값이 감소한다는 Klimesch(1999)와 Petersen과 Posner(2012)의 연구를 바탕으로 Morgan Cerf와 Manuel Garcia-Garcia가 제시한 측정방법이다. 
Approach/Withdrawal Index(AW)는 마찬가지로 Morgan Cerf와 Manuel Garcia-Garcia가 제시한 방법으로 좌뇌가 긍정적인 감정을 처리하고 우뇌가 부정적인 감정을 처리한다는 Coan과 Allen(2003) 그리고 Davison(2004)의 EEG frontal asymmetry theory에 기반한다. 
우뇌의 알파파 활성이 우세한 경우 Approach, 좌뇌 알파파 활성이 우세한 경우 Withdrawal로 보았다. 
#### AW = {(FP2 alhpa)^2+(F4 alpha)^2}/2 - {(FP1 alpha)^2 + (F3 alpha)^2}/2 이다. AW값이 클수록 우뇌 알파파 활성이 우세하기 때문에 Approach, AW값이 작을수록 Withdrawal 동기를 가졌다고 할 수 있다. 


## 데이터 설명
각 피험자의 원본 뇌파데이터에서 linefrequncy(60Hz)와 EOG artifact를 제거, alpha band를 추출하고, 영상을 시청한 부분의 뇌파만 잘라낸 데이터를 사용한다.
이 분석에서는 각 피험자의 뇌파데이터에서 AI와 AW값을 계산하고 표준화한 뒤에 A그룹끼리, B그룹끼리 평균낸 값을 A그룹의 AI, AW, B그룹의 AI, BW로 한다.
이 분석에 사용된 데이터는 미리 linefrequncy(60Hz)와 EOG artifact를 제거하고 alpha band만 추출한 데이터이다. 

## 분석 절차
이 분석에서는 50명 각 피험자의 뇌파데이터에서 AI와 AW값을 계산하고 표준화한 뒤에 A그룹끼리, B그룹끼리 평균낸 값을 A그룹의 AI, AW, B그룹의 AI, BW로 한다.
1. 50명 각 피험자의 AI, AW계산 후, 50명을 A그룹, B그룹으로 나누어 각 그룹의 AI, AW의 평균값 계산
3. 시계열 시각화
 














