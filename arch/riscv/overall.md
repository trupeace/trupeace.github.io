# RISC-V Overview

### 1. RISC-V의 정의

- 2010년 UC-Berkeley에서 만든 Open Computer ISA (Instruction Set Architecture)
    + 32bit RISC
- 현재 비영리재단인 riscv.org(since 2015)에 의해 유지,보수되고 있음
- 특정회사나 CPU구현체가 아님
    + Core IP를 자체 개발하고나 IP회사에서 구매필요

### 2. 구조
- 크게 연산용 ISA인 Non-previleged ISA와 mode 제어용 Previlaged ISA로 구성
- 연산용 ISA는 base instruction set을 중심으로 I(Integer), M(Mul., Div.), A(Atomics), F(Float), D(Double), C(Compressed)등의 각종 extension이 존재하며 Custom Instruction Set도 추가 가능함(Custom opcode 확보되어 있음)
    + 표준 set 모음으로 G(General purpose = IMAFD)가 있음
- 16b,32b,64b 연산 지원
- 4 type of instructions
    + R, I, S, U

### 3. 시장 현황
- SSD등 Micro-controller target의 제품군에서 많이 사용되고 있음
- MMU, Multi-core등을 지원하는 제품군이 등장하면서 Super computer에서도 일부 사용되고 있으나 x86/ARM에 비해 비중이 매우 떨어짐

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

