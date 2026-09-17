# 인증 및 설정

## API 활성화

1. `Win64/PalDefender/RESTAPI/RESTConfig.json`을 여세요.
2. `"Enabled"`를 `true`로 설정하세요.
3. 서버를 재시작하세요.

시작 시 다음과 비슷한 로그가 표시됩니다. 아래는 의미를 한국어로 옮긴 예시이며, 실제 서버 로그는 영어로 출력됩니다.
```
[16:42:28][info] [RESTAPI] 'RESTConfig.json'을 불러왔습니다.
[16:42:31][info] [RESTAPI] Bearer 토큰 1개를 불러왔습니다.
[16:42:31][info] [RESTAPI] 포트 17993에서 PalDefender RESTAPI를 실행합니다.
```

## 포트

- **기본 포트:** `17993`

**인터넷에 공개하지 마세요.** 로컬 네트워크나 서버 외부에서 API에 접속하려면 **리버스 프록시**(nginx / Caddy / Traefik)를 앞에 두고 프록시에서 TLS 연결을 처리하세요. 실제 PalDefender REST API는 localhost 또는 사설 네트워크 인터페이스에 바인딩해 두세요.

## 토큰

- 서버를 한 번 실행하면 예제 토큰이 생성됩니다.
- `Win64/PalDefender/RESTAPI/Tokens/` 안의 모든 `.json` 파일을 유효한 토큰 파일로 취급합니다. 단, `TokenExample.json`은 제외됩니다!
- **사용자 또는 서비스마다 별도의 토큰**을 만드세요. 토큰은 비밀번호와 같습니다.

토큰 파일 예제:

```json
{
  "Name": "AdminPanel",
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa",
  "Permissions": [
    "REST.*"
  ]
}
```

`Permissions`에는 문자열 또는 문자열 배열을 지정할 수 있습니다. 공개 대시보드나 전체 관리자 권한이 필요 없는 자동화에는 필요한 권한만 부여하세요.

## 헤더
표준 Authorization 헤더로 토큰을 전송하세요.
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Python 예제
```py
import requests

base_url = "http://127.0.0.1:17993"
# 예제용 코드입니다. 실제 토큰을 코드에 저장하지 마세요. .env 등을 사용하세요!
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```
