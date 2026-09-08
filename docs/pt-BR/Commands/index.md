# Comandos

## O que são comandos?

Comandos são instruções especiais baseadas em texto que permitem interagir com o jogo. Ao digitar comandos no chat, você pode realizar ações como teletransportar, gerar criaturas ou gerenciar jogadores. Os comandos geralmente começam com <span class="var-command">/</span> seguido pelo nome do comando e argumentos opcionais.

## Quem pode usar comandos?

**Atualmente não há nenhum comando que um jogador não administrador possa usar.**
Na versão atual existem apenas os comandos Admin e RCON disponíveis.

## Lista de Comandos

!!! note "Sintaxe de comando"
    <span class="var-command">/command_name&nbsp;</span><span class="var-command-arg">&lt;required_argument&gt;&nbsp;</span><span class="var-command-optional">[optional_argument={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg">&lt;required_argument&gt;</span> → Deve ser incluído.<br>
    <span class="var-command-optional">[optional_argument={?}]</span> → Pode ser omitido. O <span class="var-command-optional">{?}</span> indica o valor padrão que está sendo usado quando omitido.
    </p>
    <p>
    Os argumentos têm tipos diferentes. Os mais comuns são <span class="var-string">strings</span>, <span class="var-number">numbers</span>, <span class="var-float">floats</span> e <span class="var-bool">booleans</span>. Alguns comandos possuem até tipos complexos, como <span class="file">filenames</span> específico em um diretório especial ou, na verdade, um <span class="var-filter">filter</span>.
    </p>

!!! tip "Pesquisa de ID"
    Use [paldeck.cc/pals](https://paldeck.cc/pals) para `PalID`, [paldeck.cc/items](https://paldeck.cc/items) para `ItemID`, [paldeck.cc/technology](https://paldeck.cc/technology) para `TechID`, [paldeck.cc/buildings](https://paldeck.cc/buildings) para `BuildingID`, [paldeck.cc/passives](https://paldeck.cc/passives) para `PassiveID` e [paldeck.cc/skills](https://paldeck.cc/skills) para IDs de habilidade.

??? note "Somente RCON"
    ??? info "/getrconcmds"
        **Sintaxe:** `/getrconcmds`

        **Descrição:** Retorna uma lista de cada comando com a contagem de argumentos necessária que pode ser usada por RCON.

        **Argumentos:**

        - Nenhum

        **Permissões:** `RCON`

        **Exemplo:**
        ```
        /getrconcmds
        ```

??? note "Gerenciamento de Servidor"
    ??? info "/version"
        **Sintaxe:** `/version`

        **Descrição:** mostra a versão do jogo Palworld e a versão PalDefender. RCON retorna a saída JSON.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /version
        ```

    ??? info "/reloadcfg"
        **Sintaxe:** `/reloadcfg`

        **Descrição:** recarrega dados de banimento de `Config.json`, `WhiteList.json` e PalDefender.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /reloadcfg
        ```

    ??? info "/addadminip"
        **Sintaxe:** `/addadminip <IP>`

        **Descrição:** Adiciona um endereço IP à lista de permissões do administrador.

        **Argumentos:**

        - `<IP>`: O endereço IP a ser adicionado como administrador.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /addadminip 192.168.1.1
        ```

    ??? info "/setadmin"
        **Sintaxe:** `/setadmin <UserId>`

        **Descrição:** grants/revokes administrador temporário de um jogador.

        **Argumentos:**

        - `<UserId>`: o ID do jogador para o administrador do grant/revoke.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /setadmin steam_76500000000000000
        ```

    ??? info "/pgbroadcast"
        **Sintaxe:** `/pgbroadcast <Message>`

        **Descrição:** Envie uma mensagem para todos os jogadores no servidor.

        **Argumentos:**

        - `<Message>`: a mensagem a ser transmitida.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /pgbroadcast "Server will restart soon."
        ```

    ??? info "/adminlogin"
        **Sintaxe:** `/adminlogin <password>`

        **Descrição:** Faz login no modo administrador. Requer sua senha de administrador como argumento.

        **Argumentos:**

        - `<password>`: A senha do administrador.

        **Permissões:** `Chat`

        **Exemplo:**
        ```
        /adminlogin mySecretPassword
        ```

    ??? info "/adminlogout"
        **Sintaxe:** `/adminlogout`

        **Descrição:** Desconecta você do modo de administrador.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /adminlogout
        ```

    ??? info "/iwantplayerlist"
        **Sintaxe:** `/iwantplayerlist`

        **Descrição:** Ativa a sobreposição da lista de jogadores no jogo, permitindo que você visualize o UserId e o UID do jogador de cada jogador ao pressionar ESC. Útil para administradores de servidores e jogadores que desejam ver informações detalhadas dos jogadores diretamente na interface do jogo.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /iwantplayerlist
        ```

    ??? info "/getpos"
        **Sintaxe:** `/getpos [UserId]`

        **Descrição:** Obtém sua posição atual no mundo, que pode ser usada para teletransporte, invocação e ações semelhantes. Se um [UserId] for fornecido, obtém a posição desse jogador.

        **Argumentos:**

        - `[UserId]`: (Opcional) O ID do jogador cuja posição você deseja get. Se omitido, obtém sua própria posição.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /getpos
        /getpos steam_76500000000000000
        ```

    ??? info "/settime"
        **Sintaxe:** `/settime <hour>`

        **Descrição:** Altera a hora em Palworld. A hora pode ter os seguintes valores: `0` a `23`, `day` e `night`.

        **Argumentos:**

        - `<hour>`: Valor da hora (0-23, dia, noite).

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /settime 12
        /settime night
        ```

    ??? info "/togglepvp"
        **Sintaxe:** `/togglepvp`

        **Descrição:** ativa ou desativa o servidor PvP para a sessão atual em execução.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /togglepvp
        ```

    ??? info "/alert"
        **Sintaxe:** `/alert <message>`

        **Descrição:** Envia uma mensagem de alerta para todos os jogadores no servidor. Esta mensagem geralmente é exibida com destaque em suas telas.

        **Argumentos:**

        - `<message>`: a mensagem a ser transmitida como alerta.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /alert Server will restart in 5 minutes!
        ```

    ??? info "/send"
        **Sintaxe:** `/send <type> <UserId> <Message>`

        **Descrição:** Permite enviar uma mensagem ou mensagem de registro para um jogador específico.

        **Argumentos:**

        - `<type>`: o tipo de mensagem a ser enviada. Valores possíveis:
             - `msg`: mensagem de bate-papo normal.
             - `log`: Mensagem de log normal (branca, desaparece rapidamente, fonte maior).
             - `ilog`: Mensagem de log importante (azul, permanece por mais tempo).
             - `vilog`: Mensagem de log muito importante (azul, permanece extremamente longa).
        - `<UserId>`: O ID do jogador que receberá a mensagem.
        - `<Message>`: O texto da mensagem a ser enviada.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /send msg steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send log steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send ilog steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send vilog steam_76500000000000000 Dont miss out on Qonzer's sale!
        ```

    ??? info "/resetoilrig"
        **Sintaxe:** `/resetoilrig <lv30|lv55|lv60|all>`

        **Descrição:** Redefine a plataforma petrolífera selecionada ou todas as plataformas petrolíferas atualmente gerenciadas.

        **Permissões:** `Chat`, status de administrador ativo no jogo.

        **Exemplo:**
        ```
        /resetoilrig all
        ```

    ??? info "/setting"
        **Sintaxe:** `/setting list [filter]` ou `/setting <setting_name> <get|set|add|sub> [value]`

        **Descrição:** inspeciona ou altera valores `UPalGameSetting` ativos suportados. Os nomes são correspondidos sem distinção entre maiúsculas e minúsculas; um prefixo ou substring exclusivo é aceito. Isso é experimental, não substitui a configuração mundial persistente e os clientes podem continuar a exibir valores armazenados em cache.

        - `list [filter]`: lista os campos integer, float, booleanos, bytes e enum suportados.
        - `get`: Lê um valor.
        - `set`: Define qualquer tipo compatível. Booleanos aceitam `true/false`, `on/off`, `yes/no` ou `1/0`; enums aceitam um número ou nome de entrada.
        - `add` / `sub`: altera apenas valores numéricos.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplos:**
        ```
        /setting list death
        /setting PalDeathPenaltyTime get
        /setting PalDeathPenaltyTime set 10
        ```

    ??? info "/resetbosstower"
        **Sintaxe:** `/resetbosstower <BossType|all>`

        **Descrição:** Comando somente de compilação de depuração que redefine uma instância da torre de chefe ou todas as torres de chefe reconfiguráveis. Um único destino deve usar um nome `EPalBossType` válido. Não está disponível em compilações de lançamento público.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /resetbosstower all
        ```

    ??? info "/showbosses"
        **Sintaxe:** `/showbosses`

        **Descrição:** Comando de mineração de dados somente para compilação de depuração que grava informações estáticas do chefe atual em `PalDefender/Logs/BossInfo.json`. Não está disponível em compilações de lançamento público.

        **Permissões:** `Chat`, `RCON`, `Admin`

??? note "Gerenciamento Básico"
    ??? info "/findunusedbases (alias: /findbases)"
        **Sintaxe:** `/findbases [empty|inactive|unused|all] [days=N] [builds<=N]`

        **Sintaxe interativa:** `/findbases visit [filters]`, `/findbases next`, `/findbases kill [next]`

        **Descrição:** Verifica bases vazias, inativas ou não utilizadas. `visit` cria uma fila de revisão somente de bate-papo e se teletransporta para seu primeiro resultado; `next` avança; `kill` destrói a base selecionada; `kill next` destrói e avança. A destruição é irreversível, então inspecione cada alvo primeiro.

        - `empty`: Nenhum trabalhador e no máximo o limite de construção padrão (ou `builds<=N`).
        - `inactive`: Nenhum membro da guilda online e inativo por pelo menos `days` (padrão `30`).
        - `unused`: Corresponde a vazio ou inativo.
        - `all`: Lista todas as bases enquanto ainda aplica filtros explícitos.

        **Permissões:** a listagem suporta `Chat` e `RCON`; visit/next/kill requer bate-papo no jogo e permissão de administrador.

        **Exemplos:**
        ```
        /findbases empty builds<=5
        /findbases inactive days=14
        /findbases visit unused days=30
        /findbases kill next
        ```

    ??? info "/getnearestbase"
        **Sintaxe:** `/getnearestbase [X] [Y] [Z]`

        **Descrição:** Informa o nome da guilda que possui a base mais próxima do seu personagem.

        **Observação:** Quando executado via **RCON**, todos os parâmetros de localização (`[X]` `[Y]` `[Z]`) **são obrigatórios**, já que RCON não tem personagem de jogador para determinar a localização.

        **Argumentos:**

        - `[X]`: (Opcional) coordenada X.
        - `[Y]`: (Opcional) coordenada Y.
        - `[Z]`: (Opcional) coordenada Z.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /getnearestbase 100 200 50
        ```

    ??? info "/gotonearestbase"
        **Sintaxe:** `/gotonearestbase [X] [Y] [Z]`

        **Descrição:** Teleporta você para a base mais próxima do local.

        **Observação:** Quando executado via **RCON**, todos os parâmetros de localização (`[X]` `[Y]` `[Z]`) **são obrigatórios**, já que RCON não tem personagem de jogador para determinar a localização.

        **Argumentos:**

        - `[X]`: (Opcional) coordenada X.
        - `[Y]`: (Opcional) coordenada Y.
        - `[Z]`: (Opcional) coordenada Z.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /gotonearestbase 100 200 50
        ```

    ??? info "/killnearestbase"
        **Sintaxe:** `/killnearestbase [X] [Y] [Z]`

        **Descrição:** Destrói a base mais próxima (**Use com cuidado!**).

        **Observação:** Quando executado via **RCON**, todos os parâmetros de localização (`[X]` `[Y]` `[Z]`) **são obrigatórios**, já que RCON não tem personagem de jogador para determinar a localização.

        **Argumentos:**

        - `[X]`: (Opcional) coordenada X.
        - `[Y]`: (Opcional) coordenada Y.
        - `[Z]`: (Opcional) coordenada Z.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /killnearestbase 100 200 50
        ```


??? note "Gerenciamento de jogadores"
    ??? info "/kick"
        **Sintaxe:** `/kick <UserId> [Reason="Kicked by Admin."]`

        **Descrição:** Expulsa um jogador do servidor.

        **Argumentos:**

        - `<UserId>`: O ID do jogador a ser chutado.
        - `[Reason]`: (Opcional) Motivo do chute. Padrão: "Expulso pelo administrador".

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /kick steam_76500000000000000 "Spamming in chat"
        ```

    ??? info "/ban"
        **Sintaxe:** `/ban <UserId> [Reason="Banned by Admin."]`

        **Descrição:** Bane e expulsa um jogador do servidor.

        **Argumentos:**

        - `<UserId>`: O ID do jogador a ser banido.
        - `[Reason]`: (Opcional) Motivo do banimento. Padrão: "Banido pelo administrador".

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /ban gdk_25300000000000000 "Cheating"
        ```

    ??? info "/ipban"
        **Sintaxe:** `/ipban <UserId> [Reason="Banned by Admin."]`

        **Descrição:** Bane o endereço IP de um jogador e depois o expulsa do servidor.

        **Argumentos:**

        - `<UserId>`: O ID do jogador cujo IP será banido.
        - `[Reason]`: (Opcional) Motivo do banimento. Padrão: "Banido pelo administrador".

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /ipban steam_76500000000000000
        ```

    ??? info "/banip"
        **Sintaxe:** `/banip <IP>`

        **Descrição:** Bane um endereço IP do servidor.

        **Argumentos:**

        - `<IP>`: O endereço IP a ser banido.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /banip 192.168.1.1
        ```

    ??? info "/unbanip"
        **Sintaxe:** `/unbanip <IP>`

        **Descrição:** Remove um endereço IP da lista de banimentos.

        **Argumentos:**

        - `<IP>`: O endereço IP para cancelar o banimento.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /unbanip 192.168.1.1
        ```

    ??? info "/unban"
        **Sintaxe:** `/unban <UserId> [Reason="Unbanned by admin."]`

        **Descrição:** remove um UserId da lista de banimentos PalDefender.

        **Argumentos:**

        - `<UserId>`: O UserId para cancelar o banimento.
        - `[Reason]`: (Opcional) Motivo armazenado para a ação de cancelamento de banimento.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /unban steam_76500000000000000 "Appeal accepted"
        ```

    ??? info "/getip"
        **Sintaxe:** `/getip <UserId>`

        **Descrição:** Mostra o endereço IP de um jogador.

        **Argumentos:**

        - `<UserId>`: O ID do jogador.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /getip gdk_25300000000000000
        ```

    ??? info "/whitelist_add"
        **Sintaxe:** `/whitelist_add <UserId>`

        **Descrição:** Adiciona um UserId à lista de permissões.

        **Argumentos:**

        - `<UserId>`: O ID do jogador a ser colocado na lista de permissões.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /whitelist_add steam_76500000000000000
        ```

    ??? info "/whitelist_remove"
        **Sintaxe:** `/whitelist_remove <UserId>`

        **Descrição:** Remove um UserId da lista de permissões.

        **Argumentos:**

        - `<UserId>`: O ID do jogador a ser removido da lista de permissões.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /whitelist_remove gdk_25300000000000000
        ```

    ??? info "/whitelist_get"
        **Sintaxe:** `/whitelist_get`

        **Descrição:** Mostra a lista completa dos jogadores na lista de permissões.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /whitelist_get
        ```

    ??? info "/imcheater"
        **Sintaxe:** `/imcheater`

        **Descrição:** Use isto para testar como seu servidor responde a um trapaceiro.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /imcheater
        ```

    ??? info "/spectate"
        **Sintaxe:** `/spectate`

        **Descrição:** Ativa o modo espectador. O mesmo que pressionar a tecla de atalho `\`, mas a tecla de atalho não funciona para todos, como jogadores de console.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /spectate
        ```

??? note "Personagem do jogador"
    ??? info "/tp"
        **Sintaxe:**
        Qualquer um dos seguintes trabalhos:

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

        **Descrição:** Teletransporta você mesmo, ou um jogador específico, para outro jogador, coordenadas, a base própria mais próxima ou um destino de plataforma petrolífera.

        **Observação:** RCON deve incluir o jogador que está sendo teletransportado porque RCON não tem personagem no jogo.

        **Argumentos:**

        - `<UserId>`: Um jogador para o qual se teletransportar ou o jogador sendo teletransportado quando mais argumentos são fornecidos.
        - `<UserId1>`: O jogador a ser teletransportado.
        - `<UserId2>`: O jogador alvo.
        - `<X> <Y> [Z]`: Coordenadas do mapa. Se `Z` for omitido, PalDefender tentará encontrar uma altura de solo utilizável.
        - `home`: Teletransporta-se para a base de propriedade mais próxima.
        - `oilrig`, `oilrig:Lv30`, `oilrig:Lv55`, `oilrig:Lv60`: Teletransporta-se para um destino de plataforma petrolífera.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /tp steam_76500000000000000 gdk_25300000000000000
        /tp 100 -250
        /tp oilrig:Lv60
        ```

    ??? info "/give_exp"
        **Sintaxe:** `/give_exp <UserId> <Amount>`

        **Descrição:** Dá pontos de experiência a um jogador.

        **Argumentos:**

        - `<UserId>`: O ID do jogador.
        - `<Amount>`: Quantidade de pontos de experiência.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /give_exp gdk_25300000000000000 1000
        ```

    ??? info "/giveme_exp"
        **Sintaxe:** `/giveme_exp <Amount>`

        **Descrição:** Dá pontos de experiência para você mesmo.

        **Argumentos:**

        - `<Amount>`: Quantidade de pontos de experiência.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /giveme_exp 1000
        ```

    ??? info "/renameplayer"
        **Sintaxe:** `/renameplayer <UserId> <NewName>`

        **Descrição:** Renomeia o apelido de um jogador.

        **Argumentos:**

        - `<UserId>`: O ID do jogador.
        - `<NewName>`: O novo apelido.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /renameplayer steam_76500000000000000 NewNickname
        ```

    ??? info "/givestats"
        **Sintaxe:** `/givestats <UserId> [Count=1]`

        **Descrição:** Dá ao jogador um ou mais Pontos de Status Não Utilizados (o valor negativo será subtraído). Não afeta os pontos já gastos.

        **Argumentos:**

        - `<UserId>`: O ID do jogador que receberá os pontos de status.
        - `[Count]`: (Opcional) O número de pontos de status não utilizados a serem fornecidos (pode ser negativo para subtrair). Padrão: 1.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /givestats steam_76500000000000000 5
        /givestats steam_76500000000000000 -2
        ```

    ??? info "/givemestats"
        **Sintaxe:** `/givemestats [Count=1]`

        **Descrição:** Dá a si mesmo um ou mais Pontos de Status Não Utilizados (o valor negativo será subtraído). Não afeta os pontos já gastos.

        **Argumentos:**

        - `[Count]`: (Opcional) O número de pontos de status não utilizados para fornecer a si mesmo (pode ser negativo para subtrair). Padrão: 1.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /givemestats 5
        /givemestats -2
        ```

    ??? info "/godmode"
        **Sintaxe:** `/godmode [on/off]`

        **Descrição:** Concede invulnerabilidade, incluindo imunidade a efeitos de status, nega o consumo de alimentos e restaura a saúde após a ativação. Opcionalmente, permite fazer tudo de uma só vez, se habilitado na configuração.

        **Argumentos:**

        - `[on/off]`: (Opcional) Para ativar ou desativar explicitamente o godmode. Padrão: ativa e desativa.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /godmode
        /godmode on
        /godmode off
        ```

    ??? info "/admingun (alias: /agun)"
        **Sintaxe:** `/admingun`

        **Descrição:** Dá ao administrador ativo no jogo uma Admin Gun protegida. Ela mata personagens instantaneamente, destrói objetos do mapa, maximiza o dano à folhagem, tem munição e durabilidade ilimitadas e não pode ser descartada, vendida ou movida para contêineres externos. Agache-se ao destruir um objeto de armazenamento para excluir seu conteúdo; permaneça de pé para preservá-lo. A arma é removida após a morte, ao sair do servidor ou ao perder o status de administrador, e solicitar outra substitui a cópia existente.

        **Permissões:** `Chat`, status de administrador ativo no jogo. `allowAdminCheats` não é obrigatório.

        **Exemplo:**
        ```
        /agun
        ```

??? note "Gerenciamento de Guilda"
    ??? info "/setguildleader"
        **Sintaxe:** `/setguildleader <UserId>`

        **Descrição:** Torna o jogador alvo o líder de sua guilda atual.

        **Argumentos:**

        - `<UserId>`: O ID do jogador que se tornará líder da guilda.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **Sintaxe:** `/exportguilds`

        **Descrição:** Coloca todas as guildas do servidor em Pal/Binaries/Win64/PalDefender/guildexport.json.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /exportguilds
        ```
        Arquivo de saída de exemplo: `Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "Itens"
    ??? info "/give"
        **Sintaxe:** `/give <UserId> <ItemId> [Amount=1]`

        **Descrição:** Dá ao jogador um item e, se especificado, quantos.

        **Argumentos:**

        - `<UserId>`: O ID do jogador ao qual fornecer o item.
        - `<ItemId>`: O item a ser fornecido.
        - `[Amount]`: (Opcional) Quantos. Padrão: 1.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /give steam_76500000000000000 Sword 2
        ```

    ??? info "/giveitems"
        **Sintaxe:** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

        **Descrição:** Dá ao jogador mais de 1 item em um comando e, se especificado, quantos de cada um são separados por dois pontos.

        **Argumentos:**

        - `<UserId>`: O ID do jogador para quem os itens serão entregues.
        - `<ItemId>[:<Amount>] ...`: Lista de itens e valores opcionais.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /giveitems gdk_25300000000000000 Sword:2 Shield:1
        ```

    ??? info "/giveme"
        **Sintaxe:** `/giveme <ItemId> [Amount=1]`

        **Descrição:** Dá a si mesmo um item e, se especificado, quantos.

        **Argumentos:**

        - `<ItemId>`: O item que você deve dar a si mesmo.
        - `[Amount]`: (Opcional) Quantos. Padrão: 1.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /giveme Sword 3
        ```

    ??? info "/delitem"
        **Sintaxe:** `/delitem <UserId> <ItemId> [Amount=1]`

        **Descrição:** Exclui de um jogador a quantidade especificada de um item. O padrão é `1`, que exclui apenas uma ocorrência. Use `all` em vez de `1` para excluir todas as ocorrências.

        **Argumentos:**

        - `<UserId>`: O ID do jogador.
        - `<ItemId>`: O item a ser excluído.
        - `[Amount]`: (Opcional) Quantidade. Padrão: 1. Use `all` para excluir todas as ocorrências.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /delitem steam_76500000000000000 Sword 1
        /delitem gdk_25300000000000000 Sword all
        ```

    ??? info "/give_relic"
        **Sintaxe:** `/give_relic <UserId> <RelicType> [Amount]`

        **Descrição:** Dá ao jogador um ou mais pontos de relíquia do tipo selecionado.

        **Argumentos:**

        - `<UserId>`: O ID do jogador que receberá os pontos de relíquia.
        - `<RelicType>`: O tipo de relíquia a ser concedida.

        - `[Amount]`: Número opcional de pontos de relíquia para dar. O padrão é `1`.

        **Tipos de relíquias compatíveis:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /give_relic steam_76500000000000000 CapturePower 5
        ```

    ??? info "/giveme_relic"
        **Sintaxe:** `/giveme_relic <RelicType> [Amount]`

        **Descrição:** Dá a si mesmo um ou mais pontos de relíquia do tipo selecionado.

        **Argumentos:**

        - `<RelicType>`: O tipo de relíquia a ser concedida.

        - `[Amount]`: Número opcional de pontos de relíquia para você conceder. O padrão é `1`.

        **Tipos de relíquias compatíveis:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /giveme_relic CapturePower 5
        ```


    ??? info "/delitems"
        **Sintaxe:** `/delitems <UserId> <ItemId>[:<Amount>] ...`

        **Descrição:** Exclui mais de um item de um jogador em um único comando; a quantidade opcional de cada item é separada por dois-pontos. Use `all` em vez de `1` para excluir todas as ocorrências.

        **Argumentos:**

        - `<UserId>`: O ID do jogador.
        - `<ItemId>[:<Amount>] ...`: Lista de itens e valores opcionais.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /delitems steam_76500000000000000 Sword:1 Shield:all
        ```

    ??? info "/clearinv"
        **Sintaxe:** `/clearinv <UserId> [Container=items] ...`

        **Descrição:** Limpa contêineres específicos do inventário de um jogador. Contêineres disponíveis: `items`, `keyitems`, `armor`, `weapons`, `food`, `dropslot` ou `all`.

        **Argumentos:**

        - `<UserId>`: O ID do jogador.
        - `[Container] ...`: (Opcional) Contêineres a serem limpos. Padrão: itens.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /clearinv steam_76500000000000000 items
        /clearinv gdk_25300000000000000 all
        ```


??? note "Pals"
    ??? info "/givepal"
        **Sintaxe:** `/givepal <UserId> <PalId> [Level=1]`

        **Descrição:** Dá um Pal a um jogador no nível especificado.

        **Argumentos:**

        - `<UserId>`: O ID do jogador.
        - `<PalId>`: O Pal para dar.
            - **Observação:** Use o Pal ID, por exemplo, `WeaselDragon` (Cillet). Veja a lista completa em [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Opcional) Nível do Pal. Padrão: 1.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **Sintaxe:** `/givepal_j <UserID> <PalTemplate>`

        **Descrição:** Dá ao jogador um Pal definido por um arquivo PalTemplate. JSON incorporado não é mais compatível; apenas um nome de arquivo é aceito.

        **Observação:** Você não precisa incluir a extensão .json no nome do arquivo; o sistema irá anexá-lo automaticamente se estiver faltando.

        **Argumentos:**

        - `<UserID>`: O ID do jogador.
        - `<PalTemplate>`: O nome do arquivo PalTemplate (consulte [PalTemplate](../FileTypes/PalTemplate.md)).

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **Sintaxe:** `/givemepal <PalId> [Level=1]`

        **Descrição:** Dá a si mesmo um Pal no nível especificado.

        **Argumentos:**

        - `<PalId>`: O Pal para você se presentear.
            - **Observação:** Use o Pal ID, por exemplo, `WeaselDragon` (Cillet). Veja a lista completa em [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Opcional) Nível do Pal. Padrão: 1.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **Sintaxe:** `/givemepal_j <PalTemplate>`

        **Descrição:** Fornece um Pal definido por um arquivo PalTemplate. JSON incorporado não é mais compatível; apenas um nome de arquivo é aceito.

        **Argumentos:**

        - `<PalTemplate>`: O nome do arquivo PalTemplate (consulte [PalTemplate](../FileTypes/PalTemplate.md)).

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **Sintaxe:**
        Qualquer um dos seguintes trabalhos:

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **Descrição:** Gera um Pal relativo ou absoluto a você. **RCON deve especificar x, y e z!**

        **Observação:** Todas as estatísticas, exceto nível, são aleatórias.

        **Argumentos:**
        - `<PalID>`: O Pal a ser gerado.
        - `[x]`: (Opcional) x posição do pal. Padrão: relativo ao jogador invocador.
        - `[y]`: (Opcional) posição y do pal. Padrão: relativo ao jogador invocador.
        - `[z]`: (Opcional) posição z do pal. Padrão: relativo ao jogador invocador.
        - `[Level]`: (Opcional) Nível do Pal. Padrão: 1.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /spawnpal Anubis 255
        ```
        _Gera um Anúbis com nível 255!_

    ??? info "/spawnpal_ex"
        **Sintaxe:** Igual a `/spawnpal`.

        **Descrição:** Gera um Pal exatamente como `/spawnpal`, mas permite o rastreamento de danos. Quando o Pal morre ou é capturado, PalDefender registra a classificação completa do dano e a envia para `PalWebhooks.webhookURL_Summons` quando o webhook é configurado. Se `announceAdminSummonsKill` estiver ativado, os jogadores online participantes também receberão uma caixa de diálogo de resultados mostrando os cinco primeiros e sua própria classificação. O causador de maior dano é marcado como o vencedor. Este comando não usa um arquivo PalTemplate ou PalSummon e não concede recompensas.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /spawnpal_ex Anubis 230 -486 4097 80
        ```

    ??? info "/spawnnpc"
        **Sintaxe:** `/spawnnpc <NPCID|CharacterID> [Level=1]` ou `/spawnnpc <NPCID|CharacterID> <X> <Y> [Z] [Level=1]`

        **Descrição:** Gera um NPC com IA. No chat, as coordenadas omitidas aparecem perto do administrador; RCON deve fornecer coordenadas. Com apenas `X` e `Y`, PalDefender encontra a altura do piso.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /spawnnpc PIDF_Soldier_AssaultRifle 30
        ```

    ??? info "/spawnpal_j"
        **Sintaxe:**

        Qualquer um dos seguintes trabalhos:

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal_j <PalTemplate> [x] [y] [z]`

        **Descrição:** Gera um Pal relativo ou absoluto a você. **RCON deve especificar x, y e z!**

        **Observação:** Todas as estatísticas, exceto nível, são aleatórias.

        **Argumentos:**

        - `<PalTemplate>`: o nome do arquivo PalTemplate a ser usado.
        - `[x]`: (Opcional) x posição do pal. Padrão: relativo ao jogador invocador.
        - `[y]`: (Opcional) posição y do pal. Padrão: relativo ao jogador invocador.
        - `[z]`: (Opcional) posição z do pal. Padrão: relativo ao jogador invocador.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /spawnpal_j ArenaBoss 230 -486 4097
        ```

    ??? info "/spawnpal_ex_j"
        **Sintaxe:** `/spawnpal_ex_j <PalTemplate> [x] [y] [z]`

        **Descrição:** usa o mesmo PalTemplate e manipulação de coordenadas que `/spawnpal_j`, mas permite o rastreamento de danos. Quando o Pal morre ou é capturado, PalDefender registra a classificação completa do dano e a envia para `PalWebhooks.webhookURL_Summons` quando o webhook é configurado. Se `announceAdminSummonsKill` estiver ativado, os jogadores online participantes também receberão uma caixa de diálogo de resultados mostrando os cinco primeiros e sua própria classificação. O causador de maior dano é marcado como o vencedor. Este comando não usa recompensas PalSummon.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /spawnpal_ex_j ArenaBoss 230 -486 4097
        ```

    ??? info "/summon"
        **Sintaxe:** `/summon <PalSummon>`

        **Descrição:** Gera um Pal usando o arquivo PalSummon fornecido.

        **Observação:** Você não precisa incluir a extensão .json no nome do arquivo; o sistema irá anexá-lo automaticamente se estiver faltando.

        **Argumentos:**
        - `<PalSummon>`: o nome do arquivo PalSummon a ser usado.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **Sintaxe:** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **Descrição:** Dá ao usuário alvo um ovo de Pal com o Pal específico dentro e nível ajustado opcionalmente.

        **Argumentos:**

        ??? quote "<UserId\>"
            **Descrição:** O ID do jogador que receberá o ovo.

        ??? quote "<EggId\>"
            **Descrição:** O tipo de ovo a ser dado.

            **Observação:** Os valores permitidos vão de 01 (menor) a 05 (maior) para cada tipo:

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
            **Descrição:** O Pal que estará dentro do ovo.

            **Observação:** Use o Pal ID, por exemplo, `WeaselDragon` (Cillet). Veja a lista completa em [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Nível\]"
            **Descrição:** (Opcional) O nível do Pal dentro do ovo.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? info "/givemeegg"
        **Sintaxe:** `/givemeegg <EggId> <PalId> [Level]`

        **Descrição:** Dá a si mesmo um ovo de Pal com o Pal específico dentro e nível ajustado opcionalmente.

        **Argumentos:**

        ??? quote "<EggId\>"
            **Descrição:** O tipo de ovo que você deve oferecer.

            **Observação:** Os valores permitidos vão de 01 (menor) a 05 (maior) para cada tipo:

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
            **Descrição:** O Pal que estará dentro do ovo.

            **Observação:** Use o Pal ID, por exemplo, `WeaselDragon` (Cillet). Veja a lista completa em [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Nível]"
            **Descrição:** (Opcional) O nível do Pal dentro do ovo.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? info "/giveegg_j"
        **Sintaxe:** `/giveegg_j <EggId> <PalTemplate> [Level]`

        **Descrição:** Fornece um pal egg com um Pal definido por um arquivo PalTemplate e nível ajustado opcionalmente.

        **Argumentos:**

        ??? quote "<EggId\>"
            **Descrição:** O tipo de ovo a ser dado.

            **Observação:** Os valores permitidos vão de 01 (menor) a 05 (maior) para cada tipo:

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
            **Descrição:** O nome do arquivo PalTemplate a ser usado.

            **Observação:** Você não precisa incluir a extensão .json no nome do arquivo; o sistema irá anexá-lo automaticamente se estiver faltando. Consulte [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Nível]"
            **Descrição:** (Opcional) O nível do Pal dentro do ovo.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **Sintaxe:** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **Descrição:** Dá a si mesmo um pal egg com um Pal definido por um arquivo PalTemplate e nível opcionalmente ajustado.

        **Argumentos:**

        ??? quote "<EggI\>"
            **Descrição:** O tipo de ovo que você deve oferecer.

            **Observação:** Os valores permitidos vão de 01 (menor) a 05 (maior) para cada tipo:

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
            **Descrição:** O nome do arquivo PalTemplate a ser usado.

            **Observação:** Você não precisa incluir a extensão .json no nome do arquivo; o sistema irá anexá-lo automaticamente se estiver faltando. Consulte [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Nível]"
            **Descrição:** (Opcional) O nível do Pal dentro do ovo.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **Sintaxe:** `/jetragon`

        **Descrição:** Dá a você um Admin-Jetragon Pal (faaas.... desapareceu).

        **Argumentos:**
        - Nenhum

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **Sintaxe:** `/catwaifu`

        **Descrição:** Dá a você um Admin-Cat-Waifu que melhora as estatísticas do seu personagem.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **Sintaxe:** `/exportpals [UserId]`

        **Descrição:** Exporte todos os Pals de um jogador para um arquivo PalTemplate em Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/.

        **Argumentos:**

        - `[UserId]`: (Opcional) O ID do jogador cujos Pals serão exportados. Se omitido, exporta seus próprios Pals.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **Sintaxe:** `/deletepals <UserId> <PalFilter>`

        **Descrição:** Exclui Pals do usuário especificado usando filtros avançados. O filtro permite que você especifique vários critérios (como Pal ID, nível, gênero, passivos, etc.) em um comando. Teste em um ambiente seguro antes de usar dados importantes.

        **Argumentos:**

        ??? quote "<UserId\>"
            **Descrição:** O ID do jogador cujos Pals serão excluídos.

        ??? quote "<PalFilter\>"
            **Descrição:** Um conjunto de palavras-chave de filtro para selecionar quais Pals serão excluídos.

            **Observação:** Várias palavras-chave podem ser combinadas em um comando.

            Palavras-chave de filtro disponíveis:

            - `ID`: PalID ou lista de PalIDs (separados por vírgula)
            - `Nick`: String (nome do Pal)
            - `Gender`: `male` ou `female`
            - `Level`: Número, suporta símbolos `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Rank`: Número, suporta símbolos `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Lucky`: `true` ou `false` (brilhante)
            - `Passives`: PassiveSkill ou lista de PassiveSkills (separados por vírgula)
            - `Limit`: Número (quantidade máxima de Pals a excluir)

            **Exemplos de filtros:**

            - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

            As chaves de filtro e os exemplos acima são a referência atual do PalFilter.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "Árvore de Pesquisa"
    ??? info "/learntech"
        **Sintaxe:** `/learntech <UserId> <TechID>`

        **Descrição:** Permite que um jogador aprenda uma tecnologia específica. Use `all` para desbloquear tudo.

        **Argumentos:**

        - `<UserId>`: O ID do jogador.
        - `<TechID>`: A tecnologia para aprender. Use `all` para desbloquear tudo.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /learntech steam_76500000000000000 Tech001
        /learntech gdk_25300000000000000 all
        ```

    ??? info "/unlearntech"
        **Sintaxe:** `/unlearntech <UserId> <TechID>`

        **Descrição:** Faz o jogador esquecer uma tecnologia específica. Use `all` para remover tudo.

        **Argumentos:**

        - `<UserId>`: O ID do jogador.
        - `<TechID>`: A tecnologia para esquecer. Use `all` para remover tudo.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /unlearntech gdk_25300000000000000 Tech001
        /unlearntech steam_76500000000000000 all
        ```

    ??? info "/givetechpoints"
        **Sintaxe:** `/givetechpoints <UserId> [Amount=1]`

        **Descrição:** Dá ao usuário alvo X pontos de tecnologia.

        **Argumentos:**

        - `<UserId>`: O ID do jogador que receberá os pontos de tecnologia.
        - `[Amount]`: (Opcional) O número de pontos de tecnologia a serem dados. Padrão: 1.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /givetechpoints steam_76500000000000000 10
        ```

    ??? info "/givebosstechpoints"
        **Sintaxe:** `/givebosstechpoints <UserId> [Amount=1]`

        **Descrição:** Dá ao usuário alvo X pontos de tecnologia antiga.

        **Argumentos:**

        - `<UserId>`: O ID do jogador que receberá os pontos de tecnologia antiga.
        - `[Amount]`: (Opcional) O número de pontos de tecnologia antiga a serem dados. Padrão: 1.

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /givebosstechpoints steam_76500000000000000 5
        ```

    ??? info "/givemetechpoints"
        **Sintaxe:** `/givemetechpoints [Amount=1]`

        **Descrição:** Dá a si mesmo X pontos de tecnologia.

        **Argumentos:**

        - `[Amount]`: (Opcional) O número de pontos de tecnologia que você deseja conceder. Padrão: 1.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /givemetechpoints 10
        ```

    ??? info "/givemebosstechpoints"
        **Sintaxe:** `/givemebosstechpoints [Amount=1]`

        **Descrição:** Dá a si mesmo X pontos de tecnologia antiga.

        **Argumentos:**

        - `[Amount]`: (Opcional) O número de pontos de tecnologia antiga que você pode conceder. Padrão: 1.

        **Permissões:** `Chat`, `Admin`

        **Exemplo:**
        ```
        /givemebosstechpoints 5
        ```


??? note "Mineração de dados"
    ??? info "/gettechids"
        **Sintaxe:** `/gettechids`

        **Descrição:** Retorna uma lista de todos os IDs de tecnologia disponíveis. RCON obtém saída JSON.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **Sintaxe:** `/getskinids`

        **Descrição:** Retorna uma lista de todos os Pal Skin IDs disponíveis. RCON obtém saída JSON.

        **Argumentos:**

        - Nenhum

        **Permissões:** `Chat`, `RCON`, `Admin`

        **Exemplo:**
        ```
        /getskinids
        ```
