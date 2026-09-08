# 🛠️ `Config.json`

`Config.json` は、初回起動時に `<PalServer>/Pal/Binaries/Win64/PalDefender/` に生成されます。編集する前にサーバーを停止するか、変更を保存した後に `/reloadcfg` を使用してください。

!!! note "生成された設定"
    PalDefender は、現在の設定セットをこのファイルに書き込みます。以下に記載されていないキーは、廃止済み、移行専用、または現在のリリースビルドでは利用できないものです。

## 一般と強制

|キー |タイプ |デフォルト |説明 |
| --- | --- | --- | --- |
| `version` | string |現在のバージョン |構成スキーマ/バージョン マーカーは PalDefender によって維持されます。 |
| `MOTD` | array | 3 つのメッセージ |メッセージに参加します。 `{ServerName}`、`{PlayerName}`、`{Difficulty}`、`{DeathPenalty}`、`{AllowGlobalPalboxExport}`、`{AllowGlobalPalboxImport}`、`{IsPvP}`、`{IsHardcore}`、`{FriendlyFire}`、`{DayTimeSpeedRate}`、`{NightTimeSpeedRate}`、 `{ExpRate}`、`{PalCaptureRate}`、`{PalSpawnNumRate}`、`{PalEggDefaultHatchingTime}`、`{EnemyDropItemRate}`、`{PalStomachDecreaceRate}`、`{PalStaminaDecreaceRate}`、`{BaseCampMaxNumInGuild}`、`{SupplyDropSpan}`、および `{MaxBuildingLimitNum}`。 |
| `exitServerOnStartupFailure` | bool | `true` | PalDefender が初期化できない場合はサーバーを停止します。一部のホストはこれをクラッシュと解釈し、繰り返し再起動する場合があります。 |
| `preventAdminPasswordInChat` | bool | `true` |管理者パスワードがチャット テキストとして送信されるのをブロックします。 |
| `shouldWarnCheaters` | bool | `true` |自動検出がトリガーされるとプレーヤーに警告します。 |
| `shouldWarnCheatersReason` | bool | `false` |その警告には検出理由が含まれます。 |
| `shouldKickCheaters` | bool | `true` |より強力な有効化アクションが適用されない限り、検出された不正行為者をキックします。 |
| `shouldBanCheaters` | bool | `false` |アカウント禁止により不正行為者が検出されました。 |
| `shouldIPBanCheaters` | bool | `false` | IP - 検出された不正行為者を禁止します。 |
| `blockEmergencyRespawn` | bool | `true` | 「メニュー」→「緊急リスポーン」アクションをブロックします。 |

## RCON とロギング

|キー |タイプ |デフォルト |説明 |
| --- | --- | --- | --- |
| `RCONTimeout` | float | `31.0` |非アクティブな RCON 接続がタイムアウトになる数秒前。 |
| `RCONbase64` | bool | `false` | Base64 でエンコードされた RCON コマンドを有効にします。 |
| `logNetworking` | bool | `false` |サポートされているネットワーク ログを書き込みます。現在のパブリック ビルドではネットワーク ログが無効になっています。 |
| `logNetworkingToConsole` | bool | `true` |ネットワーク ログが利用可能な場合、ネットワーク ログをコンソールにミラーリングします。 |
| `logChat` | bool | `true` |グローバル、ギルド、チャットのログを記録します。 |
| `logRCON` | bool | `false` | RCON コマンドをログに記録します。 |
| `logPlayerUID` | bool | `false` |関連ログとアンチチート Webhook に PlayerUID が含まれます。 |
| `logPlayerIP` | bool | `true` |関連ログとアンチチート Webhook に IP アドレスが含まれます。 |
| `logPlayerDeaths` | bool | `true` |プレイヤーの死亡と殺害を記録します。 |
| `logPlayerLogins` | bool | `true` |プレーヤーの参加と退出を記録します。 |
| `logPlayerBuildings` | bool | `true` |サポートされる構築、キャンセル、解体、および Palbox の移動アクティビティをログに記録します。 |
| `logPlayerSummons` | bool | `true` |プレイヤーのレイドボス召喚を記録します。 |
| `logPlayerCaptures` | bool | `true` |予約済みの互換性設定。利用可能なイベントの信頼性が低いため、1.9.0 ではキャプチャ ログが無効になっています。 |
| `logPlayerDamage` | bool | `false` |プレイヤーが与えたダメージイベントと、報告された Native／Base Damage の値をサーバーコンソールへ記録します。ダメージチート検出とは独立して動作します。 |
| `BannedCampWorker` | array |パンタルスの亜種 |拠点では付与できないキャラクターID。照合では大文字と小文字が区別されません。 `BOSS_...` などのバリアントは個別にリストする必要があります。 |
| `logHelicopterKills` | bool | `true` |戦闘ヘリコプターによる撃墜数を記録します。 |
| `logCraftings` | bool | `true` |ログプレイヤーのクラフト。 |
| `logTechUnlocks` | bool | `true` |ログテクノロジーのロックが解除されます。 |
| `logOpenOilrigBoxes` | bool | `true` |石油掘削装置のエンドゴールボックスのイベントをログに記録します。 |
| `OilrigGoalBoxLocktime` |整数 | `300` |石油掘削装置のエンドゴールボックスがロックされたままの秒数。 |

