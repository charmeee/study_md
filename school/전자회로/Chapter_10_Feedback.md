
# 챕터 10 피드백 (Feedback)

## 10.1 일반 피드백 구조 (General Feedback Structure)
피드백의 양:
$$
A_f = rac{A}{1 + Aeta}
$$

1. **액티브 장치**: 큰 변동을 가진 증폭 (예: Vt의 변동 -> gm의 변동 -> Av, Ai의 변동)
2. **패시브 장치**: 재현성이 좋은 손실 -> 작은 변동 (덜 민감함)
3. **피드백**:
   - **네거티브 피드백 (퇴행성)**: 증폭기
   - **포지티브 피드백 (재생성)**: 발진기

네거티브 피드백의 효과:
- 회로 구성 요소 값 변동에 대한 증폭도를 둔감하게 함
- 비선형 왜곡 감소
- 잡음의 영향 감소
- 입력 및 출력 임피던스 제어
- 증폭기의 대역폭 확장

모든 위의 특성들은 이득의 감소를 대가로 얻어진다.

네거티브 피드백 예시:
- OP-amp, 이미터 퇴행 저항 (CE(CS) with Re, emitter (source) follower 등)

## 10.2 네거티브 피드백의 몇 가지 특성 (Some Properties of Negative Feedback)

1. **이득 둔감성 (Gain Desensitivity)**
   $$
   D = 1 + Aeta
   $$

2. **대역폭 확장 (Bandwidth Extension)**
   $$
   \omega_{L_f} = rac{\omega_L}{1 + Aeta}
   $$
   $$
   \omega_{H_f} = (1 + Aeta)\omega_H
   $$

3. **잡음 감소 (Noise Reduction)**
   $$
   SNR_{out} = rac{A_{v2}}{A_{v2}V_n^2 + V_s^2}
   $$

4. **비선형 왜곡 감소 (Reduction in Nonlinear Distortion)**
   $$
   A_f = rac{A}{1 + Aeta}
   $$

## 네 가지 기본 피드백 위상 (Four Basic Feedback Topologies)

1. **전압-전압 (series-shunt)**: 전압 증폭기
2. **전압-전류 (series-series)**: 트랜스컨덕턴스 증폭기
3. **전류-전압 (shunt-shunt)**: 트랜스레지스턴스 증폭기
4. **전류-전류 (shunt-series)**: 전류 증폭기

## 10.3 피드백 전압 증폭기 (series-shunt)

1. **이상적인 경우 (Ideal Case)**:
   - 피드백 네트워크 (RL) 및 소스 저항 (RS)로 인한 로딩 효과 없음
   - 폐루프 이득:
     $$
     A_f = rac{A}{1 + Aeta}
     $$

2. **실제 상황 (Practical Situation)**:
   - 로딩 효과 고려
   - 출력 임피던스 감소:
     $$
     R_{out} = rac{R_{OL}}{1 + Aeta}
     $$

## 10.4 체계적인 피드백 전압 증폭기 분석 (Systematic Analysis of Feedback Voltage Amplifier)

1. **이상적인 경우 (Ideal Case)**:
   - 로딩 효과 없음
   - 폐루프 이득:
     $$
     A_f = rac{A}{1 + Aeta}
     $$

2. **실제 상황 (Practical Situation)**:
   - 로딩 효과 고려
   - 출력 임피던스 감소:
     $$
     R_{out} = rac{R_{OL}}{1 + Aeta}
     $$

### 예제 10-1
오픈 루프 이득이 1000이고 피드백 계수가 0.01인 경우:
$$
A_f = rac{A}{1 + Aeta} = rac{1000}{1 + 1000 	imes 0.01} = 9.9
$$

피드백 폐루프 이득:
$$
A_f pprox rac{1}{eta} = 10
$$

이득 변화:
오픈 루프: 20%, 폐루프: 0.025%
$$
rac{\Delta A_f}{A_f} = rac{A}{1 + Aeta} 	imes rac{\Delta A}{A} = rac{1000}{1 + 1000 	imes 0.01} 	imes 0.2 = 0.0025
$$

## 10.5 기타 피드백 증폭기 유형 (Other Feedback Amplifier Types)

- 시리즈-시리즈 (트랜스컨덕턴스 증폭기)
- 션트-션트 (트랜스레지스턴스 증폭기)
- 션트-시리즈 (전류 증폭기)

## 10.6 피드백 분석 방법 요약 (Summary of the Feedback Analysis Method)

1. 이상적인 경우와 실제 상황을 모두 고려하여 분석
2. 각 피드백 토폴로지에 대해 폐루프 이득과 출력 임피던스 계산

## 10.7 안정성 문제 (The Stability Problem)

피드백 시스템에서 안정성을 유지하기 위해 다음을 고려해야 합니다:
- 폐루프 이득
- 주파수 응답
- 위상 여유

## 10.8 증폭기 극점에 대한 피드백의 효과 (Effect of Feedback on the Amplifier Poles)

피드백은 증폭기의 극점을 이동시켜 안정성을 개선할 수 있습니다:
$$
P_f = P(1 + Aeta)
$$

## 10.9 보드 플롯을 사용한 안정성 연구 (Stability Study using Bode Plots)

보드 플롯은 주파수 응답과 위상 여유를 시각적으로 분석하여 시스템의 안정성을 평가하는 데 사용됩니다.

## 10.10 주파수 보상 (Frequency Compensation)

주파수 보상 기법은 시스템의 대역폭을 확장하고 안정성을 개선하는 데 사용됩니다.
$$
\omega_{c} = rac{\omega_{H}}{1 + Aeta}
$$
$$
\omega_{L} = rac{\omega_{L}}{1 + Aeta}
$$
$$
\omega_{H} = (1 + Aeta)\omega_{H}
$$
