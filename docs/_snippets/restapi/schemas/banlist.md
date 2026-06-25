### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Records` | object[] | Ban records that match the supplied filters. |

`Records[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `EntryType` | string | Ban record type, such as user or IP. |
| `UserId` | string | Banned user ID, when the record is user-related. |
| `UserIP` | string | Banned IP address, when present. |
| `Reason` | string | Reason recorded for the ban or unban operation. |
| `Active` | boolean | Whether the ban record is currently active. |
| `IssuerType` | string | Source type that created the record. |
| `IssuerName` | string | Name of the actor that created the record. |
| `IssuerIP` | string | IP metadata for the issuer, when available. |
| `CreatedAt` | string | Record creation timestamp. |
| `UpdatedAt` | string | Last update timestamp. |
