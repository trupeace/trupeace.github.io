# RISC-V
### 1. RISC-V의 개요
- 정의: UC-Berkeley에서 만든 RISC형태의 Open Computer ISA
    + RISC: Reduced Instruction Set Computer
    + ISA: Instruction Set Architecture

- 특징
    + Open ISA: royalty free
    + Modular Instructions: 49개의 기본 인스트럭션을 바탕으로 M, F, C, P, V extension 조합 가능
    + Custom. Insturctions: reserved opcode 및 LLVM를 통해 Customized instruction 지원 가능
        * LLVM (Low Level Virtual Machine): Frontend, IR (중간 표현), Backend로 구성되어 언어 독립적인 최적화를 지원하는 모듈 기반 컴파일러 구조

- 비고
    + RISC-V 자체는 Open Source Hardware는 아니나 참조가능한 다양한 Open Source 구현체가 존재
        + boomv3, ... 


### 2. 구조
- 크게 연산용 ISA인 Non-previleged ISA와 mode 제어용 Previlaged ISA로 구성
- 연산용 ISA는 base instruction set을 중심으로 I(Integer), M(Mul., Div.), A(Atomics), F(Float), D(Double), C(Compressed)등의 각종 extension이 존재하며 Custom Instruction Set도 추가 가능함(Custom opcode 확보되어 있음)
    + 표준 set 모음으로 G(General purpose = IMAFD)가 있음
- 16b,32b,64b 연산 지원
- 4 type of instructions
    + R, I, S, U
- 2가지 차별성(Modular Design, Custom Instruction)으로 MCU에서 Super computer까지 지원 가능함


### 3. RISC-V 현황
- Embedded 분야 (Popular)
    + SSD, Storage, AI accelerator 등을  등 Micro-controller target의 제품군에서 많이 사용되고 있음
    + 고성능 CPU가 아닌 Energy efficiency 또는 royalty가 주요 요구사항: 간결한 Inst. Decoder 구조와 Custom Instruction을 이용한 최적 ASIP 설계 가능
- 학술 연구 (Popular)
    + Computer Architecture, Simulator, Prototyping, ...
    + UC-Berkeley를 중심으로 기존 DLX를 대체
    + 신입 인력 교육 비용 절감
- 고성능 AP/Supper-Computer (Early)
    + 단말용 고성능 AP분야는 미진: 고성능 AP는 ISA자체 보다는 Micro-Architecture가 주요 인자로 회사의 투자 및 역량이 중요함
    + Alibaba, EPI 의 경우 RISC-V의 extension을 활용하여 General Purpose보다는 수학적 연산을 위한 Accelerator tile로 구성한 연구가 이루어짐
        * V (Vector) Extension, Custom Instruction Extension 지원
        * 부수적으로 Peta/Exa scale 이후의 시대를 위한 128bit computing을 지원
    + Micro-Architecture에 대규모 투자를 하는 x86, ARM을 근시일내에 따라 잡기는 어려우나 중국, 인도, 유럽에서 국가적 지원하에 개선이 이루어지고 있음 
- 종합:
    + Micro-Controller또는 Custom Instruction Set이 필요한 ASIP등에서 활용 가능
    + ARM 의 Big core를 대체하기는 시기상조임: 최신 프로세서 대비 1/2이하의 성능
        + ARM사의 big.LITTLE 수준의 제품군이 등장해야 본격적으로 AP분야에 활용가능할 것으로 판단됨
        + SiFive사의 경우 주제품은 E, S core군으로 ARM사의 R, M profile의 대체제이며 최고 성능 U74,U84 core는 ARM Cortex A78의 에 해당하는 E, C, S Core군이 있으나 주요 

### 4. 기대효과
- RISC-V 도입시 vendor specific하지 않은 표준 ISA 확보 가능
    + 특정 회사가 risk가 있더라도 유사한 IP를 제공하는 타 업체로 교체 가능
    + 개발 risk 최소화 가능
- 시장에 의한 기술 혁신 도입 용이함
    + uArch. 혁신 + 반도체 공정 혁신을 시장에서 확보
- 개발 역량 집중
    + 개발 effort를 SW 개발 및 custom extension에 집중 
    + HW 개발을 custom extension으로 표준화시 SW reusability 상승

### 5. 당사 도입전략
- Data Plane Processor와 ASIP으로 이원화
- Data Plane Processor 전략
    + 당사의 Data Plane S/W는 대부분 Integer동작을 기반으로 설계 되어 있으나 ARM, x86등 고성능 프로세서를 사용하여 Floating Point Unit을 효과적으로 사용하고 있지 않음
    + 당사 S/W에 불필요한 FPU를 비교적 간단하게 disable가능(F,D extension disable)
    + 고성능 분야에서 인정받은 IP를 확보가 어려우나 단기적으로 Multi-core로 대처가 가능하며 코어당 성능도 장기적으로 확보 가능할 것으로 기대됨.
- ASIP
    + 표준 extension + custom extension 
    + LLVM, GCC 도입으로 DSP 대비 고성능 컴파일러 도입 가능
    + 장기적으로 DSP granularity는 새로운 복잡도 문제가 될 위험성이 있음.
        + RISC-V 도입으로 고성능 코어로 migration 가능할 것으로 기대됨

