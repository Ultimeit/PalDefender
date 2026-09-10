# POST /summon/pal

**エンドポイント:** `POST /v1/pdapi/summon/pal`  
**認証:** ベアラートークン  
**許可:** `REST.Summon.Pal`

## 目的

Spawns a Pal at fixed map coordinates.リクエストでは、`PalID` または `PalTemplate` のいずれかを指定する必要があります。

## リクエストボディ

|フィールド |タイプ |必須 |説明 |
| --- | --- | --- | --- |
| `PalID` | string | |のいずれかPal species ID. Mutually exclusive with `PalTemplate`. |
| `PalTemplate` | string | |のいずれかFilename from `Pals/Templates/`; uses the template's Pal and level. |
| `X`、`Y`、`Z` |番号 |はい |地図座標。 |
| `Level` | integer |いいえ | `PalID` 召喚のレベル (デフォルトは `1`)。テンプレートの場合は無視されます。 |
| `Uncapturable` | bool |いいえ |キャプチャを防止します (デフォルトは `false`)。 |
| `DisableAI` | bool |いいえ |通常の AI を無効にします (デフォルト `false`)。 |
| `DisableDamageMeter` | bool |いいえ |ダメージ追跡を無効にします (デフォルト `false`)。 |
| `DisableStatuses` | array |いいえ |抑制するステータス名。 |

!!! warning "最大 HP の移行"
    `PalTemplate` を使用すると、テンプレートの `HP` 値が生成された Pal の最大 HP になります。`HealthMultiplier` と `HPMultiplier` はリクエストで受け付けられず、レスポンスにも返されなくなりました。既存の REST 連携から削除してください。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/summon-pal.md"

## エラー

標準の `INVALID_TOKEN`、`MISSING_PERMISSION`、`INVALID_JSON`、`REQUEST_FAILED`、および `REQUEST_TIMEOUT` 応答に加えて、このルートは `VALIDATION_FAILED`、`PAL_TEMPLATE_IMPORT_FAILED`、または `SUMMON_PAL_FAILED` を返す場合があります。

## 例

```http
POST /v1/pdapi/summon/pal
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "PalTemplate": "ArenaBoss.json",
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "Uncapturable": true
}
```
