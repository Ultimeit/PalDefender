# 特徴と現状

このページには、PalDefender 1.9.1 のユーザー向け機能スイッチがまとめられています。正確なデフォルトについては、[`Config.json`](./FileTypes/Config.md) を参照してください。

## アクティブな保護

- ダメージ、スタミナ、弾薬、ベースキャンプの重複検出を個別に切り替えることができます。
- Anti-Vacuum は、通常のアイテム、Pal 卵、遺物、およびメモに対する不審なリモート ピックアップの試みをブロックします。 `allowAdminCheats` が有効な場合、管理者はサポートされているチェックをバイパスします。
- 無効なアイテム、Pal ステータス、作業台レシピ、Doctor Surgi、緊急リスポーンなどのサーバー操作チェックは、引き続き中央検証レイヤーで処理されます。
- `BannedCampWorker` は、設定されたキャラクター ID がベースで割り当てられるのをブロックします。

`antiDupe...` キーで制御される旧機能は、現在のリリースビルドでは無効化されています。新しい拠点複製検出機能はこれとは独立しており、`baseCampDupeDetectionEnabled` で制御されます。

## 運営とイベント

- `/admingun` (`/agun`) は、保護されたゲーム内 [Admin Gun](./Commands/index.md) をアクティブな管理者に付与します。
- `/setting` は、サポートされているライブ Palworld 設定を検査または一時的に変更できます。
- `/findbases` は、空の/非アクティブなベースの対話型レビュー キューを提供します。
- PalSummon は、遭遇名、AI/ダメージ メーター コントロール、ステータス乗数、条件付きキャプチャ、ランク結果、および設定可能な報酬をサポートしています。 [`PalSummon.json`](./FileTypes/PalSummon.md) を参照してください。
- Discord の送信先は `PalWebhooks` で設定し、チャット、コマンド、死亡、参加・退出、召喚、オイルリグイベント、アンチチート検出を通知できます。

## ハートビート

リリースビルドは、ゲームの準備完了後、10 秒ごとに `https://pallink.net/api/heartbeat` へハートビートを送信します。送信内容には、ワールド／サーバー GUID、OS ロケールの国コード、PalDefender と Palworld のバージョン、Windows／Wine／Proton の実行環境、プロセスの稼働時間、現在／最大／累計ユニークプレイヤー数が含まれます。プレイヤー名、アカウント ID、IP アドレス、チャットメッセージ、セーブデータは含まれません。デバッグビルドでは送信されません。

## REST API

認証付き REST API は、プレイヤー、Pal、インベントリ、テクノロジー、進行状況、ギルド、BAN、メッセージ、報酬、モデレーションの各操作に対応しています。バージョン 1.9.0 では、[`POST /summon/pal`](./RESTAPI/Endpoints/summon-pal.md) と [`POST /summon/npc`](./RESTAPI/Endpoints/summon-npc.md) も追加されました。
