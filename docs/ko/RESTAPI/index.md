# PalDefender REST API

이 섹션에서는 PalDefender에 내장된 REST API를 설명합니다. **로컬 또는 신뢰할 수 있는 환경**에서 사용하도록 설계된 경량 HTTP 인터페이스입니다.

- **기본 URL:** `http://127.0.0.1:17993`
- **인증:** Bearer 토큰 (모든 엔드포인트에서 필수)
- **버전 확인 엔드포인트:** `/v1/pdapi/version`

> 보안 안내: 이 포트를 인터넷에 직접 공개하지 **마세요**. 원격 접속이 필요하면 리버스 프록시와 적절한 접근 제어를 사용하세요.

## 문서 안내
- [인증 및 설정](authentication.md)
- [엔드포인트](Endpoints/index.md)