## Discord Webhook

`PalWebhooks` は object です。その宛先を無効にするには、個々の URL を空のままにしておきます。 Webhook 配信はキューに入れられるため、ゲーム スレッドをブロックするのではなく、バーストが時間差で行われます。

|ネストされたキー |送信 |
| --- | --- |
| `webhookURL_Chat` |グローバル チャット メッセージと Say チャット メッセージ。 |
| `webhookURL_GuildChat` |ギルド名を含むギルドチャットメッセージ。 |
| `webhookURL_Commands` |コマンドは、管理者や完全なコマンドを含め、ゲーム内チャットを通じて実行されます。 |
| `webhookURL_Deaths` |死と殺害。 `announcePlayerDeaths` または `logPlayerDeaths` が必要です。 |
| `webhookURL_JoinLeave` | `announceConnections` が有効な場合のイベントへの参加/退出。 `dontAnnounceAdminConnections` を尊重します。 |
| `webhookURL_Summons` |プレイヤー/管理者の召喚アナウンスと完全な追跡召喚ダメージ結果。 |
| `webhookURL_Oilrig` |対応する `announce...` 設定が有効になっている場合、石油掘削装置のボックスとヘリコプターは破壊されます。 |
| `webhookURL_AntiCheats` |自動および手動でのアンチチート検出のレビュー。 UID/IP は、`logPlayerUID` および `logPlayerIP` に続きます。 |

```json
"PalWebhooks": {
    "webhookURL_Chat": "",
    "webhookURL_GuildChat": "",
    "webhookURL_Commands": "",
    "webhookURL_Deaths": "",
    "webhookURL_JoinLeave": "",
    "webhookURL_Summons": "",
    "webhookURL_Oilrig": "",
    "webhookURL_AntiCheats": ""
}
```

## 管理、チャット、お知らせ

