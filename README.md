# Packet Cinema - Web Security Hardening

영화관 웹사이트 보안 강화 프로젝트

## 🎬 프로젝트 개요

Packet Cinema 웹사이트의 취약점을 패치하고, **ModSecurity + Suricata + pfSense**를 이용한 다층 방어 시스템 구축

[![[가상 영화관 웹 취약점 진단] OWASP Top 10 (SQL Injection, Brute Force, Path Traversal) 모의 해킹 및 방어 테스트](https://img.youtube.com/vi/VvKSCRkPEwg/maxresdefault.jpg)](https://www.youtube.com/watch?v=VvKSCRkPEwg)

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

![Splunk Dashboard](./images/splunk-dashboard.png)

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
