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

- 

<br>
<br>

## Utility 추가 및 라이브러리 생성

- 루트 위치에 git clone

```
git clone https://github.com/micro-ROS/micro_ros_stm32cubemx_utils.git
```

- 이후 도커 컨테이너 실행

<pre>
docker run -it --rm \
  -v $(pwd):/project \
  -e MICROROS_LIBRARY_FOLDER=micro_ros_stm32cubemx_utils/microros_static_library \
  microros/micro_ros_static_library_builder:humble
</pre>

- 라이브러리 파일 확인

<pre>
ls micro_ros_stm32cubemx_utils/microros_static_library/libmicroros 
available_ros2_types	built_packages		libmicroros.a		microros_include
</pre>

- Project - Properties - C/C++ Build -> Settings -> MCU GCC Compiler -> Include -> Add -> Workspace ... 후 추가

<img width="808" height="772" alt="image" src="https://github.com/user-attachments/assets/baf38e9d-59e9-41ed-b317-72d2c4fc5f99" />

<br>

- Project - Properties - C/C++ Build -> Settings -> MCU GCC Linker -> Libraries (-L) -> Add -> Workspace... 후 추가

<img width="803" height="766" alt="image" src="https://github.com/user-attachments/assets/7c1163d6-bfa5-4bd5-9e31-4d02925080c5" />



<br>

- 프로젝트 우측 클릭 -> New -> Other -> General -> File -> Advanced -> Link to file in the file system 체크 -> Browse.. 후 파일 4개 추가

<pre>
micro_ros_stm32cubemx_utils/extra_sources/custom_memory_manager.c
micro_ros_stm32cubemx_utils/extra_sources/microros_time.c
micro_ros_stm32cubemx_utils/extra_sources/microros_allocators.c
micro_ros_stm32cubemx_utils/extra_sources/microros_transports/dma_transport.c
</pre>

<img width="579" height="684" alt="image" src="https://github.com/user-attachments/assets/41252579-b2e1-44e5-8276-d5d9d95183ef" />

<br>

<img width="242" height="86" alt="image" src="https://github.com/user-attachments/assets/b5daf8f5-ba3c-4d12-93f4-9a79ea515d28" />

<br>

- Project -> Properties -> C/C++ Build -> Settings -> MCU GCC Compiler -> PreProcessor - Include - RMW_UXRCE_TRANSPORT_CUSTOM 추가

<img width="810" height="772" alt="image" src="https://github.com/user-attachments/assets/47703e0a-2547-4b61-ae8b-60fab7f22271" />

<br>

이전에 추가한 dma_transport.c 에서 전처리문을 추가하는 과정
<br>

<img width="649" height="204" alt="image" src="https://github.com/user-attachments/assets/a0098e16-3560-44ec-a79f-5538139b65c7" />

<br>