|キー |タイプ |デフォルト |説明 |
| --- | --- | --- | --- |
| `useAdminWhitelist` | bool | `true` |管理者のログイン/コマンドを `adminIPs` に制限します。 |
| `adminAutoLogin` | bool | `false` |ホワイトリストに登録された IP に参加する場合、管理モードを自動的に有効にします。 |
| `adminIPs` | array | `127.0.0.1` |サーバーの管理を許可される正確な IP およびサポートされているワイルドカード エントリ。 |
| `bannedChatWords` | array | RMT の一般的な用語 |大文字と小文字を区別しないチャット フィルター用語。 |
| `bannedNames` | array |既知の虐待の名前 |ログイン時にプレーヤー名が拒否されました。 |
| `allowAdminCheats` | bool | `false` |管理者が `adminCheats` のコマンドを使用し、選択した保護をバイパスできるようにします。 Admin Gun 自体には、アクティブなゲーム内管理者ステータスのみが必要です。 |
| `allowGodmodeOnehit` | bool | `false` |ゴッドモードユーザーは一撃ダメージを与えることができます。 |
| `adminCheats` | array |生成されたリスト | `allowAdminCheats` が無効になっている場合、コマンドは管理チートとして扱われます。 RCON はこのリストではブロックされません。 |
| `announceConnections` | bool | `false` |チャットへの参加/退席をアナウンスし、Webhook ソースの参加/退席を有効にします。 |
| `dontAnnounceAdminConnections` | bool | `true` |これらのアナウンスから管理者の参加/退席を非表示にします。 |
| `announcePunishments` | bool | `false` |自動チートキック/禁止を発表します。 |
| `announcePlayerDeaths` | bool | `false` |チャットでプレイヤーの死亡を発表します。 |
| `announceOpenOilrigBoxes` | bool | `false` |石油掘削装置ボックス イベントを発表し、Webhook ソースを有効にします。 |
| `announceHelicopterKills` | bool | `false` |ヘリコプターが殺害され、Webhook ソースが有効になったことを発表します。 |
| `announcePlayerSummons` | bool | `false` |プレイヤーレイドボス召喚を発表。 |
| `announceAdminSummons` | bool | `false` |管理召喚機能を通じて生成された Pals を発表します。 |
| `announceAdminSummonsKill` | bool | `true` |管理上召喚されたPalsの殺害/死亡を発表。 |
| `chatBypassWait` | bool | `true` |メッセージ間の通常のチャット待機を削除します。 |
| `chatMessageMaxLen` |整数 | `128` |受け入れられるチャット メッセージの最大長。 |
| `useWhitelist` | bool | `false` | `WhiteList.json` を有効にします。 |
| `whitelistMessage` | string |生成されたテキスト |拒否されたホワイトリストに登録されていないプレーヤーに表示されるメッセージ。 |
| `steamidProtection` | bool | `true` | UserId の重複した同時使用を拒否します。 |

## ゲームプレイの検証

|キー |タイプ |デフォルト |説明 |
| --- | --- | --- | --- |
| `pvpMaxToBuildingDamage` |整数 | `100` |建物への最大許容PvPダメージ。 |
| `pvpMaxToPalDamage` |整数 | `1000` | Pals に対する最大許容 PvP ダメージ。 |
| `pveMaxToPalBanThreshold` |整数 | `900000` | PvE Pal - チート検出で使用されるダメージのしきい値。 |
| `droppedPalPickupRange` |整数 | `99999` |ドロップされたPalピックアップの最大許容距離。 |
| `treeLimiter` | float | `0.1` |葉のバーストを制限するために使用される木の破壊イベント間の最小秒数。 |
| `disableIllegalItemProtection` | bool | `false` |無効/変更されたアイテムの保護を無効にします。 |
| `disableButchering` | bool | `false` | Pal の解体を禁止します。 |
| `disableRenaming` | bool | `false` |プレーヤーの名前変更をブロックします。 |
| `disablePalRenaming` | bool | `false` | Pal の名前変更を禁止します。 |
| `doActionUponIllegalPalStats` | bool | `true` |不可能な Pal 統計に対して、設定されたチート アクションを適用します。 |
| `preventUnsupportedWorkbenchRecipes` | bool | `true` |要求されたワークベンチでサポートされていないレシピをブロックします。 |
| `preventDoctorSurgiExploit` | bool | `true` | Doctor Surgi エクスプロイトを検出/ブロックします。 |
| `doActionUponDoctorSurgiExploit` | bool | `true` |そのエクスプロイトに対して設定されたチート アクションを適用します。 |
| `palStatsMaxRank` |整数 | `-1` | Pal の最大強化ランク。`-1` の場合は自動的に現在のゲーム上限を使用します。 |
| `bannedTechnologies` | array |空 |テクノロジー ID は学習からブロックされ、検出されると削除されます。 |

