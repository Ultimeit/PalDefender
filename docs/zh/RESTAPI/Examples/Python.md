# Python 示例

    此示例使用当前拆分后的 REST 奖励端点。

!!! tip "ID 查询"
    使用 [paldeck.cc/items](https://paldeck.cc/items) 查询 `ItemID`，使用 [paldeck.cc/pals](https://paldeck.cc/pals) 查询 `PalID`，使用 [paldeck.cc/technology](https://paldeck.cc/technology) 查询 `TechID`。

```py
import random
import requests

url = "http://127.0.0.1:17993"
# 不要在代码中保存真实令牌。请使用环境变量或 Secret Manager。
auth_token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"
headers = {"Authorization": f"Bearer {auth_token}"}


def show(label: str, response: requests.Response):
    print(label)
    print("Status Code:", response.status_code)
    print("Response Body:", response.text)
    print()


def test_version():
    response = requests.get(url + "/v1/pdapi/version", headers=headers, timeout=10)
    show("GET /v1/pdapi/version", response)


def test_guilds():
    response = requests.get(url + "/v1/pdapi/guilds", headers=headers, timeout=10)
    show("GET /v1/pdapi/guilds", response)


def test_guild(guild_id: str):
    response = requests.get(url + f"/v1/pdapi/guild/{guild_id}", headers=headers, timeout=10)
    show(f"GET /v1/pdapi/guild/{guild_id}", response)


def test_rewards(user_id: str):
    progression = {
        "EXP": 100000,
        "Relics": {
            "CapturePower": 25,
            "MoveSpeed": 5,
        },
        "TechnologyPoints": 10,
        "AncientTechnologyPoints": 5,
    }
    show(
        "POST /v1/pdapi/give/progression",
        requests.post(url + f"/v1/pdapi/give/progression/{user_id}", json=progression, headers=headers, timeout=10),
    )

    items = {
        "Items": [
            {"ItemID": "Launcher_Default_5", "Count": 1},
            {"ItemID": "ExplosiveBullet", "Count": 500},
        ]
    }
    show(
        "POST /v1/pdapi/give/items",
        requests.post(url + f"/v1/pdapi/give/items/{user_id}", json=items, headers=headers, timeout=10),
    )

    pals = {
        "Pals": [
            {"PalID": "Anubis", "Level": random.randint(1, 55)},
            {"PalID": "Kirin", "Level": random.randint(1, 55)},
        ]
    }
    show(
        "POST /v1/pdapi/give/pals",
        requests.post(url + f"/v1/pdapi/give/pals/{user_id}", json=pals, headers=headers, timeout=10),
    )

    templates = {"PalTemplates": ["ExamplePalTemplate.json"]}
    show(
        "POST /v1/pdapi/give/paltemplate",
        requests.post(url + f"/v1/pdapi/give/paltemplate/{user_id}", json=templates, headers=headers, timeout=10),
    )

    eggs = {
        "PalEggs": [
            {"EggID": "PalEgg_Normal_01", "PalID": "Kirin", "Level": 15},
            {"EggID": "PalEgg_Electricity_01", "PalTemplate": "ExamplePalTemplate.json"},
        ]
    }
    show(
        "POST /v1/pdapi/give/paleggs",
        requests.post(url + f"/v1/pdapi/give/paleggs/{user_id}", json=eggs, headers=headers, timeout=10),
    )

    tech = {"Technology": "All"}
    show(
        "POST /v1/pdapi/learntech",
        requests.post(url + f"/v1/pdapi/learntech/{user_id}", json=tech, headers=headers, timeout=10),
    )


if __name__ == "__main__":
    test_guilds()
    test_guild("44BC8C67-42886202--15E0478-70B511C2")
    test_version()
    test_rewards("steam_76561114233277828")
```
