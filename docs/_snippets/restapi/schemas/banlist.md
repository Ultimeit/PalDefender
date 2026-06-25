### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Banlist` | object | Banlist data after applying query filters. |

`Banlist` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Version` | integer | Banlist file format version. |
| `BannedMessage` | string | Message shown to banned players. |
| `UserEntries` | object[] | User ban entries that match the supplied filters. |
| `IPEntries` | object[] | IP ban entries that match the supplied filters. |

`UserEntries[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `UserId` | string | Banned user ID. |
| `Active` | boolean | Whether the ban is currently active. |
| `BannedBy` | object | Issuer data for the ban action. |
| `UnbannedBy` | object | Issuer data for the unban action, when present. |

`IPEntries[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `IP` | string | Banned IP address. |
| `Active` | boolean | Whether the ban is currently active. |
| `BannedBy` | object | Issuer data for the ban action. |
| `UnbannedBy` | object | Issuer data for the unban action, when present. |

Issuer object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Type` | string | Issuer type, such as `rest`, `player`, or `system`. |
| `NameValue` | string | Issuer name, user ID, token, or type fallback. |
| `IP` | string | Issuer IP address metadata. |
| `Reason` | string | Reason recorded for the action. |
| `Timestamp` | object | UTC timestamp components for the action. |

Timestamp object schema:

| Field | Type | Description |
|-------|------|-------------|
| `UTC` | integer | Unix timestamp in seconds. |
| `Year` | integer | UTC year. |
| `Month` | integer | UTC month. |
| `Day` | integer | UTC day of month. |
| `Hour` | integer | UTC hour. |
| `Min` | integer | UTC minute. |
| `Sec` | integer | UTC second. |
| `Msec` | integer | Millisecond component. |
