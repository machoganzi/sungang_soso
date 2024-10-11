# 🚗 자동차 전장 제어 시스템 요구사항 정의서

## 1. 소개
### 1.1 목적 
> 본 문서는 자동차 전장(전기장치) 제어 시스템의 상세한 요구사항을 정의합니다. 이 시스템은 차량의 주요 전기 구성 요소를 제어하고 모니터링하며, **안전하고 효율적인 차량 운행**을 보장하는 것을 목표로 합니다.  
> 본 문서는 **시스템 개발자**, **테스트 엔지니어**, **프로젝트 관리자**, **품질 보증 팀**을 위해 작성되었습니다.

### 1.2 문서 규칙
- 🟥 **필수**: 반드시 구현해야 하는 요구사항
- 🟨 **권장**: 가능한 구현하는 것이 좋은 요구사항
- 🟩 **선택**: 리소스가 허용되는 경우 구현할 수 있는 요구사항

### 1.3 독자 대상과 읽는 방법
- **시스템 개발자**: 3장 시스템 특성을 통해 시스템 설계 및 구현에 필요한 기술적 요구사항을 이해
- **테스트 엔지니어**: 2.5 활용 사례와 3장 시스템 특성을 통해 테스트 시나리오를 작성하고 기능 확인
- **프로젝트 관리자**: 전체 문서를 통해 시스템 개발 진행 상황을 파악하고 리스크 관리
- **품질 보증 팀**: 4장 기타 비기능 요건을 통해 시스템의 안전성, 성능 및 품질 요건 검증

### 1.4 프로젝트 범위
- 주요 차량 전기장치(엔진, 도어, 트렁크, 잠금장치 등) 제어 시스템 개발
- 사용자 인터페이스(대시보드 디스플레이)
- 시뮬레이터를 통한 시스템 검증
- **아이디어 💡** 실시간 모니터링 및 진단 시스템
- **아이디어 💡** 안전 기능 구현 (예: 충돌 감지 시 자동 도어 잠금 해제)
- 변속 기어

**📌 범위에서 제외되는 항목**:
- 인포테인먼트 시스템
- 내비게이션 시스템
- 자율 주행 기능
- 페달의 압력에 따른 속력 조절

### 1.5 참조
- **📚 ISO 26262**: 자동차 기능 안전 국제 표준
- **📚 AUTOSAR**: 자동차 오픈 시스템 아키텍처 표준
- **📚 SAE J3061**: 자동차 사이버보안 가이드북
- **📚 MISRA C**: 자동차 소프트웨어 개발을 위한 C 언어 가이드라인
- **📚 ISO/IEC 27001**: 정보 보안 관리 시스템 표준
- **📚 ISO 21434**: 자동차 사이버 보안 관리 표준

---

## 2. 전체 설명
### 2.1 제품 조망
자동차 전장 제어 시스템은 차량의 핵심 전기 구성 요소를 통합적으로 제어하고 모니터링하는 **임베디드 소프트웨어 시스템**입니다. 본 시스템은 차량의 **안전성**, **효율성**, **편의성**을 극대화하는 것을 목표로 합니다.

### 2.2 제품 기능
- **⚙️ 엔진 제어**: 시동/정지, 성능 최적화
- **🔒 차량 잠금 시스템**: 중앙 잠금, 스마트키 연동
- **🚪 도어 제어**: 개폐, 안전 잠금
- **📦 트렁크 제어**: 개폐, 잠금
- **🚗 가속 및 제동 제어**: 전자식 스로틀, ABS 연동
- **🛡️ 안전 기능**: 충돌 감지, 에어백 전개, 비상등 자동 작동
- **📊 실시간 차량 상태 모니터링 및 진단**
- **📟 대시보드 정보 표시**

### 2.3 운영 환경
- **💻 하드웨어 환경**: 
  - **CPU**: 32비트 ARM Cortex-M7 프로세서, 최소 240MHz
  - **메모리**: 최소 512KB RAM, 2MB Flash 메모리
  - **통신 인터페이스**: CAN bus, LIN bus, FlexRay
  - **센서**: 속도 센서, 가속도 센서, 온도 센서 등
- **🛠️ 소프트웨어 환경**: 
  - **RTOS**: FreeRTOS 또는 AUTOSAR 호환 OS
  - **개발 도구**: MISRA C 호환 컴파일러, 정적 코드 분석 도구
  - **버전 관리 시스템**: Git

### 2.4 설계 및 구현 제약사항
- **표준 준수**: 
  - **✅ ISO 26262**, **✅ MISRA C**, **✅ AUTOSAR** 준수
- **성능 제약**: 
  - 메모리 사용량 **256KB** 이하
  - 응답 시간 **10ms** 이내
  - CPU 사용률 **80% 미만**
- **보안 제약**: 
  - **🔐 암호화**: AES-256 사용
  - **🔏 접근 제어**: Role-based access control (RBAC) 구현
- **유지보수성**: 모듈화 및 문서화, 향후 기능 추가를 고려한 인터페이스 설계

### 2.5 활용 사례
- **운전자 활용 사례 🚗**
  - **시동/정지**: 운전자가 시동을 걸거나 끄는 작업
  - **전체 잠금장치 ON/OFF**: 차량 접근 제어
  - **문 열기/닫기**: 운전자가 도어를 개폐
- **시스템 활용 사례 ⚙️**
  - **충돌 감지 및 대응**: 충돌 시 도어 자동 해제 및 전원 차단
  - **실시간 상태 모니터링**: 차량 상태 감지 및 경고
  - **주행 중 안전 기능 활성화**: 속도 모니터링 및 안전 기능

---

## 3. 시스템 특성
### 3.1 정차 시 차량 제어
- **우선순위**:
  - 속도 확인 🚦
  - 엔진 상태 🔧
  - 페달 상태 ⚙️
  - 문 및 트렁크 제어 🚪
  - 전체 잠금장치 작동 🔒

---

## 4. 기타 비기능 요건
### 4.1 성능 요구사항
- 입력에 대해 **100ms 이내** 응답
- CPU 사용률 평균 **50% 미만**
- 시스템 부팅 시간 **2초 이내**

### 4.2 안전 요구사항
- **🛡️ ISO 26262 ASIL B** 이상 만족
- 중요 기능에 대한 **이중화**
- 시스템 오류 발생 시 **안전한 상태로 전환**

### 4.3 보안 요구사항
- 외부 통신 **암호화**
- 승인되지 않은 소프트웨어 업데이트 **방지**
- 차량 진단 포트(OBD-II) 접근 **인증**

### 4.4 소프트웨어 품질 특성
- **🧩 신뢰성**: MTBF **10,000시간** 이상
- **🔧 유지보수성**: 모듈화된 설계
- **🌐 이식성**: 다양한 차종에 적용 가능

### 4.5 테스트 전략
- **🧪 단위 테스트**: 코드 커버리지 **90% 이상**
- **🔍 통합 테스트**: 모듈 간 인터페이스 및 시나리오 테스트
- **📈 시스템 테스트**: 성능 및 안전, 보안 관련 테스트
- **🔁 회귀 테스트**: 자동화된 테스트 스위트 구축

### 4.6 유지보수 계획
- **🗓️ 정기 및 긴급 유지보수**
- **📊 성능 모니터링** 및 보고서 생성
- **📥 사용자 피드백 수집** 및 반영

---

