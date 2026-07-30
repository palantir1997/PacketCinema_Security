# Packet Cinema - Web Security Hardening

영화관 웹사이트 보안 강화 프로젝트

## 🎬 프로젝트 개요

Packet Cinema 웹사이트의 취약점을 패치하고, **ModSecurity + Suricata + pfSense**를 이용한 다층 방어 시스템 구축

[![Packet Cinema - 모의 해킹 및 방어 테스트](https://img.youtube.com/vi/oH_uLIhvd5Q/maxresdefault.jpg)](https://www.youtube.com/watch?v=oH_uLIhvd5Q)

<img width="1280" height="720" alt="슬라이드9" src="https://github.com/user-attachments/assets/f2a9ea67-0f77-4175-95b5-c42efc105baf" />

### 기술스택/환경구성
<img width="1280" height="720" alt="슬라이드10" src="https://github.com/user-attachments/assets/a9d4f21b-04b4-4ef0-8fc8-1c89a3053d62" />
<img width="1280" height="720" alt="슬라이드11" src="https://github.com/user-attachments/assets/063a17fb-e4dc-4521-a31d-ff14a978b224" />

## 🛡️ 현재 구축 환경

<img width="1536" height="1024" alt="구축환경" src="https://github.com/user-attachments/assets/51480634-b481-4a62-8083-264990ebdda2" />

## 🛡️ 구현 기능

### 기존 취약점 패치
- 발견된 모든 보안 결함 수정
- 코드 보안 강화

### 다층 방어 시스템
- **ModSecurity**: WAF (웹 애플리케이션 방화벽)
- **Suricata**: IDS (침입 탐지 시스템)
- **pfSense**: 네트워크 방화벽

### 공격 테스트 & 차단 검증

| 공격 유형 | OWASP | 결과 |
|----------|-------|------|
| **SQL Injection** | A03:2021 | ✅ 차단됨 |
| **Brute Force** | A07:2021 | ✅ 차단됨 |
| **Path Traversal** | A01:2021 | ✅ 차단됨 |

## 📊 모니터링

Splunk를 통한 실시간 보안 이벤트 모니터링 및 분석

<img width="1280" height="720" alt="슬라이드1" src="https://github.com/user-attachments/assets/54d9b451-e237-4dfb-9b7c-5cc71a1d4ddf" />
<img width="1280" height="720" alt="슬라이드2" src="https://github.com/user-attachments/assets/4c110d38-27cf-42c0-93ce-129e6d5c04be" />
<img width="1280" height="720" alt="슬라이드3" src="https://github.com/user-attachments/assets/ba31fc8e-a9c5-430e-a2cb-a86f1c82b471" />
<img width="1280" height="720" alt="슬라이드4" src="https://github.com/user-attachments/assets/6a1a8157-270f-4640-9a84-50b8eb6b5355" />
<img width="1280" height="720" alt="슬라이드5" src="https://github.com/user-attachments/assets/3b74a15e-d5ec-4d28-91e3-f4ebf8058d0e" />
<img width="1280" height="720" alt="슬라이드6" src="https://github.com/user-attachments/assets/28a725ff-f0d5-4691-88b4-9b1fe5687e58" />
<img width="1280" height="720" alt="슬라이드7" src="https://github.com/user-attachments/assets/4997fb9a-9cd9-4600-b5ff-9a4c347f4317" />
<img width="1280" height="720" alt="슬라이드8" src="https://github.com/user-attachments/assets/868defac-1380-4fe6-9a21-3899374b73ef" />

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

## 📸 결과 화면

- ModSecurity 차단 로그
- Suricata 탐지 알림
- Splunk 대시보드

## 👥 팀

[팀원 정보]

## 📝 라이선스

MIT
