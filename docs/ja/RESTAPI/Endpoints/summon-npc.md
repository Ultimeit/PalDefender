# POST /summon/npc

**エンドポイント:** `POST /v1/pdapi/summon/npc`  
**認証:** ベアラートークン  
**許可:** `REST.Summon.NPC`

## 目的

固定マップ座標で NPC を生成します。

## リクエストボディ

|フィールド |タイプ |必須 |説明 |
| --- | --- | --- | --- |
| `NPCID` | string |はい | NPC ID または NPC 文字 ID。 |
| `X`、`Y`、`Z` |番号 |はい |地図座標。 |
| `Level` | integer |いいえ | NPC レベル (デフォルトは `1`)。 |
| `Uncapturable` | bool |いいえ |キャプチャを防止します (デフォルトは `false`)。 |
| `DisableAI` | bool |いいえ |通常の AI を無効にします (デフォルト `false`)。 |

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/summon-npc.md"

## エラー

標準の認証/リクエスト エラーに加えて、このルートは `VALIDATION_FAILED` または `SUMMON_NPC_FAILED` を返す場合があります。

## 例

```http
POST /v1/pdapi/summon/npc
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "NPCID": "PIDF_Soldier_AssaultRifle",
    "Level": 30,
    "X": 230,
    "Y": -486,
    "Z": 4097
}
```
