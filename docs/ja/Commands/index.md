# コマンド

## コマンドとは何ですか?

コマンドは、ゲームを操作できるようにする特別なテキストベースの指示です。チャットにコマンドを入力すると、テレポート、クリーチャーのスポーン、プレイヤーの管理などのアクションを実行できます。コマンドは通常、<span class="var-command">/</span> で始まり、その後にコマンド名とオプションの引数が続きます。

## コマンドを使用できるのは誰ですか?

**現在、管理者以外のプレイヤーが使用できるコマンドはありません。**
現在のバージョンでは、Admin コマンドと RCON コマンドのみが使用可能です。

## コマンドリスト

!!! note "コマンド構文"
    <span class="var-command">/command_name </span><span class="var-command-arg"><必須引数> </span><span class="var-command-optional">[optional_argument={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg"><required_argument></span> → 必ず含める必要があります。<br>
    <span class="var-command-optional">[optional_argument={?}]</span> →省略可能。 <span class="var-command-optional">{?}</span> は、省略された場合に使用されるデフォルト値を示します。
    </p>
    <p>
    引数にはさまざまな種類があります。最も一般的なのは、<span class="var-string">strings</span>、<span class="var-number">numbers</span>、<span class="var-float">floats</span>、および <span class="var-bool">booleans</span> です。一部のコマンドには、特別なディレクトリ内の特定の <span class="file">filenames</span> や、実際には <span class="var-filter">filter</span> など、複雑なタイプもあります。
    </p>

!!! tip "ID検索"
    `PalID` には [paldeck.cc/pals](https://paldeck.cc/pals)、`ItemID` には [paldeck.cc/items](https://paldeck.cc/items)、`TechID` には [paldeck.cc/technology](https://paldeck.cc/technology)、`TechID` には [paldeck.cc/buildings](https://paldeck.cc/buildings) を使用します。 `BuildingID`、`PassiveID` の場合は [paldeck.cc/passives](https://paldeck.cc/passives)、スキル ID の場合は [paldeck.cc/skills](https://paldeck.cc/skills)。

??? note "RCON のみ"
    ??? info "/getrconcmds"
        **構文:** `/getrconcmds`

        **説明:** RCON で使用できる、必要な引数カウントを含むすべてのコマンドのリストを返します。

        **引数:**

        - なし

        **権限:** `RCON`

        **例:**
        ```
        /getrconcmds
        ```

??? note "サーバー管理"
    ??? info "/version"
        **構文:** `/version`

        **説明:** Palworld ゲームのバージョンと PalDefender のバージョンを表示します。 RCON は JSON 出力を返します。

        **引数:**

        - なし

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /version
        ```

    ??? info "/reloadcfg"
        **構文:** `/reloadcfg`

        **説明:** `Config.json`、`WhiteList.json`、および PalDefender 禁止データをリロードします。

        **引数:**

        - なし

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /reloadcfg
        ```

    ??? info "/addadminip"
        **構文:** `/addadminip <IP>`

        **説明:** IP アドレスを管理者ホワイトリストに追加します。

        **引数:**

        - `<IP>`: 管理者として追加する IP アドレス。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /addadminip 192.168.1.1
        ```

    ??? info "/setadmin"
        **構文:** `/setadmin <UserId>`

        **説明:** プレイヤーに一時的に管理者を付与または取り消します。

        **引数:**

        - `<UserId>`: 管理者を付与/取り消すプレーヤーの ID。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /setadmin steam_76500000000000000
        ```

    ??? info "/pgbroadcast"
        **構文:** `/pgbroadcast <Message>`

        **説明:** サーバー内のすべてのプレイヤーにメッセージを送信します。

        **引数:**

        - `<Message>`: ブロードキャストするメッセージ。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /pgbroadcast "Server will restart soon."
        ```

    ??? info "/adminlogin"
        **構文:** `/adminlogin <password>`

        **説明:** 管理者モードにログインします。引数として管理者パスワードが必要です。

        **引数:**

        - `<password>`: 管理者パスワード。

        **権限:** `Chat`

        **例:**
        ```
        /adminlogin mySecretPassword
        ```

    ??? info "/adminlogout"
        **構文:** `/adminlogout`

        **説明:** 管理者モードからログアウトします。

        **引数:**

        - なし

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /adminlogout
        ```

    ??? info "/iwantplayerlist"
        **構文:** `/iwantplayerlist`

        **説明:** ゲーム内のプレーヤー リスト オーバーレイを有効にし、ESC キーを押したときにすべてのプレーヤーの UserId とプレーヤー UID を表示できるようにします。ゲーム インターフェイスで詳細なプレーヤー情報を直接確認したいサーバー管理者やプレーヤーに役立ちます。

        **引数:**

        - なし

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /iwantplayerlist
        ```

    ??? info "/getpos"
        **構文:** `/getpos [UserId]`

        **説明:** 世界での現在の位置を取得します。これは、テレポート、召喚、および同様のアクションに使用できます。 [UserId] が指定されている場合は、代わりにそのプレーヤーの位置を取得します。

        **引数:**

        - `[UserId]`: (オプション) ポジションを取得したいプレーヤーの ID。省略した場合は、独自の位置を取得します。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /getpos
        /getpos steam_76500000000000000
        ```

    ??? info "/settime"
        **構文:** `/settime <hour>`

        **説明:** Palworld の時刻を変更します。時間には次の値を指定できます: `0` ～ `23`、`day`、および `night`。

        **引数:**

        - `<hour>`: 時間の値 (0 ～ 23、昼、夜)。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /settime 12
        /settime night
        ```

    ??? info "/togglepvp"
        **構文:** `/togglepvp`

        **説明:** 現在実行中のセッションでサーバー PvP のオンとオフを切り替えます。

        **引数:**

        - なし

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /togglepvp
        ```

    ??? info "/alert"
        **構文:** `/alert <message>`

        **説明:** サーバー上のすべてのプレイヤーに警告メッセージを送信します。通常、このメッセージは画面に目立つように表示されます。

        **引数:**

        - `<message>`: アラートとしてブロードキャストするメッセージ。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /alert Server will restart in 5 minutes!
        ```

    ??? info "/send"
        **構文:** `/send <type> <UserId> <Message>`

        **説明:** 特定のプレーヤーにメッセージまたはログ メッセージを送信できます。

        **引数:**

        - `<type>`: 送信するメッセージのタイプ。可能な値:
             - `msg`: 通常のチャット メッセージ。
             - `log`: 通常のログ メッセージ (白色、すぐに消えます、フォントが大きくなります)。
             - `ilog`: 重要なログ メッセージ (青色、表示時間が長くなります)。
             - `vilog`: 非常に重要なログ メッセージ (青色、非常に長く残ります)。
        - `<UserId>`: メッセージを受信するプレーヤーの ID。
        - `<Message>`: 送信するメッセージ テキスト。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /send msg steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send log steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send ilog steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send vilog steam_76500000000000000 Dont miss out on Qonzer's sale!
        ```

    ??? info "/resetoilrig"
        **構文:** `/resetoilrig <lv30|lv55|lv60|all>`

        **説明:** 選択した石油掘削装置または現在管理されているすべての石油掘削装置をリセットします。

        **権限:** `Chat`、アクティブなゲーム内管理者ステータス。

        **例:**
        ```
        /resetoilrig all
        ```

    ??? info "/setting"
        **構文:** `/setting list [filter]` または `/setting <setting_name> <get|set|add|sub> [value]`

        **説明:** サポートされているライブ `UPalGameSetting` 値を検査または変更します。名前は大文字と小文字を区別せずに照合されます。一意の接頭辞または部分文字列が受け入れられます。これは実験的なものであり、永続的なワールド構成に代わるものではなく、クライアントは引き続きキャッシュされた値を表示する可能性があります。

        - `list [filter]`: サポートされている integer、float、ブール型、バイト型、および列挙型フィールドをリストします。
        - `get`: 値を読み取ります。
        - `set`: サポートされているタイプを設定します。ブール値は `true/false`、`on/off`、`yes/no`、または `1/0` を受け入れます。 enum は数値またはエントリ名を受け入れます。
        - `add` / `sub`: 数値のみを変更します。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /setting list death
        /setting PalDeathPenaltyTime get
        /setting PalDeathPenaltyTime set 10
        ```

    ??? info "/resetbosstower"
        **構文:** `/resetbosstower <BossType|all>`

        **説明:** 1 つのボス タワー インスタンスまたはリセット可能なすべてのボス タワーをリセットするデバッグビルド専用コマンド。単一のターゲットは有効な `EPalBossType` 名を使用する必要があります。パブリック リリース ビルドでは使用できません。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /resetbosstower all
        ```

    ??? info "/showbosses"
        **構文:** `/showbosses`

        **説明:** 現在の Boss 静的情報を `PalDefender/Logs/BossInfo.json` に書き込むデバッグビルド専用のデータマイニング コマンド。パブリック リリース ビルドでは使用できません。

        **権限:** `Chat`、`RCON`、`Admin`

??? note "拠点管理"
    ??? info "/findunusedbases (alias: /findbases)"
        **構文:** `/findbases [empty|inactive|unused|all] [days=N] [builds<=N]`

        **対話型構文:** `/findbases visit [filters]`、`/findbases next`、`/findbases kill [next]`

        **説明:** 空、非アクティブ、または未使用の塩基をスキャンします。 `visit` はチャット専用のレビュー キューを作成し、その最初の結果にテレポートします。 `next` が進みます。 `kill` は選択したベースを破棄します。 `kill next` がそれを破壊して進みます。破壊は元に戻せないため、最初に各ターゲットを検査してください。

        - `empty`: ワーカーは存在せず、最大でもデフォルトの建築制限 (または `builds<=N`) です。
        - `inactive`: オンライン ギルド メンバーがおらず、少なくとも `days` (デフォルト `30`) の間非アクティブです。
        - `unused`: 空または非アクティブと一致します。
        - `all`: 明示的なフィルターを適用しながら、すべての塩基をリストします。

        **権限:** リストは `Chat` および `RCON` をサポートします。訪問/次へ/キルにはゲーム内チャットと管理者の許可が必要です。

        **例:**
        ```
        /findbases empty builds<=5
        /findbases inactive days=14
        /findbases visit unused days=30
        /findbases kill next
        ```

    ??? info "/getnearestbase"
        **構文:** `/getnearestbase [X] [Y] [Z]`

        **説明:** あなたのキャラクターに最も近い基地を所有するギルド名を示します。

        **注:** **RCON** 経由で実行する場合、RCON には位置を決定するプレイヤー キャラクターがないため、すべての位置パラメータ (`[X]` `[Y]` `[Z]`) **が必要です**。

        **引数:**

        - `[X]`: (オプション) X 座標。
        - `[Y]`: (オプション) Y 座標。
        - `[Z]`: (オプション) Z 座標。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /getnearestbase 100 200 50
        ```

    ??? info "/gotonearestbase"
        **構文:** `/gotonearestbase [X] [Y] [Z]`

        **説明:** その場所の最も近い基地にテレポートします。

        **注:** **RCON** 経由で実行する場合、RCON には位置を決定するプレイヤー キャラクターがないため、すべての位置パラメータ (`[X]` `[Y]` `[Z]`) **が必要です**。

        **引数:**

        - `[X]`: (オプション) X 座標。
        - `[Y]`: (オプション) Y 座標。
        - `[Z]`: (オプション) Z 座標。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /gotonearestbase 100 200 50
        ```

    ??? info "/killnearestbase"
        **構文:** `/killnearestbase [X] [Y] [Z]`

        **説明:** 最も近い基地を破壊します (**使用には注意してください!**)。

        **注:** **RCON** 経由で実行する場合、RCON には位置を決定するプレイヤー キャラクターがないため、すべての位置パラメータ (`[X]` `[Y]` `[Z]`) **が必要です**。

        **引数:**

        - `[X]`: (オプション) X 座標。
        - `[Y]`: (オプション) Y 座標。
        - `[Z]`: (オプション) Z 座標。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /killnearestbase 100 200 50
        ```


??? note "プレイヤーマネジメント"
    ??? info "/kick"
        **構文:** `/kick <UserId> [Reason="Kicked by Admin."]`

        **説明:** プレーヤーをサーバーからキックします。

        **引数:**

        - `<UserId>`: キックするプレーヤーの ID。
        - `[Reason]`: (オプション) キックの理由。デフォルト:「管理者によってキックされました」。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /kick steam_76500000000000000 "Spamming in chat"
        ```

    ??? info "/ban"
        **構文:** `/ban <UserId> [Reason="Banned by Admin."]`

        **説明:** プレイヤーを禁止し、サーバーから追い出します。

        **引数:**

        - `<UserId>`: 禁止するプレイヤーの ID。
        - `[Reason]`: (オプション) 禁止の理由。デフォルト: 「管理者によって禁止されています。」

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /ban gdk_25300000000000000 "Cheating"
        ```

    ??? info "/ipban"
        **構文:** `/ipban <UserId> [Reason="Banned by Admin."]`

        **説明:** プレーヤーの IP アドレスを禁止し、サーバーからキックします。

        **引数:**

        - `<UserId>`: IP 禁止するプレイヤーの ID。
        - `[Reason]`: (オプション) 禁止の理由。デフォルト: 「管理者によって禁止されています。」

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /ipban steam_76500000000000000
        ```

    ??? info "/banip"
        **構文:** `/banip <IP>`

        **説明:** IP アドレスをサーバーから禁止します。

        **引数:**

        - `<IP>`: 禁止する IP アドレス。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /banip 192.168.1.1
        ```

    ??? info "/unbanip"
        **構文:** `/unbanip <IP>`

        **説明:** IP アドレスを禁止リストから削除します。

        **引数:**

        - `<IP>`: 禁止を解除する IP アドレス。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /unbanip 192.168.1.1
        ```

    ??? info "/unban"
        **構文:** `/unban <UserId> [Reason="Unbanned by admin."]`

        **説明:** PalDefender 禁止リストから UserId を削除します。

        **引数:**

        - `<UserId>`: 禁止を解除する UserId。
        - `[Reason]`: (オプション) 禁止解除アクションに対して保存された理由。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /unban steam_76500000000000000 "Appeal accepted"
        ```

    ??? info "/getip"
        **構文:** `/getip <UserId>`

        **説明:** プレーヤーの IP アドレスを表示します。

        **引数:**

        - `<UserId>`: プレーヤーの ID。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /getip gdk_25300000000000000
        ```

    ??? info "/whitelist_add"
        **構文:** `/whitelist_add <UserId>`

        **説明:** UserId をホワイトリストに追加します。

        **引数:**

        - `<UserId>`: ホワイトリストに登録するプレーヤーの ID。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /whitelist_add steam_76500000000000000
        ```

    ??? info "/whitelist_remove"
        **構文:** `/whitelist_remove <UserId>`

        **説明:** ホワイトリストから UserId を削除します。

        **引数:**

        - `<UserId>`: ホワイトリストから削除するプレーヤーの ID。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /whitelist_remove gdk_25300000000000000
        ```

    ??? info "/whitelist_get"
        **構文:** `/whitelist_get`

        **説明:** ホワイトリストに登録されたプレーヤーの完全なリストを表示します。

        **引数:**

        - なし

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /whitelist_get
        ```

    ??? info "/imcheater"
        **構文:** `/imcheater`

        **説明:** これを使用して、サーバーが不正行為者にどのように応答するかをテストします。

        **引数:**

        - なし

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /imcheater
        ```

    ??? info "/spectate"
        **構文:** `/spectate`

        **説明:** 観戦モードをオンにします。ホットキー `\` を押すのと同じですが、ホットキーはコンソール プレーヤーなど、すべての人に機能するわけではありません。

        **引数:**

        - なし

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /spectate
        ```

??? note "プレイヤーキャラクター"
    ??? info "/tp"
        **構文:**
        以下のいずれかの作品：

        - `/tp <UserId>`
        - `/tp <UserId1> <UserId2>`
        - `/tp <X> <Y>`
        - `/tp <X> <Y> <Z>`
        - `/tp <UserId> <X> <Y>`
        - `/tp <UserId> <X> <Y> <Z>`
        - `/tp home`
        - `/tp oilrig`
        - `/tp oilrig:Lv30`
        - `/tp oilrig:Lv55`
        - `/tp oilrig:Lv60`

        **説明:** 自分自身、または指定されたプレイヤーを、別のプレイヤー、座標、最も近い所有基地、または石油採掘場の目的地にテレポートします。

        **注意:** RCON にはゲーム内キャラクターがないため、RCON にはテレポートされるプレイヤーを含める必要があります。

        **引数:**

        - `<UserId>`: テレポート先のプレーヤー、またはさらに引数が指定された場合にテレポートされるプレーヤー。
        - `<UserId1>`: テレポートするプレイヤー。
        - `<UserId2>`: ターゲットプレイヤー。
        - `<X> <Y> [Z]`: マップ座標。 `Z` が省略された場合、PalDefender は使用可能な地面の高さを見つけようとします。
        - `home`: 最も近い所有基地にテレポートします。
        - `oilrig`、`oilrig:Lv30`、`oilrig:Lv55`、`oilrig:Lv60`: 石油掘削装置の目的地にテレポートします。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /tp steam_76500000000000000 gdk_25300000000000000
        /tp 100 -250
        /tp oilrig:Lv60
        ```

    ??? info "/give_exp"
        **構文:** `/give_exp <UserId> <Amount>`

        **説明:** プレイヤーに経験値を与えます。

        **引数:**

        - `<UserId>`: プレーヤーの ID。
        - `<Amount>`: 経験値の量。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /give_exp gdk_25300000000000000 1000
        ```

    ??? info "/giveme_exp"
        **構文:** `/giveme_exp <Amount>`

        **説明:** 自分自身に経験値を与えます。

        **引数:**

        - `<Amount>`: 経験値の量。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /giveme_exp 1000
        ```

    ??? info "/renameplayer"
        **構文:** `/renameplayer <UserId> <NewName>`

        **説明:** プレイヤーのニックネームの名前を変更します。

        **引数:**

        - `<UserId>`: プレーヤーの ID。
        - `<NewName>`: 新しいニックネーム。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /renameplayer steam_76500000000000000 NewNickname
        ```

    ??? info "/givestats"
        **構文:** `/givestats <UserId> [Count=1]`

        **説明:** プレイヤーに 1 つ以上の未使用ステータス ポイントを与えます (負の値は減算されます)。すでに使用されているポイントには影響しません。

        **引数:**

        - `<UserId>`: ステータス ポイントを受け取るプレイヤーの ID。
        - `[Count]`: (オプション) 与える未使用のステータス ポイントの数 (減算するには負の値にすることもできます)。デフォルト: 1。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /givestats steam_76500000000000000 5
        /givestats steam_76500000000000000 -2
        ```

    ??? info "/givemestats"
        **構文:** `/givemestats [Count=1]`

        **説明:** 1 つ以上の未使用ステータス ポイントを自分に与えます (負の値は減算されます)。すでに使用されているポイントには影響しません。

        **引数:**

        - `[Count]`: (オプション) 自分に与える未使用のステータス ポイントの数 (マイナスの値を引くこともできます)。デフォルト: 1。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /givemestats 5
        /givemestats -2
        ```

    ??? info "/godmode"
        **構文:** `/godmode [on/off]`

        **説明:** ステータス効果に対する免疫を含む無敵性を付与し、食物の摂取を拒否し、発動時に健康を回復します。設定で有効になっている場合は、オプションですべてをワンショットで実行できます。

        **引数:**

        - `[on/off]`: (オプション) ゴッドモードを明示的に有効または無効にします。デフォルト: オンとオフを切り替えます。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /godmode
        /godmode on
        /godmode off
        ```

    ??? info "/admingun (alias: /agun)"
        **構文:** `/admingun`

        **説明:** アクティブなゲーム内管理者に、保護された Admin Gun を与えます。キャラクターを即座に殺し、マップオブジェクトを破壊し、葉へのダメージを最大化し、弾薬と耐久性は無制限で、ドロップしたり、販売したり、外部コンテナに移動したりすることはできません。ストレージ object を破壊しながらしゃがむと、その内容が削除されます。それらを保存するために立ったままにしてください。銃は死亡時、ログアウト時、または管理者ログアウト時に削除され、別の銃を要求すると既存のコピーが置き換えられます。

        **権限:** `Chat`、アクティブなゲーム内管理者ステータス。 `allowAdminCheats` は必要ありません。

        **例:**
        ```
        /agun
        ```

??? note "ギルド運営"
    ??? info "/setguildleader"
        **構文:** `/setguildleader <UserId>`

        **説明:** ターゲット プレイヤーを現在のギルドのリーダーにします。

        **引数:**

        - `<UserId>`: ギルドリーダーにするプレイヤーのID。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **構文:** `/exportguilds`

        **説明:** サーバーのすべてのギルドを Pal/Binaries/Win64/PalDefender/guildexport.json にダンプします。

        **引数:**

        - なし

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /exportguilds
        ```
        出力ファイルの例: `Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "アイテム"
    ??? info "/give"
        **構文:** `/give <UserId> <ItemId> [Amount=1]`

        **説明:** プレイヤーにアイテムを与え、指定されている場合はその数を与えます。

        **引数:**

        - `<UserId>`: アイテムを渡すプレイヤーの ID。
        - `<ItemId>`: 与えるアイテム。
        - `[Amount]`: (オプション) いくつ。デフォルト: 1。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /give steam_76500000000000000 Sword 2
        ```

    ??? info "/giveitems"
        **構文:** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

        **説明:** 1 つのコマンドでプレイヤーに複数のアイテムを与えます。指定されている場合は、それぞれのアイテムの数をコロンで区切ります。

        **引数:**

        - `<UserId>`: アイテムを渡すプレイヤーの ID。
        - `<ItemId>[:<Amount>] ...`: アイテムとオプションの金額のリスト。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /giveitems gdk_25300000000000000 Sword:2 Shield:1
        ```

    ??? info "/giveme"
        **構文:** `/giveme <ItemId> [Amount=1]`

        **説明:** 自分自身にアイテムを 1 つ、指定されている場合はその数を与えます。

        **引数:**

        - `<ItemId>`: 自分に贈るアイテム。
        - `[Amount]`: (オプション) いくつ。デフォルト: 1。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /giveme Sword 3
        ```

    ??? info "/delitem"
        **構文:** `/delitem <UserId> <ItemId> [Amount=1]`

        **説明:** プレーヤーからアイテムを削除し、指定されている場合はその数を削除します。デフォルトは `1` で、その項目が 1 つだけ削除されます。すべての出現を削除するには、`1` の代わりに `all` を使用します。

        **引数:**

        - `<UserId>`: プレーヤーの ID。
        - `<ItemId>`: 削除する項目。
        - `[Amount]`: (オプション) いくつ。デフォルト: 1. すべての出現を削除するには、`all` を使用します。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /delitem steam_76500000000000000 Sword 1
        /delitem gdk_25300000000000000 Sword all
        ```

    ??? info "/give_relic"
        **構文:** `/give_relic <UserId> <RelicType> [Amount]`

        **説明:** 選択したタイプの 1 つ以上のレリック ポイントをプレイヤーに与えます。

        **引数:**

        - `<UserId>`: レリックポイントを受け取るプレイヤーのID。
        - `<RelicType>`: 付与するレリックのタイプ。

        - `[Amount]`: 与えるレリックポイントのオプションの数。デフォルトは `1` です。

        **サポートされているレリック タイプ:** `CapturePower`、`HungerReduction`、`SwimSpeed`、`FoodDecayReduction`、`JumpPower`、`GliderSpeed`、`ClimbSpeed`、`StatusAilmentResist`、`StaminaReduction`、`SphereHoming`、 `ExpBonus`、`RainbowPassiveRate`、`MoveSpeed`。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /give_relic steam_76500000000000000 CapturePower 5
        ```

    ??? info "/giveme_relic"
        **構文:** `/giveme_relic <RelicType> [Amount]`

        **説明:** 選択したタイプのレリック ポイントを 1 つ以上自分に与えます。

        **引数:**

        - `<RelicType>`: 付与するレリックのタイプ。

        - `[Amount]`: 自分に与えるレリックポイントのオプションの数。デフォルトは `1` です。

        **サポートされているレリック タイプ:** `CapturePower`、`HungerReduction`、`SwimSpeed`、`FoodDecayReduction`、`JumpPower`、`GliderSpeed`、`ClimbSpeed`、`StatusAilmentResist`、`StaminaReduction`、`SphereHoming`、 `ExpBonus`、`RainbowPassiveRate`、`MoveSpeed`。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /giveme_relic CapturePower 5
        ```


    ??? info "/delitems"
        **構文:** `/delitems <UserId> <ItemId>[:<Amount>] ...`

        **説明:** 1 つのコマンドでプレーヤーから複数のアイテムを削除します。指定されている場合は、それぞれのアイテムの数をコロンで区切って削除します。すべての出現を削除するには、`1` の代わりに `all` を使用します。

        **引数:**

        - `<UserId>`: プレーヤーの ID。
        - `<ItemId>[:<Amount>] ...`: アイテムとオプションの金額のリスト。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /delitems steam_76500000000000000 Sword:1 Shield:all
        ```

    ??? info "/clearinv"
        **構文:** `/clearinv <UserId> [Container=items] ...`

        **説明:** プレイヤーのインベントリから指定されたコンテナをクリアします。使用可能なコンテナー: `items`、`keyitems`、`armor`、`weapons`、`food`、`dropslot`、または `all`。

        **引数:**

        - `<UserId>`: プレーヤーの ID。
        - `[Container] ...`: (オプション) クリアするコンテナ。デフォルト: アイテム。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /clearinv steam_76500000000000000 items
        /clearinv gdk_25300000000000000 all
        ```


??? note "Pals"
    ??? info "/givepal"
        **構文:** `/givepal <UserId> <PalId> [Level=1]`

        **説明:** 指定されたレベルのプレイヤーに Pal を与えます。

        **引数:**

        - `<UserId>`: プレーヤーの ID。
        - `<PalId>`: 与える Pal。
            - **注:** Pal ID (例: `WeaselDragon` (チレット)) を使用してください。完全なリストは [paldeck.cc/pals](https://paldeck.cc/pals) でご覧ください。
        - `[Level]`: (オプション) Pal のレベル。デフォルト: 1。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **構文:** `/givepal_j <UserID> <PalTemplate>`

        **説明:** PalTemplate ファイルによって定義された Pal をプレーヤーに提供します。埋め込み JSON はサポートされなくなりました。ファイル名のみが受け入れられます。

        **注意:** ファイル名に .json 拡張子を含める必要はありません。見つからない場合は、システムが自動的に追加します。

        **引数:**

        - `<UserID>`: プレーヤーの ID。
        - `<PalTemplate>`: PalTemplate ファイルの名前 ([PalTemplate](../FileTypes/PalTemplate.md) を参照)。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **構文:** `/givemepal <PalId> [Level=1]`

        **説明:** 指定されたレベルで自分自身に Pal を与えます。

        **引数:**

        - `<PalId>`: 自分自身に与える Pal。
            - **注:** Pal ID (例: `WeaselDragon` (チレット)) を使用してください。完全なリストは [paldeck.cc/pals](https://paldeck.cc/pals) でご覧ください。
        - `[Level]`: (オプション) Pal のレベル。デフォルト: 1。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **構文:** `/givemepal_j <PalTemplate>`

        **説明:** PalTemplate ファイルによって定義された Pal を自分自身に与えます。埋め込み JSON はサポートされなくなりました。ファイル名のみが受け入れられます。

        **引数:**

        - `<PalTemplate>`: PalTemplate ファイルの名前 ([PalTemplate](../FileTypes/PalTemplate.md) を参照)。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **構文:**
        以下のいずれかの作品：

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **説明:** あなたに対して相対的または絶対的に Pal を生成します。 **RCON では x、y、z を指定する必要があります!**

        **注意:** レベルを除くすべてのステータスはランダム化されます。

        **引数:**
        - `<PalID>`: 生成する Pal。
        - `[x]`: (オプション) 仲間の x 位置。デフォルト: プレイヤーの呼び出し元を基準にします。
        - `[y]`: (オプション) 仲間の y 位置。デフォルト: プレイヤーの呼び出し元を基準にします。
        - `[z]`: (オプション) 仲間の z 位置。デフォルト: プレイヤーの呼び出し元を基準にします。
        - `[Level]`: (オプション) Pal のレベル。デフォルト: 1。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /spawnpal Anubis 255
        ```
        _レベル 255 のアヌビスをスポーンします!_

    ??? info "/spawnpal_ex"
        **構文:** `/spawnpal` と同じ。

        **説明:** `/spawnpal` と同じ方法で Pal をスポーンし、さらにダメージ計測を有効にします。Pal が死亡または捕獲されると、PalDefender は完全なダメージランキングをログへ記録します。`PalWebhooks.webhookURL_Summons` が設定されている場合は、同じランキングを Webhook にも送信します。`announceAdminSummonsKill` が有効な場合、戦闘に参加したオンラインプレイヤーには、上位 5 名と自分の順位を示す結果ダイアログも表示されます。最も多くダメージを与えたプレイヤーが勝者として表示されます。このコマンドは PalTemplate／PalSummon ファイルを使用せず、報酬も付与しません。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /spawnpal_ex Anubis 230 -486 4097 80
        ```

    ??? info "/spawnnpc"
        **構文:** `/spawnnpc <NPCID|CharacterID> [Level=1]` または `/spawnnpc <NPCID|CharacterID> <X> <Y> [Z] [Level=1]`

        **説明:** AI を使用して NPC を生成します。チャットでは、省略された座標が管理者の近くに出現します。 RCON は座標を指定する必要があります。 `X` と `Y` のみを使用して、PalDefender は床の高さを求めます。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /spawnnpc PIDF_Soldier_AssaultRifle 30
        ```

    ??? info "/spawnpal_j"
        **構文:**

        以下のいずれかの作品：

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal_j <PalTemplate> [x] [y] [z]`

        **説明:** あなたに対して相対的または絶対的に Pal を生成します。 **RCON では x、y、z を指定する必要があります!**

        **注意:** レベルを除くすべてのステータスはランダム化されます。

        **引数:**

        - `<PalTemplate>`: 使用する PalTemplate ファイルの名前。
        - `[x]`: (オプション) 仲間の x 位置。デフォルト: プレイヤーの呼び出し元を基準にします。
        - `[y]`: (オプション) 仲間の y 位置。デフォルト: プレイヤーの呼び出し元を基準にします。
        - `[z]`: (オプション) 仲間の z 位置。デフォルト: プレイヤーの呼び出し元を基準にします。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /spawnpal_j ArenaBoss 230 -486 4097
        ```

    ??? info "/spawnpal_ex_j"
        **構文:** `/spawnpal_ex_j <PalTemplate> [x] [y] [z]`

        **説明:** `/spawnpal_j` と同じ PalTemplate および座標処理を使用し、さらにダメージ計測を有効にします。Pal が死亡または捕獲されると、PalDefender は完全なダメージランキングをログへ記録します。`PalWebhooks.webhookURL_Summons` が設定されている場合は、同じランキングを Webhook にも送信します。`announceAdminSummonsKill` が有効な場合、戦闘に参加したオンラインプレイヤーには、上位 5 名と自分の順位を示す結果ダイアログも表示されます。最も多くダメージを与えたプレイヤーが勝者として表示されます。このコマンドでは PalSummon の報酬は使用されません。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /spawnpal_ex_j ArenaBoss 230 -486 4097
        ```

    ??? info "/summon"
        **構文:** `/summon <PalSummon>`

        **説明:** 提供された PalSummon ファイルを使用して Pal を生成します。

        **注意:** ファイル名に .json 拡張子を含める必要はありません。見つからない場合は、システムが自動的に追加します。

        **引数:**
        - `<PalSummon>`: 使用する PalSummon ファイルの名前。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **構文:** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **説明:** ターゲット ユーザーに、特定の仲間が内部に含まれ、オプションでレベルが調整された仲間の卵を与えます。

        **引数:**

        ??? quote "<UserId\>"
            **説明:** 卵を受け取るプレイヤーの ID。

        ??? quote "<EggId\>"
            **説明:** 与える卵の種類。

            **注:** 各タイプの許容値は 01 (最小) から 05 (最大) です。

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **説明:** 卵の中に入る Pal。

            **注:** Pal ID (例: `WeaselDragon` (Chillet)) を使用します。完全なリストは [paldeck.cc/pals](https://paldeck.cc/pals) でご覧ください。

        ??? quote "[レベル\]"
            **説明:** (オプション) 卵内の Pal のレベル。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? info "/givemeegg"
        **構文:** `/givemeegg <EggId> <PalId> [Level]`

        **説明:** 特定の仲間が入った仲間の卵を自分に与え、オプションでレベルを調整できます。

        **引数:**

        ??? quote "<EggId\>"
            **説明:** 自分自身に与える卵のタイプ。

            **注:** 各タイプの許容値は 01 (最小) から 05 (最大) です。

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **説明:** 卵の中に入る Pal。

            **注:** Pal ID (例: `WeaselDragon` (Chillet)) を使用します。完全なリストは [paldeck.cc/pals](https://paldeck.cc/pals) でご覧ください。

        ??? quote "[レベル]"
            **説明:** (オプション) 卵内の Pal のレベル。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? info "/giveegg_j"
        **構文:** `/giveegg_j <EggId> <PalTemplate> [Level]`

        **説明:** PalTemplate ファイルによって定義された Pal と、オプションで調整されたレベルを持つ仲間の卵を与えます。

        **引数:**

        ??? quote "<EggId\>"
            **説明:** 与える卵の種類。

            **注:** 各タイプの許容値は 01 (最小) から 05 (最大) です。

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **説明:** 使用する PalTemplate ファイルの名前。

            **注意:** ファイル名に .json 拡張子を含める必要はありません。見つからない場合は、システムが自動的に追加します。 [PalTemplate](../FileTypes/PalTemplate.md) を参照してください。

        ??? quote "[レベル]"
            **説明:** (オプション) 卵内の Pal のレベル。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **構文:** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **説明:** PalTemplate ファイルによって定義された Pal と、オプションで調整されたレベルを持つ仲間の卵を自分に与えます。

        **引数:**

        ??? quote "<EggI\>"
            **説明:** 自分自身に与える卵のタイプ。

            **注:** 各タイプの許容値は 01 (最小) から 05 (最大) です。

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **説明:** 使用する PalTemplate ファイルの名前。

            **注意:** ファイル名に .json 拡張子を含める必要はありません。見つからない場合は、システムが自動的に追加します。 [PalTemplate](../FileTypes/PalTemplate.md) を参照してください。

        ??? quote "[レベル]"
            **説明:** (オプション) 卵内の Pal のレベル。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **構文:** `/jetragon`

        **説明:** Admin-Jetragon Pal を提供します (faaas.... なくなってしまいました)。

        **引数:**
        - なし

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **構文:** `/catwaifu`

        **説明:** キャラクターの統計を強化する管理者猫ワイフを与えます。

        **引数:**

        - なし

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **構文:** `/exportpals [UserId]`

        **説明:** プレーヤーのすべての Pal を、Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/ にある PalTemplate ファイルにエクスポートします。

        **引数:**

        - `[UserId]`: (オプション) Pals がエクスポートされるプレーヤーの ID。省略した場合は、独自の Pals をエクスポートします。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **構文:** `/deletepals <UserId> <PalFilter>`

        **説明:** 高度なフィルターを使用して、指定されたユーザーから Pals を削除します。フィルターを使用すると、1 つのコマンドで複数の基準 (Pal ID、レベル、性別、パッシブなど) を指定できます。重要なデータに使用する前に、安全な環境でテストしてください。

        **引数:**

        ??? quote "<UserId\>"
            **説明:** Pals が削除されるプレーヤーの ID。

        ??? quote "<PalFilter\>"
            **説明:** 削除する Pals を選択するためのフィルター キーワードのセット。

            **注意:** 複数のキーワードを 1 つのコマンドに組み合わせることができます。

            利用可能なフィルターキーワード:

            - `ID`: PalID または PalID のリスト (カンマ区切り)
            - `Nick`: 文字列 (Pal の名前)
            - `Gender`: `male` または `female`
            - `Level`: 数値。シンボル `<`、`>`、`<=`、`>=`、`=`、`!=` をサポートします。
            - `Rank`: 数値。シンボル `<`、`>`、`<=`、`>=`、`=`、`!=` をサポートします。
            - `Lucky`: `true` または `false` (光沢あり)
            - `Passives`: パッシブスキルまたはパッシブスキルのリスト (カンマ区切り)
            - `Limit`: 数値 (削除する Pals の最大数)

            **フィルターの例:**

            - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

            上記のフィルター キーと例は、現在の PalFilter リファレンスです。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "リサーチツリー"
    ??? info "/learntech"
        **構文:** `/learntech <UserId> <TechID>`

        **説明:** プレイヤーが特定のテクノロジーを学習できるようにします。すべてのロックを解除するには、`all` を使用してください。

        **引数:**

        - `<UserId>`: プレーヤーの ID。
        - `<TechID>`: 学ぶべきテクノロジー。すべてのロックを解除するには、`all` を使用してください。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /learntech steam_76500000000000000 Tech001
        /learntech gdk_25300000000000000 all
        ```

    ??? info "/unlearntech"
        **構文:** `/unlearntech <UserId> <TechID>`

        **説明:** プレイヤーに特定のテクノロジーを忘れさせます。すべてを削除するには、`all` を使用します。

        **引数:**

        - `<UserId>`: プレーヤーの ID。
        - `<TechID>`: 忘れるべきテクノロジー。すべてを削除するには、`all` を使用します。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /unlearntech gdk_25300000000000000 Tech001
        /unlearntech steam_76500000000000000 all
        ```

    ??? info "/givetechpoints"
        **構文:** `/givetechpoints <UserId> [Amount=1]`

        **説明:** 対象ユーザーに X テクノロジー ポイントを付与します。

        **引数:**

        - `<UserId>`: テクノロジー ポイントを受け取るプレイヤーの ID。
        - `[Amount]`: (オプション) 与えるテクノロジー ポイントの数。デフォルト: 1。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /givetechpoints steam_76500000000000000 10
        ```

    ??? info "/givebosstechpoints"
        **構文:** `/givebosstechpoints <UserId> [Amount=1]`

        **説明:** 対象ユーザーに X 古代技術ポイントを与えます。

        **引数:**

        - `<UserId>`: 古代技術ポイントを受け取るプレイヤーのID。
        - `[Amount]`: (オプション) 与える古代技術ポイントの数。デフォルト: 1。

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /givebosstechpoints steam_76500000000000000 5
        ```

    ??? info "/givemetechpoints"
        **構文:** `/givemetechpoints [Amount=1]`

        **説明:** 自分自身に X テクノロジー ポイントを与えます。

        **引数:**

        - `[Amount]`: (オプション) 自分に与えるテクノロジー ポイントの数。デフォルト: 1。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /givemetechpoints 10
        ```

    ??? info "/givemebosstechpoints"
        **構文:** `/givemebosstechpoints [Amount=1]`

        **説明:** 自分自身に X 古代技術ポイントを与えます。

        **引数:**

        - `[Amount]`: (オプション) 自分に与える古代技術ポイントの数。デフォルト: 1。

        **権限:** `Chat`、`Admin`

        **例:**
        ```
        /givemebosstechpoints 5
        ```


??? note "データマイニング"
    ??? info "/gettechids"
        **構文:** `/gettechids`

        **説明:** 使用可能なすべてのテクノロジー ID のリストを返します。 RCON は JSON 出力を取得します。

        **引数:**

        - なし

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **構文:** `/getskinids`

        **説明:** 使用可能なすべての Pal スキン ID のリストを返します。 RCON は JSON 出力を取得します。

        **引数:**

        - なし

        **権限:** `Chat`、`RCON`、`Admin`

        **例:**
        ```
        /getskinids
        ```
