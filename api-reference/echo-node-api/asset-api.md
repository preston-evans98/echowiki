# Asset API

## get\_asset\_holders\(asset\_id, start, limit\)

Retrieve the information about the holders of the specified asset.

### Parameters

| Option | Description |
| :--- | :--- |
| `asset_id_type asset_id` | ID of the asset to retrieve, a string that look like 1.3. |
| `uint32_t start` | The acount id to start retrieving from |
| `uint32_t limit` | Limit to that much accounts \(max 100\) |

### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        ASSET_API_ID,
        "get_asset_holders",
        [
            "1.3.0",
            "10",
            "3"
        ]
    ]
}
```

### Returns

An array of information about asset holders, that has the following structure:

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "name": "name1",
            "account_id": "1.2.18",
            "amount": "1551589041306"
        },
        {
            "name": "name2",
            "account_id": "1.2.468",
            "amount": "1505000000000"
        },
        {
            "name": "name3",
            "account_id": "1.2.19",
            "amount": "1009806000000"
        }
    ]
}
```

## get\_asset\_holders\_count\(asset\_id\)

Retrieve the number of holders of the provided asset.

### Parameters

| Option | Description |
| :--- | :--- |
| `asset_id_type asset_id` | ID of the asset to retrieve, a string that look like 1.6. |

### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        ASSET_API_ID,
        "get_asset_holders_count",
        [
            "1.3.0"
        ]
    ]
}
```

### Returns

Holders count for the specified asset.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": 1357
}
```

## get\_all\_asset\_holders\(\)

An array of all asset IDs with the number of holders.

### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        ASSET_API_ID,
        "get_all_asset_holders",
        []
    ]
}
```

### Returns

An array of the following structure:

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "asset_id": "1.3.0",
            "count": 1357
        },
        {
            "asset_id": "1.3.1",
            "count": 19
        },
        {
            "asset_id": "1.3.2",
            "count": 1
        }
    ]
}
```

