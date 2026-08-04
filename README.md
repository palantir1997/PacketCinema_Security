# Packet Cinema - Web Security Hardening

영화관 웹사이트 보안 강화 프로젝트

## 🎬 프로젝트 개요

Packet Cinema 웹사이트의 취약점을 패치하고, **ModSecurity + Suricata + pfSense**를 이용한 다층 방어 시스템 구축

[![Packet Cinema - 모의 해킹 및 방어 테스트](https://img.youtube.com/vi/oH_uLIhvd5Q/maxresdefault.jpg)](https://www.youtube.com/watch?v=oH_uLIhvd5Q)

<img width="1326" height="738" alt="스크린샷 2026-08-04 170409" src="https://github.com/user-attachments/assets/ba407993-01e1-444a-8525-2e991ef3751c" />


### 기술스택/환경구성
<img width="1326" height="742" alt="스크린샷 2026-08-04 152935" src="https://github.com/user-attachments/assets/424878f6-68ea-48f6-b425-b0a9c7aa861d" />

<img width="1325" height="742" alt="스크린샷 2026-08-04 152941" src="https://github.com/user-attachments/assets/161f698d-4ff3-4616-aa97-870cb1cd491e" />


## 🛡️ 현재 구축 환경

<img width="1737" height="979" alt="스크린샷 2026-08-03 170937" src="https://github.com/user-attachments/assets/0d1935b1-0795-49a2-90c4-2b523488fc7c" />


## 🛡️ 구현 기능

### 기존 취약점 패치
- 발견된 모든 보안 결함 수정
- 코드 보안 강화

### 다층 방어 시스템
- **ModSecurity**: WAF (웹 애플리케이션 방화벽)
- **Suricata**: IDS (침입 탐지 시스템)
- **pfSense**: 네트워크 방화벽


<img width="1735" height="950" alt="스크린샷 2026-08-03 170619" src="https://github.com/user-attachments/assets/d7f57af5-eed0-479b-9991-b90621fd0897" />
<img width="1744" height="982" alt="스크린샷 2026-08-03 170625" src="https://github.com/user-attachments/assets/2de145ee-ea15-452f-b673-51b31612baba" />

### 공격 테스트 & 차단 검증

| 공격 유형 | OWASP | 결과 |
|----------|-------|------|
| **SQL Injection** | A03:2021 | ✅ 차단됨 |
| **Brute Force** | A07:2021 | ✅ 차단됨 |
| **Path Traversal** | A01:2021 | ✅ 차단됨 |

### 영상 참조

## 📊 모니터링

Splunk를 통한 실시간 보안 이벤트 모니터링 및 분석

<img width="1280" height="720" alt="슬라이드1" src="https://github.com/user-attachments/assets/54d9b451-e237-4dfb-9b7c-5cc71a1d4ddf" />
<img width="1280" height="720" alt="슬라이드2" src="https://github.com/user-attachments/assets/4c110d38-27cf-42c0-93ce-129e6d5c04be" />
<img width="1280" height="720" alt="슬라이드3" src="https://github.com/user-attachments/assets/ba31fc8e-a9c5-430e-a2cb-a86f1c82b471" />
<img width="1280" height="720" alt="슬라이드4" src="https://github.com/user-attachments/assets/6a1a8157-270f-4640-9a84-50b8eb6b5355" />
<img width="1280" height="720" alt="슬라이드5" src="https://github.com/user-attachments/assets/3b74a15e-d5ec-4d28-91e3-f4ebf8058d0e" />
<img width="1280" height="720" alt="슬라이드6" src="https://github.com/user-attachments/assets/28a725ff-f0d5-4691-88b4-9b1fe5687e58" />
<img width="1280" height="720" alt="슬라이드7" src="https://github.com/user-attachments/assets/748c05a9-5760-4a74-8a43-ce0d60a496b1" />
<img width="1280" height="720" alt="슬라이드8" src="https://github.com/user-attachments/assets/e891f76c-086e-47be-be5a-838eca01465b" />



## 📁 구조

```
Packet Cinema/
├── app/                    # 웹사이트 코드
├── security/
│   ├── modsecurity/        # WAF 규칙
│   ├── suricata/           # IDS 규칙
│   └── pfsense/            # 방화벽 설정
├── monitoring/             # Splunk 대시보드
└── tests/                  # 공격 테스트 결과
```

## 🚀 시작하기

### 필수 요구사항
- ModSecurity
- Suricata
- pfSense
- Splunk

## ✅ 검증 결과

<img width="1536" height="1024" alt="Firefly" src="https://github.com/user-attachments/assets/23c727de-3ec9-4b69-856b-11bf98ea929c" />


<img width="1718" height="946" alt="스크린샷 2026-08-03 170548" src="https://github.com/user-attachments/assets/08bc0c66-6cb9-42dd-b946-d71c4d2b6fe8" />


- ✅ SQL Injection 공격 100% 차단
- ✅ Brute Force 공격 100% 차단
- ✅ Path Traversal 공격 100% 차단
- ✅ Splunk 실시간 모니터링 성공

## 📌 주요 방어 기법

1. **입력값 검증** - Whitelist 기반 필터링
2. **Rate Limiting** - 비정상 요청 차단
3. **WAF Rules** - ModSecurity OWASP 규칙셋
4. **IPS Detection** - Suricata 시그니처 탐지
5. **Network Filtering** - pfSense 정책 적용

## 사이트 화면 구성

<img width="1902" height="944" alt="스크린샷 2026-08-04 172118" src="https://github.com/user-attachments/assets/b2851f8d-fef6-4899-92d8-1f99f5b3eacc" />

<img width="1903" height="931" alt="스크린샷 2026-08-04 172130" src="https://github.com/user-attachments/assets/2670e03e-06db-483a-b6e7-9742dbd14b48" />

<img width="1914" height="938" alt="스크린샷 2026-08-04 172148" src="https://github.com/user-attachments/assets/6d256e20-71ae-44bd-abfa-12d0a8522cc2" />

<img width="1906" height="938" alt="스크린샷 2026-08-04 172156" src="https://github.com/user-attachments/assets/525b3f61-6024-41f3-be50-3b511eb7aacf" />

<img width="1907" height="932" alt="스크린샷 2026-08-04 172204" src="https://github.com/user-attachments/assets/afae949f-fded-40da-989c-26052bdda2f8" />

<img width="1907" height="935" alt="스크린샷 2026-08-04 172211" src="https://github.com/user-attachments/assets/8534be3c-9066-4124-814e-cfca91d445df" />

<img width="1905" height="939" alt="스크린샷 2026-08-04 172219" src="https://github.com/user-attachments/assets/a05dbafe-899b-4b34-8dbe-1aaa004c32c1" />


## 📝 라이선스

MIT

## 작성자
palantir1997@gmail.com
