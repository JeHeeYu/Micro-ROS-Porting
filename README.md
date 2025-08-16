# Micro-ROS-Porting

<br>
<br>

## .ioc 설정

- System Core - High Speed Clock (HSE)을 Crysal/Ceramic Resonator 으로 설정
- System Core - SYS - Timebase Source를 TIM1 으로 설정
- Middleware and Software Packs - FREERTOS - Interface를 CMSIS_V2 으로 설정
- FREERTOS - Configuration - Tasks and Queues에서 Stack Size를 3000으로 설정

<img width="361" height="239" alt="image" src="https://github.com/user-attachments/assets/ce1884c7-d55d-48b3-a396-5f6f99681058" />

<br>

공식 깃허브에서 10k 이상 설정하라고 하는 것을 알 수 있음

<img width="774" height="294" alt="image" src="https://github.com/user-attachments/assets/06972739-f3e9-4ff7-81f9-75ef81292f94" />

<br>

- UART3 채널의 DMA 설정
  - RX : Circular Mode / Priority -> Very High로 설정
  - TX : Normal Mode / Prioirty -> Very High로 설정
 
<img width="653" height="373" alt="image" src="https://github.com/user-attachments/assets/5c0f5734-a4ec-43ac-b9dc-1b90954d3863" />

<br>

- UART3 인터럽트 활성화

<img width="650" height="131" alt="image" src="https://github.com/user-attachments/assets/daea4fa0-1713-453e-bffe-ebda4e0eeab1" />

<br>
<br>

## Utility 추가 및 라이브러리 생성

- 루트 위치에 git clone

```
git clone https://github.com/micro-ROS/micro_ros_stm32cubemx_utils.git
```