## アンチチート機能スイッチ

|キー |タイプ |デフォルト |説明 |
| --- | --- | --- | --- |
| `antiDupeEnabled` | bool | `true` |従来の AntiDupe 機能の互換性スイッチ。現在のリリースのビルドでは非アクティブです。 |
| `antiDupeBuildRateLimitSeconds` | float | `1.5` |従来のビルド間の最小間隔。現在活動停止中。 |
| `antiDupeDismantleRateLimitSeconds` | float | `1.5` |従来の解体間の最小間隔。現在活動停止中。 |
| `antiDupeShowBlockMessage` | bool | `true` |従来のブロックメッセージスイッチ。現在活動停止中。 |
| `antiDupeBuildMessage` | string |生成されたテキスト |従来のビルドブロック メッセージ。現在活動停止中。 |
| `antiDupeDismantleMessage` | string |生成されたテキスト |従来の解体ブロック メッセージ。現在活動停止中。 |
| `antiVacuumEnabled` | bool | `true` |リモートピックアップ（バキューム）保護を有効にします。 |
| `antiVacuumBlockAutoPickup` | bool | `true` |通常の自動ピックアップにアンチバキュームチェックを適用します。 |
| `antiVacuumBlockRelicObtain` | bool | `true` |レリックコレクションにチェックを適用します。 |
| `antiVacuumBlockNoteObtain` | bool | `true` |ノートのコレクションにチェックを適用します。 |
| `antiVacuumBlockEggPickup` | bool | `true` |卵のピックアップにチェックを適用します。 |
| `antiVacuumMaxPickupDistance` | float | `800.0` |保護されたリクエストの最大許容ピックアップ距離。 |
| `antiVacuumShowBlockMessage` | bool | `true` |ピックアップがブロックされている場合、プレイヤーに向けたメッセージを表示します。 |
| `antiVacuumBlockMessage` | string |生成されたテキスト |ブロックされたリモート ピックアップに対して表示されるメッセージ。 |
| `staminaCheatDetectionEnabled` | bool | `true` |不審なスタミナアクションの検出を有効にします。 |
| `baseCampDupeDetectionEnabled` | bool | `true` |ベースキャンプの重複検出を有効にします。 |
| `damageCheatDetectionEnabled` | bool | `true` |ダメージチート検出を有効にします。 |
| `damageCheatDetectionTolerancePercent` | float | `5.0` |報告された Native Damage と、再計算した `BasePower × AttackWithBuff` の値との間で許容する誤差率（%）。 |
| `damageCheatDetectionWeaponBasePowerMultiplier` | float | `1.5` |装備中の武器が持つ静的な `AttackValue` に対して許容する、武器 `BasePower` の最大倍率。 |
| `ammoCheatDetectionEnabled` | bool | `true` |弾薬/武器状態のチート検出を有効にします。 |

`antiDupe...` キーは構成の互換性のために引き続き生成されますが、従来の AntiDupe 機能は現在のリリース ビルドでは無効になっています。機能が再び有効になるまで、これらのコントロールに依存しないでください。

## 従来の移行キー

`PalImport_Disabled`、`PalImport_BanIfPalIsImpossible`、`PalImport_BannedPalIDs`、`PalImport_AllowGenderNone`、`PalImport_MaxLevel`、`PalImport_MaxRank`、`PalImport_MaxSoulHP`、`PalImport_MaxSoulATK`、`PalImport_MaxSoulDEF`、`PalImport_MaxSoulCS`、および `PalImport_MaxIV` は移行の読み取り専用です。古いインストールを [`Pals/ImportRules/Default.json`](./PalImportRules.md) にコピーします。これらは現在の `Config.json` ファイルには書き込まれなくなりました。

古い `RCONUsePacketIdFix`、`bannedIPs`、`bannedMessage`、`isChineseCmd`、および `blockTowerBossCapture` キーは、現在の構成の一部ではありません。禁止レコードは `Banlist.json` に属します。
