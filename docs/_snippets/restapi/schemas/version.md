### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Version` | object | PalDefender version details. |

`Version` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Major` | integer | Major version number. |
| `Minor` | integer | Minor version number. |
| `Patch` | integer | Patch version number. |
| `Build` | integer | Build number. |
| `Version` | string | Short version string. |
| `VersionLong` | string | Long version string. |
| `Beta` | boolean | Whether this build is marked as beta. |
