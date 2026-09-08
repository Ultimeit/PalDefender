# 📁 Tipos de arquivo

**PalDefender** oferece suporte a uma variedade de tipos de arquivos personalizados que podem ser usados para configurar o comportamento do seu servidor e estender seus recursos.
Atualmente suportado:
* `Config.json`
* `WhiteList.json`
* `Banlist.json`
* `PalTemplate.json`
* `PalSummon.json`
* `Pals/ImportRules/*.json`
* `RESTAPI/RESTConfig.json`
* `RESTAPI/Tokens/*.json`

---

## ⚡ Visão geral rápida

### 🛠️ [Config.json](./Config.md)

Controla o comportamento do servidor, moderação, registro e configurações administrativas.

* **Segurança:** Anti-cheat (avisar, expulsar, banir, banir IP), filtragem name/word, proteção SteamID, verificações ilegais de stat/item.
* **Registro:** Rastreia bate-papo, RCON, logins, mortes, convocações, atividades de construção, eventos de plataformas petrolíferas.
* **Administrador:** lista de permissões de IP, login automático, godmode/cheats, visibilidade de ações administrativas.
* **Anúncios:** MOTD, mortes de jogadores, convocações, punições e eventos de saque.
* **Limites de bate-papo e jogabilidade:** Duração da mensagem, desvio de tempo de espera, PvP/PvE limites de dano, limite de corte de árvores.
* **Diversos:** RCON suporte base64, tratamento de falhas de inicialização, modo de comando chinês opcional.

---

### 👥 `WhiteList.json`

Define quem tem permissão para ingressar no servidor.
Suporta **IDs de usuário** e **endereços IP** (incluindo intervalos mascarados).

---

### 🚫 `Banlist.json`

Armazena registros de banimento PalDefender usados pelas ferramentas de banimento, unban, IP-ban e REST de punição.

* Prefira `/ban`, `/unban`, `/banip`, `/unbanip` ou REST API em vez de editar este arquivo manualmente.
* Se você precisar editá-lo manualmente, pare o servidor primeiro ou recarregue a configuração após as alterações.

---

### 🧬 [PalTemplate.json](./PalTemplate.md)

Usado para gerar ou dar Pals personalizados por meio de comandos.

* Define o **ID, apelido, gênero, estatísticas (HP/SP/MP), fome, sanidade, status brilhante, habilidades, IVs, passivos** do Pal e muito mais.
* Permite a personalização completa das **características de combate, utilidade e trabalho** de um Pal.

---

### 📍 [PalSummon.json](./PalSummon.md)

Gera um Pal personalizado em um local específico.

* Faz referência a `PalTemplate`, define **posição mundial (X, Y, Z)**.
* Configura sinalizadores como **incapturável** e desativa **efeitos de status** específicos (por exemplo, veneno, afogamento, queimadura, etc.).

---

### 🧾 [Pals/ImportRules/*.json](./PalImportRules.md)

Controla como os modelos Pal personalizados são aceitos.

* Defina limites globais em `Pals/ImportRules/Default.json`.
* Adicione substituições por Pal com arquivos como `Pals/ImportRules/Anubis.json`.
* Escolha se os valores acima do limite serão bloqueados ou fixados.
* Escolha se os passivos não permitidos bloqueiam as importações ou são removidos.

---

### 🌐 Arquivos de configuração REST API

A configuração de REST API reside em `RESTAPI/RESTConfig.json`, enquanto os tokens de portador residem em `RESTAPI/Tokens/*.json`.

* `RESTConfig.json` controla se API está habilitado, o endereço de ligação, porta, registro do console e configurações de CORS.
* Cada arquivo de token deve conter um token privado e permissões. Não compartilhe valores de token publicamente.
