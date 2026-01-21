# Python Example

```py
import requests
import random

url = 'http://127.0.0.1:17993'
# do not do this. Never store the token in any code. use smth like .env! This is only for demonstration.
auth_token = 'DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa'
headers = {
   'Authorization': f'Bearer {auth_token}'
}

def test_guilds():
    response = requests.get(url + "/v1/pdapi/guilds", headers=headers)
    print('GET /v1/pdapi/guilds Request')
    print('Status Code:', response.status_code)
    print('Response Body:', response.text)
    print()

def test_guild(guild: str):
    response = requests.get(url + f"/v1/pdapi/guild/{guild}", headers=headers)
    print('GET /v1/pdapi/guild/{guild} Request')
    print('Status Code:', response.status_code)
    print('Response Body:', response.text)
    print()

def test_version():
    response = requests.get(url + "/v1/pdapi/version", headers=headers)
    print('GET Request')
    print('Status Code:', response.status_code)
    print('Response Body:', response.text)
    print()

def test_give(user_id: str):
    payload = {
        "UserID": user_id,
        "EXP": 100000,
        "Lifmunks": 500,
        "TechnologyPoints": 500,
        "AncientTechnologyPoints": 500,
        "UnlockTechnology": "All",
        "Items": [
            { "ItemID": "Launcher_Default_5", "Count": 1 },
            { "ItemID": "ExplosiveBullet", "Count": 500 },
            { "ItemID": "LaserGatlingGun_5", "Count": 1 },
            { "ItemID": "LaserGatlingBullet", "Count": 500 },
            { "ItemID": "MultiGuidedMissileLauncher_5", "Count": 1 },
            { "ItemID": "MissileBullet", "Count": 500 },
            { "ItemID": "EnergyRocketLauncher_5", "Count": 1 },
            { "ItemID": "EnergyLauncherBullet", "Count": 500 }
        ],
        "Pals": [
            { "PalID": "Anubis", "Level": random.randint(1, 55) },
            { "PalID": "Kirin", "Level": random.randint(1, 55) },
            { "PalID": "AmaterasuWolf", "Level": random.randint(1, 55) },
            { "PalID": "WhiteTiger_Ground", "Level": random.randint(1, 55) }
        ],
        "PalTemplates": [
            "ExamplePalTemplate.json"
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Normal_01", "PalID": "Kirin", "Level": 15 },
            { "EggID": "PalEgg_Fire_01", "PalID": "Kirin" },
            { "EggID": "PalEgg_Electricity_01", "PalTemplate": "ExamplePalTemplate.json", "Level": 15 },
            { "EggID": "PalEgg_Electricity_01", "PalTemplate": "fsdf.json" }
        ]
    }

    print(payload)

    response = requests.post(url + "/v1/pdapi/give", json=payload, headers=headers)

    print('POST Request')
    print('Status Code:', response.status_code)
    print('Response Body:', response.text)
    print()

if __name__ == '__main__':
    test_guilds()
    test_guild("44BC8C67-42886202--15E0478-70B511C2")
    test_version()
    test_give("steam_76561114233277828")

```