# DataBase API

## Objects

#### get\_objects\(ids\)

Get the objects corresponding to the provided IDs.

If any of the provided IDs does not map to an object, a null is returned in its position.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<object_id_type> ids` | an array of object IDs, e.g. `["1.2.1", "1.2.2", ...]` |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_objects",
        [
            [
                "1.2.1",
                "1.2.2"
            ]
        ]
    ]
}
```

#### Returns

The objects retrieved, in the order they are mentioned in ids.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.2.1",
            "registrar": "1.2.1",
            "network_fee_percentage": 0,
            "name": "placeholder-account",
            "active": {
                "weight_threshold": 1,
                "account_auths": [],
                "key_auths": []
            },
            "echorand_key": "ECHODaQencDTLD5u6LGk9JNaMoJBh6sAkGchMnZPjtJXdvG3",
            "options": {
                "voting_account": "1.2.5",
                "delegating_account": "1.2.5",
                "num_committee": 0,
                "votes": [],
                "extensions": []
            },
            "statistics": "2.5.1",
            "whitelisting_accounts": [],
            "blacklisting_accounts": [],
            "whitelisted_accounts": [],
            "blacklisted_accounts": [],
            "active_special_authority": [
                0,
                {}
            ],
            "top_n_control_flags": 0,
            "extensions": []
        },
        {
            "id": "1.2.2",
            "registrar": "1.2.2",
            "network_fee_percentage": 2000,
            "name": "relaxed-committee-account",
            "active": {
                "weight_threshold": 4,
                "account_auths": [
                    [
                        "1.2.6",
                        1
                    ],
                    [
                        "1.2.7",
                        1
                    ],
                    [
                        "1.2.8",
                        1
                    ],
                    [
                        "1.2.9",
                        1
                    ],
                    [
                        "1.2.10",
                        1
                    ],
                    [
                        "1.2.11",
                        1
                    ]
                ],
                "key_auths": []
            },
            "echorand_key": "ECHODaQencDTLD5u6LGk9JNaMoJBh6sAkGchMnZPjtJXdvG3",
            "options": {
                "voting_account": "1.2.5",
                "delegating_account": "1.2.5",
                "num_committee": 0,
                "votes": [],
                "extensions": []
            },
            "statistics": "2.5.2",
            "whitelisting_accounts": [],
            "blacklisting_accounts": [],
            "whitelisted_accounts": [],
            "blacklisted_accounts": [],
            "active_special_authority": [
                0,
                {}
            ],
            "top_n_control_flags": 0,
            "extensions": []
        }
    ]
}
```

## Subscriptions

### set\_subscribe\_callback\(callback, clear\_filter\)

Subscribe to updates.

#### Parameters

| Option | Description |
| :--- | :--- |
| `function<void(variant)> callback` | global subscription callback can be registered |
| `clear_filter` | whether subscribe to universal object creation and removal events |

If _clear\_filter_ is set to true, the API server will notify all newly created objects and ID of all newly removed objects to the client, no matter whether client subscribed to the objects

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "set_subscribe_callback",
        [
            CALLBACK_ID,
            true
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": null
}
```

#### Notice example

```javascript
{
    "method": "notice",
    "params": [ 
        CALLBACK_ID,
        [
            [
                {
                    "id": "2.1.0", ...
                },
                {
                    "id": ...
                },
                {
                    "id": ...
                },
                {
                    "id": ...
                }
            ]
        ]
    ],
}
```

### set\_pending\_transaction\_callback\(callback\)

Subscribe to pending transactions.

#### Parameters

| Option | Description |
| :--- | :--- |
| `function<void(variant)> callback` | notifications for incoming unconfirmed transactions |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "set_pending_transaction_callback",
        [
            CALLBACK_ID
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": null
}
```

#### Notice example

```javascript
{
    "method": "notice",
    "params": [
        CALLBACK_ID,
        [
            {
                "ref_block_num": 46,
                "ref_block_prefix": 620557504,
                "expiration": "2019-08-14T12:35:31",
                "operations": [
                    [
                        21,
                        {
                            "fee": {
                                "amount": 0,
                                "asset_id": "1.3.0"
                            },
                            "deposit_to_account": "1.2.26",
                            "balance_to_claim": "1.8.0",
                            "balance_owner_key": "ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu",
                            "total_claimed": {
                                "amount": "1000000000000000",
                                "asset_id": "1.3.0"
                            },
                            "extensions": []
                        }
                    ]
                ],
                "extensions": [],
                "signatures": [
                    "1c8747b07f8131b4caaa52932c14a2472b52fdff339456ceb52befe5f2f14142e0020a4ba02258a68c43668bd36fc4c56ba19234a9a525e9c493fbc251103e0a"
                ],
                "signed_with_echorand_key": false
            }
        ]
    ]
}
```

### set\_block\_applied\_callback\(callback\)

Subscribe to block applications.

#### Parameters

| Option | Description |
| :--- | :--- |
| `function<void(variant block_id)> callback` | gives a notification whenever the block block\_id is applied to the blockchain |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "set_block_applied_callback",
        [
            CALLBACK_ID
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": null
}
```

#### Notice example

```javascript
{
    "method": "notice",
    "params": [
        CALLBACK_ID,
        [
            "0013191865d4306288d52d2f648476508a159a0d"
        ]
    ]
}
```

### cancel\_all\_subscriptions\(\)

Stop receiving any notifications. Unsubscribe from all subscribed objects.

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "cancel_all_subscriptions",
        [
            CALLBACK_ID
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": null
}
```

## Blocks and transactions

### get\_block\_header\(block\_num\)

Retrieve a block header.

#### Parameters

| Option | Description |
| :--- | :--- |
| `uint32_t block_num` | height of the block whose header should be returned |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_block_header",
        [
            "1000"
        ]
    ]
}
```

#### Returns

Header of the referenced block, or null if no matching block was found.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "previous": "000003e792f925703c5e033e0b0d0419d955cd38",
        "round": 1000,
        "timestamp": "2019-08-15T15:50:15",
        "account": "1.2.12",
        "delegate": "1.2.0",
        "transaction_merkle_root": "0000000000000000000000000000000000000000",
        "vm_root": [
            "56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b42156e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
            "0.9a71ff66a2f503e4e96c4e9a2521d6a710f2d373b422332029da170d78fa1a68"
        ],
        "prev_signatures": [
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 6,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "4bd5fefe4735219d3154bd773a909aca5233c0c4d881afd93a74f60a894403b501f955e49c4c058d0cab9933a463c19ddc01d093e8c76a339bbff7b5a1875d05"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 9,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "8063dc28f2d5c58119282b474e4a8aae89abbeef3b6cfc2db26e8cf929b22c3c52c01c7983df3a968286a6d48f86804d5ef283aedd433ac1f1407e5e6777f701"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 10,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "dcf2b9b38e02cdc9af772c716d2668f945e2effa3752a23dde5b3a64b27738e51eaf1847ebe2aa41d4056215db8ecc8b61504e28cb3ffa14f9675de5fc2d1b06"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 12,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "b33102eed7bafcbeffc2f10b1bfe622e888fcaaffb3a3415de35fbd8577bb7d88c2c26eea3738eee90d448116f465eb9f512fab6982adb058c0136dfad3bdf07"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 11,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "9d0505e795c4beaea4c5121be821f5b7d037142e99bc91877fad3fc2d1b635a752a5cdde2141270fbd199dee11c2ae1b35398dc31ea4cc6425defddec549220e"
            }
        ],
        "extensions": []
    }
}
```

### get\_block\_header\_batch\(block\_nums\)

Retrieve multiple block header by block numbers.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<uint32_t> block_nums` | vector containing heights of the block whose header should be returned |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_block_header_batch",
        [
            [
                "10",
                "20",
                "30", ...
            ]
        ]
    ]
}
```

#### Returns

Array of headers of the referenced blocks, or null if no matching block was found.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        [
            10,
            {
                "previous": "00000009f7885380cc57bf4aa824d9093f370ad1",
                "round": 10,
                "timestamp": "2019-08-23T06:51:20",
                "account": "1.2.11",
                "delegate": "1.2.0",
                "transaction_merkle_root": "0000000000000000000000000000000000000000",
                "vm_root": [
                    "56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b42156e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
                    "0.9a71ff66a2f503e4e96c4e9a2521d6a710f2d373b422332029da170d78fa1a68"
                ],
                "prev_signatures": [
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 6,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "06ff421646f117611343084c91068825390af1ad49eb4a3d4534666d08adc022e63456a7951f3c0b77748c96b26aa6ef0525844c40e3daa22289ed1ef557a903"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 11,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "c0fe3fa8fa23b179ecaa7a335e98c51e2fbb8a338caa499d1f6cb8a271fec378023e3358c8b5886ac1861b95e1a25a9b73a53afa262ce557150df85e920c0a07"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 10,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "a5d45aa849328674d459845fd566485238bc10fff5eeffc65f5f0703ae2974fe2a5d7b8a2d360d13de01c556b27c1d517180c43caf08f7557f735afc8af4ee02"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 12,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "d784f31966ca12017c2e369d6c7385a5ff68964b3eb06f3c3a955114e56196968f2c6c95be1268287fb02a7d436d7785afa2fbc6b0976b6546679b14769ab902"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 8,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "9ebe07b847ab5661bc60dfb7a0e998ee4ef1c8f8bb9be1853e0ebbeb471e1082c21f7b478d87b5048a518d1898a3649b028bebabafdd53163a4c2a2d3f1cf106"
                    }
                ],
                "extensions": []
            }
        ],
        [
            20,
            {
                "previous": "00000013749cec13c673f95aa1d1954bda6374a7",
                "round": 20,
                "timestamp": "2019-08-23T06:51:51",
                "account": "1.2.12",
                "delegate": "1.2.0",
                "transaction_merkle_root": "0000000000000000000000000000000000000000",
                "vm_root": [
                    "56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b42156e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
                    "0.9a71ff66a2f503e4e96c4e9a2521d6a710f2d373b422332029da170d78fa1a68"
                ],
                "prev_signatures": [
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 9,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "15b0f5ef8f6c207e71bfbd60def7500325d1dc9facb3b7b3f6dbf1bb2a03e365f5228469fe67d89c25cd16b1205b5261f4f94195485df7608d9bbeeebabe700b"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 8,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "a4abd1fe9b8053cc63873807437d13151de9819f7e3e013281dc18c7c61ee126c65ae813836054d190813b1a78d73fa26f01d6c8e39343b930be9bb02ed37604"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 10,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "08926d2c80cf3324f14a5b1a3de46d1d645a0d71494e3f22953045e8b193c9e9c8b40394ccbd770a7c6a8b017ea99fec4776fed4b1b8105a92b64d4f06dd6205"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 12,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "14075233e2feac901c85e782e1a798ba56c62db796e07149c79860d41e74a17222c5842832aca4bfc1e85870d161fe8cdc7ac24707334c2bf1542b2d1689f803"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 9,
                        "_signer": 11,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "3292d61fa622c88385a0dec27b31bf92fe7dfc3c81d767d1ee576689ec3a71f2e0ee75e7d183ad5d4b76be5973927c4b08f9ffdd754226542ded48259891c800"
                    }
                ],
                "extensions": []
            }
        ],
        [
            30,
            {
                "previous": "0000001dc801dd1e87082ba87064188fc412bb63",
                "round": 30,
                "timestamp": "2019-08-23T06:52:31",
                "account": "1.2.6",
                "delegate": "1.2.0",
                "transaction_merkle_root": "0000000000000000000000000000000000000000",
                "vm_root": [
                    "56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b42156e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
                    "0.9a71ff66a2f503e4e96c4e9a2521d6a710f2d373b422332029da170d78fa1a68"
                ],
                "prev_signatures": [
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 7,
                        "_signer": 9,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "5283b5d0c718d2c52b291ab7f8f97a53fddac6733532189599636bd33c192e49361c649fb831027e610a715f1f7f11a6e89c0361a7cc9be0f2fe1cdd389afa0a"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 7,
                        "_signer": 8,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "0d7c6bf69e6571f7947b7d17df0fd75e04d6321beb7c0f646a9b3f517d43e90d8e2bb7baa98d9924c857e4e91870f607c33ad7fc7c88c83911442ebed889ad09"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 7,
                        "_signer": 12,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "52f9a1344c3589985049bd29bd1730b387a76b427cf876fb12740fe2e7b396f433f49b45d75810cfb2ff73d6287644631d0ee95dffea1dc7da5fc641a4781706"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 7,
                        "_signer": 11,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "c16da013f5c459d93d72af24f4498004f052635b9cc652aceb33220dfd7bfab949a5f93fe2fb836a20c386727f807f06d0ed72924eaa79af8e1cbf842ccfb208"
                    },
                    {
                        "_step": 4,
                        "_value": 0,
                        "_leader": 7,
                        "_signer": 10,
                        "_delegate": 0,
                        "_fallback": 0,
                        "_bba_sign": "2dd2fad713aa9163eb262e1cc54674ac8c66bb0c1a2138cf2a9d8c16a6fc7c8cb11d27df3217f312ec4053102dfa69baf0b32f6c10e030077ca6224c1b7ce600"
                    }
                ],
                "extensions": []
            }
        ]
    ]
}
```

### get\_block\(block\_num\)

Retrieve a full, signed block.

#### Parameters

| Option | Description |
| :--- | :--- |
| `uint32_t block_num` | height of the block to be returned |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_block",
        [
            "1000"
        ]
    ]
}
```

#### Returns

The referenced block, or null if no matching block was found.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "previous": "000003e792f925703c5e033e0b0d0419d955cd38",
        "round": 1000,
        "timestamp": "2019-08-15T15:50:15",
        "account": "1.2.12",
        "delegate": "1.2.0",
        "transaction_merkle_root": "0000000000000000000000000000000000000000",
        "vm_root": [
            "56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b42156e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
            "0.9a71ff66a2f503e4e96c4e9a2521d6a710f2d373b422332029da170d78fa1a68"
        ],
        "prev_signatures": [
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 6,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "4bd5fefe4735219d3154bd773a909aca5233c0c4d881afd93a74f60a894403b501f955e49c4c058d0cab9933a463c19ddc01d093e8c76a339bbff7b5a1875d05"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 9,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "8063dc28f2d5c58119282b474e4a8aae89abbeef3b6cfc2db26e8cf929b22c3c52c01c7983df3a968286a6d48f86804d5ef283aedd433ac1f1407e5e6777f701"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 10,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "dcf2b9b38e02cdc9af772c716d2668f945e2effa3752a23dde5b3a64b27738e51eaf1847ebe2aa41d4056215db8ecc8b61504e28cb3ffa14f9675de5fc2d1b06"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 12,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "b33102eed7bafcbeffc2f10b1bfe622e888fcaaffb3a3415de35fbd8577bb7d88c2c26eea3738eee90d448116f465eb9f512fab6982adb058c0136dfad3bdf07"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 11,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "9d0505e795c4beaea4c5121be821f5b7d037142e99bc91877fad3fc2d1b635a752a5cdde2141270fbd199dee11c2ae1b35398dc31ea4cc6425defddec549220e"
            }
        ],
        "extensions": [],
        "ed_signature": "6e1ba3b86e0dffab6a06abe3fa7725fc7bf8737773cc105957a0c671252a5c4f52e134cb65f3f81c8ba90dea3b7b5200432f755e98d8008fb0344f2da1baf90f",
        "rand": "008d90988856b11453a1727a2475f3e7ece17ca5a18dd07605200f6a56cdb18d",
        "cert": [
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 10,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "267b545c018b555a1bbf901f34ee8ded8173af60fb9e23cd6c3b152e75147327ff43b408d6574627575f29a0a6ff921812cb5008f359e888bd9d573501f4a801"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 9,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "c19e034e79c056e35b813078598cdb976e83ef0e0b957875d8d25ef6b34c28f724d7e5dd1426498a14de466f674e522ac320fbad41bb32412a5c8eb50fd72808"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 6,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "0ea7dd8a26e95ccf1b3ad24aafda694f032eacecb25f81d06fb283c60357f305d5a6ce62fa0793303b1d093c76277939aa09a1e4ae5aaeed7c19b98a87891d0c"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 8,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "34b1d6b8afaff8693117c17600686b1d759923ead90d9bdbf26eed5e02bf1caae0a095026c83245a78e4c3e0fa965e2845a6c28038af422631361e82e8e74209"
            },
            {
                "_step": 4,
                "_value": 0,
                "_leader": 12,
                "_signer": 7,
                "_delegate": 0,
                "_fallback": 0,
                "_bba_sign": "44f9ab6a4729eadeb95041b57c04fff62097815779f008ca96c67f6d8756a99bad2f0e138332e0d9172cd6a7103060e95259c0e5e3a746632894f13c2f351804"
            }
        ],
        "transactions": []
    }
}
```

### get\_block\_tx\_number\(id\)

Get the total number of transactions in block.

#### Parameters

| Option | Description |
| :--- | :--- |
| `block_id_type(ripemd160) id` | ID of the block to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_block_tx_number",
        [
            "000003e835f96c81ce14fea203ad5658f8b2f5b1"
        ]
    ]
}
```

#### Returns

If block was found total number of transaction in block, or null if no matching block was found.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": 1
}
```

### get\_block\_virtual\_ops\(block\_num\)

Get virtual ops from the block.

#### Parameters

| Option | Description |
| :--- | :--- |
| `uint32_t block_num` | height of the block to be returned |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_block_virtual_ops",
        [
            "7429"
        ]
    ]
}
```

#### Returns

Array of operation history objects, or null if no matching operation was found.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.6.2018",
            "op": [
                37,
                {
                    "fee": {
                        "amount": 0,
                        "asset_id": "1.3.0"
                    },
                    "value": {
                        "amount": 10000,
                        "asset_id": "1.3.1"
                    },
                    "account": "1.2.1013",
                    "deposit_id": "1.13.0",
                    "extensions": []
                }
            ],
            "result": [
                0,
                {}
            ],
            "block_num": 1413,
            "trx_in_block": 3,
            "op_in_trx": 0,
            "virtual_op": 15129,
            "extensions": []
        }
    ]
}
```

### get\_transaction\(block\_num, trx\_in\_block\)

Fetch an individual transaction.

#### Parameters

| Option | Description |
| :--- | :--- |
| `uint32_t block_num` | height of the block in which the transaction resides |
| `uint32_t trx_in_block` | index of the transaction in the block |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_transaction",
        [
            "1000",
            "10"
        ]
    ]
}
```

#### Returns

A processed transaction object.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "ref_block_num": 221,
        "ref_block_prefix": 4141892275,
        "expiration": "2019-08-14T14:05:52",
        "operations": [
            [
                0,
                {
                    "fee": {
                        "amount": 20,
                        "asset_id": "1.3.0"
                    },
                    "from": "1.2.26",
                    "to": "1.2.10",
                    "amount": {
                        "amount": 1000000000,
                        "asset_id": "1.3.0"
                    },
                    "extensions": []
                }
            ]
        ],
        "extensions": [],
        "signatures": [
            "5c95aedb574a86252749031f4d5cbb790037604b8c2e01e6e6eae071cb231459a4902e2932383b14e0d61d49812a73992766c958c823cd2691c5d4d4fe803b07"
        ],
        "signed_with_echorand_key": false,
        "operation_results": [
            [
                0,
                {}
            ]
        ]
    }
}
```

### get\_recent\_transaction\_by\_id\(id\)

If the transaction has not expired, this method will return the transaction for the given ID or it will return null if it is not known. Just because it is not known does not mean it wasn’t included in the blockchain.

#### Parameters

| Option | Description |
| :--- | :--- |
| `transaction_id_type(ripemd160) id` | ID of the transaction |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_recent_transaction_by_id",
        [
            "15ec7bf0b50732b49f8228e07d24365338f9e3ab"
        ]
    ]
}
```

#### Returns

A signed transaction object.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "ref_block_num": 27,
        "ref_block_prefix": 109608699,
        "expiration": "2019-08-14T14:22:17",
        "operations": [
            [
                21,
                {
                    "fee": {
                        "amount": 0,
                        "asset_id": "1.3.0"
                    },
                    "deposit_to_account": "1.2.26",
                    "balance_to_claim": "1.8.0",
                    "balance_owner_key": "ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu",
                    "total_claimed": {
                        "amount": "1000000000000000",
                        "asset_id": "1.3.0"
                    },
                    "extensions": []
                }
            ]
        ],
        "extensions": [],
        "signatures": [
            "c621da6b014a5cf6d4533ea747f0d77908663e6b4daaa3f5041f6d176f26a947847889c467d82506da9c00316e073c2435f21a6bb6e2788996c8c0b94e93bd01"
        ],
        "signed_with_echorand_key": false,
        "operation_results": [
            [
                0,
                {}
            ]
        ]
    }
}
```

## Globals

### get\_chain\_properties\(\)

Retrieve the chain property object associated with the chain.

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_chain_properties",
        []
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "id": "2.9.0",
        "chain_id": "ee3aa7f1a6cc08a2759c2c9844a0dd475d5e9ee5a4a032f74c6d9fa1c0b9c89e",
        "immutable_parameters": {
            "min_committee_member_count": 11
        },
        "extensions": []
    }
}
```

### get\_global\_properties\(\)

Retrieve the current global property object.

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_global_properties",
        []
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "id": "2.0.0",
        "parameters": {
            "current_fees": {
                "parameters": [
                    [
                        0,
                        {
                            "fee": 20
                        }
                    ],
                    [
                        1,
                        {
                            "basic_fee": 5000,
                            "premium_fee": 2000,
                            "price_per_kbyte": 1000
                        }
                    ],
                    [
                        2,
                        {
                            "fee": 200,
                            "price_per_kbyte": 100
                        }
                    ],
                    [
                        3,
                        {
                            "fee": 300000
                        }
                    ],
                    [
                        4,
                        {
                            "fee": 500
                        }
                    ],
                    [
                        5,
                        {
                            "symbol3": 500000,
                            "symbol4": 300000,
                            "long_symbol": 5000,
                            "price_per_kbyte": 10
                        }
                    ],
                    [
                        6,
                        {
                            "fee": 5000,
                            "price_per_kbyte": 10
                        }
                    ],
                    [
                        7,
                        {
                            "fee": 5000
                        }
                    ],
                    [
                        8,
                        {
                            "fee": 50000
                        }
                    ],
                    [
                        9,
                        {
                            "fee": 2000
                        }
                    ],
                    [
                        10,
                        {
                            "fee": 2000
                        }
                    ],
                    [
                        11,
                        {
                            "fee": 100
                        }
                    ],
                    [
                        12,
                        {
                            "fee": 100
                        }
                    ],
                    [
                        13,
                        {
                            "fee": 2000,
                            "price_per_kbyte": 10
                        }
                    ],
                    [
                        14,
                        {
                            "fee": 2000,
                            "price_per_kbyte": 10
                        }
                    ],
                    [
                        15,
                        {
                            "fee": 100
                        }
                    ],
                    [
                        16,
                        {
                            "fee": 50000
                        }
                    ],
                    [
                        17,
                        {
                            "fee": 200
                        }
                    ],
                    [
                        18,
                        {
                            "fee": 10
                        }
                    ],
                    [
                        19,
                        {
                            "fee": 1000
                        }
                    ],
                    [
                        20,
                        {
                            "fee": 20000
                        }
                    ],
                    [
                        21,
                        {}
                    ],
                    [
                        22,
                        {
                            "fee": 2000
                        }
                    ],
                    [
                        23,
                        {
                            "fee": 2000
                        }
                    ],
                    [
                        24,
                        {
                            "fee": 200
                        }
                    ],
                    [
                        25,
                        {
                            "fee": 200
                        }
                    ],
                    [
                        26,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        27,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        28,
                        {
                            "fee": 5000,
                            "price_per_kbyte": 100
                        }
                    ],
                    [
                        29,
                        {
                            "fee": 2000
                        }
                    ],
                    [
                        30,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        31,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        32,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        33,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        34,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        35,
                        {
                            "fee": 2000
                        }
                    ],
                    [
                        36,
                        {
                            "fee": 2000
                        }
                    ],
                    [
                        37,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        38,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        39,
                        {
                            "fee": 5000,
                            "pool_fee": 5000
                        }
                    ],
                    [
                        40,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        41,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        42,
                        {
                            "fee": 0
                        }
                    ],
                    [
                        43,
                        {
                            "fee": 2000
                        }
                    ]
                ],
                "scale": 10000
            },
            "block_interval": 5,
            "maintenance_interval": 86400,
            "maintenance_duration_seconds": 10,
            "committee_proposal_review_period": 3600,
            "maximum_transaction_size": 2097152,
            "maximum_block_size": 5242880,
            "maximum_time_until_expiration": 86400,
            "maximum_proposal_lifetime": 2419200,
            "maximum_asset_whitelist_authorities": 10,
            "maximum_asset_feed_publishers": 10,
            "maximum_committee_count": 1001,
            "maximum_authority_membership": 10,
            "reserve_percent_of_fee": 2000,
            "network_percent_of_fee": 2000,
            "max_predicate_opcode": 1,
            "accounts_per_fee_scale": 1000,
            "account_fee_scale_bitshifts": 4,
            "max_authority_depth": 2,
            "echorand_config": {
                "_time_net_1mb": 3000,
                "_time_net_256b": 1500,
                "_creator_count": 2,
                "_verifier_count": 7,
                "_ok_threshold": 5,
                "_max_bba_steps": 12,
                "_gc1_delay": 0
            },
            "sidechain_config": {
                "eth_contract_address": "cd8A072122AEB5Fa749c0c5ce817bbE58111a03D",
                "eth_committee_update_method": {
                    "method": "f1e3eb60",
                    "gas": 1000000
                },
                "eth_gen_address_method": {
                    "method": "ffcc34fd",
                    "gas": 1000000
                },
                "eth_withdraw_method": {
                    "method": "e21bd1ce",
                    "gas": 1000000
                },
                "eth_update_addr_method": {
                    "method": "f1e3eb60",
                    "gas": 1000000
                },
                "eth_withdraw_token_method": {
                    "method": "1c69c0e2",
                    "gas": 1000000
                },
                "eth_collect_tokens_method": {
                    "method": "5940a240",
                    "gas": 1000000
                },
                "eth_committee_updated_topic": "514bf7702a7d2aca90dcf3d947158aad29563a17c1dbdc76d2eae84c22420142",
                "eth_gen_address_topic": "1855f12530a368418f19b2b15227f19225915b8113c7e17d4c276e2a10225039",
                "eth_deposit_topic": "77227a376c41a7533c952ebde8d7b44ee36c7a6cec0d3448f1a1e4231398356f",
                "eth_withdraw_topic": "481c4276b65cda86cfcd095776a5e290a13932f5bed47d4f786b0ffc4d0d76ae",
                "erc20_deposit_topic": "d6a701782aaded96fbe10d6bd46445ecef12edabc8eb5d3b15fb0e57f6395911",
                "erc20_withdraw_topic": "ec7288d868c54d049bda9254803b6ddaaf0317b76e81601c0af91a480592b272",
                "ETH_asset_id": "1.3.1",
                "fines": {
                    "generate_eth_address": -10
                },
                "waiting_blocks": 30,
                "gas_price": "10000000000"
            },
            "erc20_config": {
                "contract_code": "60806040523480156200001157600080fd5b5060405162001fdb38038062001fdb8339810180604052810190808051820192919060200180518201929190602001805190602001909291905050506200006733620000bd640100000000026401000000009004565b82600190805190602001906200007f9291906200033a565b508160029080519060200190620000989291906200033a565b5080600360006101000a81548160ff021916908360ff160217905550505050620003e9565b620000e18160006200012764010000000002620019d7179091906401000000009004565b8073ffffffffffffffffffffffffffffffffffffffff167f6ae172837ea30b801fbfcdd4108aa1d5bf8ff775444fd70256b44e6bf3dfc3f660405160405180910390a250565b62000142828262000216640100000000026401000000009004565b151515620001b8576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601f8152602001807f526f6c65733a206163636f756e7420616c72656164792068617320726f6c650081525060200191505060405180910390fd5b60018260000160008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff0219169083151502179055505050565b60008073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff1614151515620002e3576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260228152602001807f526f6c65733a206163636f756e7420697320746865207a65726f20616464726581526020017f737300000000000000000000000000000000000000000000000000000000000081525060400191505060405180910390fd5b8260000160008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff16905092915050565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106200037d57805160ff1916838001178555620003ae565b82800160010185558215620003ae579182015b82811115620003ad57825182559160200191906001019062000390565b5b509050620003bd9190620003c1565b5090565b620003e691905b80821115620003e2576000816000905550600101620003c8565b5090565b90565b611be280620003f96000396000f3006080604052600436106100f1576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806306fdde03146100f6578063095ea7b31461018657806318160ddd146101eb57806323b872dd14610216578063313ce5671461029b57806339509351146102cc57806340c10f191461033157806342966c681461039657806370a08231146103c357806379cc67901461041a57806395d89b4114610467578063983b2d56146104f7578063986502751461053a578063a457c2d714610551578063a9059cbb146105b6578063aa271e1a1461061b578063dd62ed3e14610676575b600080fd5b34801561010257600080fd5b5061010b6106ed565b6040518080602001828103825283818151815260200191508051906020019080838360005b8381101561014b578082015181840152602081019050610130565b50505050905090810190601f1680156101785780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561019257600080fd5b506101d1600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919050505061078f565b604051808215151515815260200191505060405180910390f35b3480156101f757600080fd5b506102006107a6565b6040518082815260200191505060405180910390f35b34801561022257600080fd5b50610281600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506107b0565b604051808215151515815260200191505060405180910390f35b3480156102a757600080fd5b506102b0610861565b604051808260ff1660ff16815260200191505060405180910390f35b3480156102d857600080fd5b50610317600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610878565b604051808215151515815260200191505060405180910390f35b34801561033d57600080fd5b5061037c600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919050505061091d565b604051808215151515815260200191505060405180910390f35b3480156103a257600080fd5b506103c1600480360381019080803590602001909291905050506109d6565b005b3480156103cf57600080fd5b50610404600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291905050506109e3565b6040518082815260200191505060405180910390f35b34801561042657600080fd5b50610465600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610a2c565b005b34801561047357600080fd5b5061047c610a3a565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156104bc5780820151818401526020810190506104a1565b50505050905090810190601f1680156104e95780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561050357600080fd5b50610538600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610adc565b005b34801561054657600080fd5b5061054f610b8b565b005b34801561055d57600080fd5b5061059c600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610b96565b604051808215151515815260200191505060405180910390f35b3480156105c257600080fd5b50610601600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610c3b565b604051808215151515815260200191505060405180910390f35b34801561062757600080fd5b5061065c600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610c52565b604051808215151515815260200191505060405180910390f35b34801561068257600080fd5b506106d7600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610c6f565b6040518082815260200191505060405180910390f35b606060018054600181600116156101000203166002900480601f0160208091040260200160405190810160405280929190818152602001828054600181600116156101000203166002900480156107855780601f1061075a57610100808354040283529160200191610785565b820191906000526020600020905b81548152906001019060200180831161076857829003601f168201915b5050505050905090565b600061079c338484610cf6565b6001905092915050565b6000600654905090565b60006107bd848484610f77565b610856843361085185600560008a73ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020546112a190919063ffffffff16565b610cf6565b600190509392505050565b6000600360009054906101000a900460ff16905090565b6000610913338461090e85600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008973ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205461132b90919063ffffffff16565b610cf6565b6001905092915050565b600061092833610c52565b15156109c2576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260308152602001807f4d696e746572526f6c653a2063616c6c657220646f6573206e6f74206861766581526020017f20746865204d696e74657220726f6c650000000000000000000000000000000081525060400191505060405180910390fd5b6109cc83836113b5565b6001905092915050565b6109e03382611574565b50565b6000600460008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020549050919050565b610a368282611759565b5050565b606060028054600181600116156101000203166002900480601f016020809104026020016040519081016040528092919081815260200182805460018160011615610100020316600290048015610ad25780601f10610aa757610100808354040283529160200191610ad2565b820191906000526020600020905b815481529060010190602001808311610ab557829003601f168201915b5050505050905090565b610ae533610c52565b1515610b7f576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260308152602001807f4d696e746572526f6c653a2063616c6c657220646f6573206e6f74206861766581526020017f20746865204d696e74657220726f6c650000000000000000000000000000000081525060400191505060405180910390fd5b610b8881611800565b50565b610b943361185a565b565b6000610c313384610c2c85600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008973ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020546112a190919063ffffffff16565b610cf6565b6001905092915050565b6000610c48338484610f77565b6001905092915050565b6000610c688260006118b490919063ffffffff16565b9050919050565b6000600560008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054905092915050565b600073ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff1614151515610dc1576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260248152602001807f45524332303a20617070726f76652066726f6d20746865207a65726f2061646481526020017f726573730000000000000000000000000000000000000000000000000000000081525060400191505060405180910390fd5b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff1614151515610e8c576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260228152602001807f45524332303a20617070726f766520746f20746865207a65726f20616464726581526020017f737300000000000000000000000000000000000000000000000000000000000081525060400191505060405180910390fd5b80600560008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff167f8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925836040518082815260200191505060405180910390a3505050565b600073ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff1614151515611042576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260258152602001807f45524332303a207472616e736665722066726f6d20746865207a65726f20616481526020017f647265737300000000000000000000000000000000000000000000000000000081525060400191505060405180910390fd5b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415151561110d576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260238152602001807f45524332303a207472616e7366657220746f20746865207a65726f206164647281526020017f657373000000000000000000000000000000000000000000000000000000000081525060400191505060405180910390fd5b61115f81600460008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020546112a190919063ffffffff16565b600460008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055506111f481600460008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205461132b90919063ffffffff16565b600460008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a3505050565b60008083831115151561131c576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601e8152602001807f536166654d6174683a207375627472616374696f6e206f766572666c6f77000081525060200191505060405180910390fd5b82840390508091505092915050565b60008082840190508381101515156113ab576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601b8152602001807f536166654d6174683a206164646974696f6e206f766572666c6f77000000000081525060200191505060405180910390fd5b8091505092915050565b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415151561145a576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601f8152602001807f45524332303a206d696e7420746f20746865207a65726f20616464726573730081525060200191505060405180910390fd5b61146f8160065461132b90919063ffffffff16565b6006819055506114c781600460008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205461132b90919063ffffffff16565b600460008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff16600073ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a35050565b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff161415151561163f576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260218152602001807f45524332303a206275726e2066726f6d20746865207a65726f2061646472657381526020017f730000000000000000000000000000000000000000000000000000000000000081525060400191505060405180910390fd5b611654816006546112a190919063ffffffff16565b6006819055506116ac81600460008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020546112a190919063ffffffff16565b600460008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a35050565b6117638282611574565b6117fc82336117f784600560008873ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020546112a190919063ffffffff16565b610cf6565b5050565b6118148160006119d790919063ffffffff16565b8073ffffffffffffffffffffffffffffffffffffffff167f6ae172837ea30b801fbfcdd4108aa1d5bf8ff775444fd70256b44e6bf3dfc3f660405160405180910390a250565b61186e816000611ab490919063ffffffff16565b8073ffffffffffffffffffffffffffffffffffffffff167fe94479a9f7e1952cc78f2d6baab678adc1b772d936c6583def489e524cb6669260405160405180910390a250565b60008073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff1614151515611980576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260228152602001807f526f6c65733a206163636f756e7420697320746865207a65726f20616464726581526020017f737300000000000000000000000000000000000000000000000000000000000081525060400191505060405180910390fd5b8260000160008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff16905092915050565b6119e182826118b4565b151515611a56576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252601f8152602001807f526f6c65733a206163636f756e7420616c72656164792068617320726f6c650081525060200191505060405180910390fd5b60018260000160008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff0219169083151502179055505050565b611abe82826118b4565b1515611b58576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260218152602001807f526f6c65733a206163636f756e7420646f6573206e6f74206861766520726f6c81526020017f650000000000000000000000000000000000000000000000000000000000000081525060400191505060405180910390fd5b60008260000160008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff02191690831515021790555050505600a165627a7a72305820349dee86ac45cd218b5a45a2e9f0b85e882b152c7660c39dfceb517e911822ff0029",
                "create_token_fee": 1000,
                "transfer_topic": "ddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                "check_balance_method": {
                    "method": "70a08231",
                    "gas": 1000000
                },
                "burn_method": {
                    "method": "42966c68",
                    "gas": 1000000
                },
                "issue_method": {
                    "method": "40c10f19",
                    "gas": 1000000
                }
            },
            "gas_price": {
                "price": 1,
                "gas_amount": 1000
            },
            "extensions": []
        },
        "next_available_vote_id": 6,
        "active_committee_members": [
            "1.4.0",
            "1.4.1",
            "1.4.2",
            "1.4.3",
            "1.4.4"
        ]
    }
}
```

### get\_config\(\)

Retrieve compile-time constants.

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_config",
        []
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "ECHO_SYMBOL": "ECHO",
        "ECHO_ADDRESS_PREFIX": "ECHO",
        "ECHO_ED_PREFIX": "ECHO",
        "ECHO_MIN_ACCOUNT_NAME_LENGTH": 1,
        "ECHO_MAX_ACCOUNT_NAME_LENGTH": 63,
        "ECHO_MIN_ASSET_SYMBOL_LENGTH": 3,
        "ECHO_MAX_ASSET_SYMBOL_LENGTH": 16,
        "ECHO_MAX_SHARE_SUPPLY": "1000000000000000",
        "ECHO_MAX_PAY_RATE": 10000,
        "ECHO_MAX_SIG_CHECK_DEPTH": 2,
        "ECHO_MIN_TRANSACTION_SIZE_LIMIT": 1024,
        "ECHO_MIN_BLOCK_INTERVAL": 1,
        "ECHO_MAX_BLOCK_INTERVAL": 30,
        "ECHO_DEFAULT_BLOCK_INTERVAL": 5,
        "ECHO_DEFAULT_MAX_TRANSACTION_SIZE": 2097152,
        "ECHO_DEFAULT_MAX_BLOCK_SIZE": 5242880,
        "ECHO_DEFAULT_MAX_TIME_UNTIL_EXPIRATION": 86400,
        "ECHO_DEFAULT_MAINTENANCE_INTERVAL": 86400,
        "ECHO_DEFAULT_MAINTENANCE_DURATION_SECONDS": 10,
        "ECHO_MIN_UNDO_HISTORY": 10,
        "ECHO_MAX_UNDO_HISTORY": 10000,
        "ECHO_MIN_BLOCK_SIZE_LIMIT": 5120,
        "ECHO_BLOCKCHAIN_PRECISION": 100000000,
        "ECHO_BLOCKCHAIN_PRECISION_DIGITS": 8,
        "ECHO_DEFAULT_TRANSFER_FEE": 100000000,
        "ECHO_MAX_INSTANCE_ID": "281474976710655",
        "ECHO_100_PERCENT": 10000,
        "ECHO_1_PERCENT": 100,
        "ECHO_DEFAULT_PRICE_FEED_LIFETIME": 86400,
        "ECHO_DEFAULT_MAX_AUTHORITY_MEMBERSHIP": 10,
        "ECHO_DEFAULT_MAX_ASSET_WHITELIST_AUTHORITIES": 10,
        "ECHO_DEFAULT_MAX_ASSET_FEED_PUBLISHERS": 10,
        "ECHO_COLLATERAL_RATIO_DENOM": 1000,
        "ECHO_MIN_COLLATERAL_RATIO": 1001,
        "ECHO_MAX_COLLATERAL_RATIO": 32000,
        "ECHO_DEFAULT_MAINTENANCE_COLLATERAL_RATIO": 1750,
        "ECHO_DEFAULT_MAX_SHORT_SQUEEZE_RATIO": 1500,
        "ECHO_DEFAULT_MAX_COMMITTEE": 1001,
        "ECHO_DEFAULT_MAX_PROPOSAL_LIFETIME_SEC": 2419200,
        "ECHO_DEFAULT_COMMITTEE_PROPOSAL_REVIEW_PERIOD_SEC": 1209600,
        "ECHO_DEFAULT_NETWORK_PERCENT_OF_FEE": 2000,
        "ECHO_DEFAULT_BURN_PERCENT_OF_FEE": 2000,
        "ECHO_DEFAULT_MAX_ASSERT_OPCODE": 1,
        "ECHO_DEFAULT_ACCOUNTS_PER_FEE_SCALE": 1000,
        "ECHO_DEFAULT_ACCOUNT_FEE_SCALE_BITSHIFTS": 4,
        "ECHO_MAX_URL_LENGTH": 127,
        "ECHO_DEFAULT_COMMITEE_PAY_VESTING_SECONDS": 86400,
        "ECHO_COMMITTEE_ACCOUNT": "1.2.0",
        "ECHO_RELAXED_COMMITTEE_ACCOUNT": "1.2.2",
        "ECHO_NULL_ACCOUNT": "1.2.3",
        "ECHO_TEMP_ACCOUNT": "1.2.4"
    }
}
```

### get\_chain\_id\(\)

Get the chain ID.

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_chain_id",
        []
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": "31cde47f6b94908c2b2ed67c3365c7f58bb744dac145ecf6dc0941e1167c34ab"
}
```

### get\_dynamic\_global\_properties\(\)

Retrieve the current dynamic global property object.

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_dynamic_global_properties",
        []
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "id": "2.1.0",
        "head_block_number": 105496,
        "head_block_id": "00019c18e813c010fcd54663f2f382fa8f9ccd89",
        "time": "2019-08-21T08:45:29",
        "next_maintenance_time": "2019-08-22T00:00:00",
        "last_budget_time": "2019-08-21T00:00:03",
        "committee_budget": 4,
        "accounts_registered_this_interval": 13,
        "recently_missed_count": 1000603,
        "current_aslot": 388256,
        "dynamic_flags": 0,
        "last_irreversible_block_num": 105481,
        "extensions": []
    }
}
```

## Keys

### get\_key\_references\(keys\)

Retreive an array of account IDs associated with the given keys.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<public_key_t> keys` | an array of public keys |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_key_references",
        [
            [
                "ECHO61p48u6pHnjSAYP5kzQ4RGNQzFDBDYRrfqrAuhtb2Hdm",
                "ECHO6ffcvxMD8XrWWNRSPmusHSFFjuPe9qnnVbVQBgERd3fi", ...
            ]
        ]
    ]
}
```

#### Returns

An array of arrays of account IDs for every public key provided.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        [
            "1.2.14"
        ],
        [
            "1.2.13"
        ]
    ]
}
```

### is\_public\_key\_registered\(public\_key\)

Determine whether of a public key is _currently_ linked to any _registered_ \(i.e. non-stealth\) account on the blockchain.

#### Parameters

| Option | Description |
| :--- | :--- |
| `public_key_t key` | public key |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "is_public_key_registered",
        [
            "ECHOEdjiBUy2RBJ9sMN7jKMK4x9Fa4QVR7JgtNLwbgcZtcZB"
        ]
    ]
}
```

#### Returns

Whether a public key is known.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": false
}
```

## Accounts

### get\_accounts\(account\_ids\)

Get a list of accounts by ID. This function has semantics identical to get\_objects.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<account_id_type> accounts_ids` | IDs of the accounts to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_accounts",
        [
            [
                "1.2.10"
            ]
        ]
    ]
}
```

#### Returns

The accounts corresponding to the provided IDs.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.2.10",
            "registrar": "1.2.4",
            "network_fee_percentage": 2000,
            "name": "init4",
            "active": {
                "weight_threshold": 1,
                "account_auths": [],
                "key_auths": [
                    [
                        "ECHOCh3WGJCMKkBJHFJpzaC378cwwYisNbNKpD6oYhcuA6nR",
                        1
                    ]
                ]
            },
            "echorand_key": "ECHOCh3WGJCMKkBJHFJpzaC378cwwYisNbNKpD6oYhcuA6nR",
            "options": {
                "voting_account": "1.2.5",
                "delegating_account": "1.2.5",
                "num_committee": 0,
                "votes": [],
                "extensions": []
            },
            "statistics": "2.5.10",
            "whitelisting_accounts": [],
            "blacklisting_accounts": [],
            "whitelisted_accounts": [],
            "blacklisted_accounts": [],
            "active_special_authority": [
                0,
                {}
            ],
            "top_n_control_flags": 0,
            "extensions": []
        }
    ]
}
```

### get\_full\_accounts\(names\_or\_ids, subscribe\)

Fetch all objects relevant to the specified accounts and subscribe to updates.

This function fetches all relevant objects for the given accounts, and subscribes to updates to the given accounts. If any of the strings in names\_or\_ids cannot be tied to an account, that input will be ignored. All other accounts will be retrieved and subscribed.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<string> names_or_ids` | an array of either the names or IDs of accounts to retrieve \(can be mixed\) |
| `bool subscribe` | whether to subscribe to updates |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_full_accounts",
        [
            [
                "1.2.10"
            ],
            "false"
        ]
    ]
}
```

#### Returns

A map of strings from names\_or\_ids to the corresponding accounts.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        [
            "1.2.10",
            {
                "account": {
                    "id": "1.2.10",
                    "registrar": "1.2.4",
                    "network_fee_percentage": 2000,
                    "name": "init4",
                    "active": {
                        "weight_threshold": 1,
                        "account_auths": [],
                        "key_auths": [
                            [
                                "ECHOCh3WGJCMKkBJHFJpzaC378cwwYisNbNKpD6oYhcuA6nR",
                                1
                            ]
                        ]
                    },
                    "echorand_key": "ECHOCh3WGJCMKkBJHFJpzaC378cwwYisNbNKpD6oYhcuA6nR",
                    "options": {
                        "voting_account": "1.2.5",
                        "delegating_account": "1.2.5",
                        "num_committee": 0,
                        "votes": [],
                        "extensions": []
                    },
                    "statistics": "2.5.10",
                    "whitelisting_accounts": [],
                    "blacklisting_accounts": [],
                    "whitelisted_accounts": [],
                    "blacklisted_accounts": [],
                    "active_special_authority": [
                        0,
                        {}
                    ],
                    "top_n_control_flags": 0,
                    "extensions": []
                },
                "statistics": {
                    "id": "2.5.10",
                    "owner": "1.2.10",
                    "most_recent_op": "2.8.274",
                    "total_ops": 8,
                    "removed_ops": 0,
                    "total_blocks": 5295,
                    "total_core_in_orders": 0,
                    "pending_fees": 0,
                    "generated_eth_address": false,
                    "committeeman_rating": 0,
                    "extensions": []
                },
                "registrar_name": "temp-account",
                "votes": [],
                "balances": [
                    {
                        "id": "2.4.6",
                        "owner": "1.2.10",
                        "asset_type": "1.3.0",
                        "balance": "1000000000000",
                        "extensions": []
                    }
                ],
                "vesting_balances": [
                    {
                        "id": "1.7.4",
                        "owner": "1.2.10",
                        "balance": {
                            "amount": 186563,
                            "asset_id": "1.3.0"
                        },
                        "policy": [
                            1,
                            {
                                "vesting_seconds": 86400,
                                "start_claim": "1970-01-01T00:00:00",
                                "coin_seconds_earned": "11835590400",
                                "coin_seconds_earned_last_update": "2019-08-21T07:14:21"
                            }
                        ],
                        "extensions": []
                    }
                ],
                "proposals": [],
                "assets": []
            }
        ]
    ]
}
```

#### Notice example

The notification was received by performing the account update operation for changing delegating\_account.

```javascript
{
    "method": "notice",
    "params": [
        CALLBACK_ID,
        [
            [
                {
                    "id": "1.2.10",
                    "registrar": "1.2.4",
                    "network_fee_percentage": 2000,
                    "name": "init4",
                    "active": {
                        "weight_threshold": 1,
                        "account_auths": [],
                        "key_auths": [
                            [
                                "ECHOCh3WGJCMKkBJHFJpzaC378cwwYisNbNKpD6oYhcuA6nR",
                                1
                            ]
                        ]
                    },
                    "echorand_key": "ECHOCh3WGJCMKkBJHFJpzaC378cwwYisNbNKpD6oYhcuA6nR",
                    "options": {
                        "voting_account": "1.2.5",
                        "delegating_account": "1.2.13",
                        "num_committee": 0,
                        "votes": [],
                        "extensions": []
                    },
                    "statistics": "2.5.10",
                    "whitelisting_accounts": [],
                    "blacklisting_accounts": [],
                    "whitelisted_accounts": [],
                    "blacklisted_accounts": [],
                    "active_special_authority": [
                        0,
                        {}
                    ],
                    "top_n_control_flags": 0,
                    "extensions": []
                }
            ]
        ]
    ]
}
```

### get\_account\_by\_name\(name\)

Get the account object by it's name.

#### Parameters

| Option | Description |
| :--- | :--- |
| `string name` | account name |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_account_by_name",
        [
            "nathan"
        ]
    ]
}
```

#### Returns

Account object it the account exists, null otherwise.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "id": "1.2.12",
        "registrar": "1.2.4",
        "network_fee_percentage": 2000,
        "name": "nathan",
        "active": {
            "weight_threshold": 1,
            "account_auths": [],
            "key_auths": [
                [
                    "ECHO9GUY5DUWy5bHZWPwhdmV1oi8QdvBcwxKF73WESeHDoWQ",
                    1
                ]
            ]
        },
        "echorand_key": "ECHO9GUY5DUWy5bHZWPwhdmV1oi8QdvBcwxKF73WESeHDoWQ",
        "options": {
            "voting_account": "1.2.5",
            "delegating_account": "1.2.5",
            "num_committee": 0,
            "votes": [],
            "extensions": []
        },
        "statistics": "2.5.12",
        "whitelisting_accounts": [],
        "blacklisting_accounts": [],
        "whitelisted_accounts": [],
        "blacklisted_accounts": [],
        "active_special_authority": [
            0,
            {}
        ],
        "top_n_control_flags": 0,
        "extensions": []
    }
}
```

### get\_account\_references\(account\_id\)

All accounts that refer to the key or account id in their active authorities.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type account_id` | id of the account |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_account_references",
        [
            "1.2.10"
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        "1.2.0",
        "1.2.2"
    ]
}
```

### lookup\_account\_names\(account\_names\)

Get a list of accounts by name. This function has semantics identical to get\_objects.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<string> account_names` | names of the accounts to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "lookup_account_names",
        [
            [
                "nathan"
            ]
        ]
    ]
}
```

#### Returns

The accounts holding the provided names.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.2.12",
            "registrar": "1.2.4",
            "network_fee_percentage": 2000,
            "name": "nathan",
            "active": {
                "weight_threshold": 1,
                "account_auths": [],
                "key_auths": [
                    [
                        "ECHO9GUY5DUWy5bHZWPwhdmV1oi8QdvBcwxKF73WESeHDoWQ",
                        1
                    ]
                ]
            },
            "echorand_key": "ECHO9GUY5DUWy5bHZWPwhdmV1oi8QdvBcwxKF73WESeHDoWQ",
            "options": {
                "voting_account": "1.2.5",
                "delegating_account": "1.2.5",
                "num_committee": 0,
                "votes": [],
                "extensions": []
            },
            "statistics": "2.5.12",
            "whitelisting_accounts": [],
            "blacklisting_accounts": [],
            "whitelisted_accounts": [],
            "blacklisted_accounts": [],
            "active_special_authority": [
                0,
                {}
            ],
            "top_n_control_flags": 0,
            "extensions": []
        }
    ]
}
```

### lookup\_accounts\(lower\_bound\_name, limit\)

Get names and IDs for registered accounts.

#### Parameters

| Option | Description |
| :--- | :--- |
| `string lower_bound_name` | lower bound of the first name to return |
| `uint32_t limit` | maximum number of results to return must not exceed 1000 |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "lookup_accounts",
        [
            "init1",
            "3"
        ]
    ]
}
```

#### Returns

Map of account names to corresponding IDs.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        [
            "init1",
            "1.2.7"
        ],
        [
            "init2",
            "1.2.8"
        ],
        [
            "init3",
            "1.2.9"
        ]
    ]
}
```

### get\_account\_count\(\)

Get the total number of accounts registered with the blockchain.

#### Example

```javascript
{
    "id": 3,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_account_count",
        []
    ]
}
```

#### Returns

```javascript
{
    "id": 3,
    "jsonrpc": "2.0",
    "result": 27
}
```

### get\_account\_addresses\(account\_id, from, limit\)

Get addresses of specified account.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type account_id` | ID of the account |
| `uint64_t from` | number of block to start retrieve from |
| `unsigned limit` | maximum number of addresses to return |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        2,
        "get_account_addresses",
        [
            "1.2.26",
            "0",
            "1"
        ]
    ]
}
```

#### Returns

Addresses owned by account in specified ids interval.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "2.15.0",
            "owner": "1.2.26",
            "label": "label1",
            "address": "6b34edbee7b4eaf077ab8217a50ac43a00d0ba05",
            "extensions": []
        }
    ]
}
```

### get\_account\_by\_address\(address\)

Get owner of specified address.

#### Parameters

| Option | Description |
| :--- | :--- |
| `ripemd160 address` | address in form of ripemd160 hash |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_account_by_address",
        [
            "8815c69de5d32d3061e52ca9386446332225b43d"
        ]
    ]
}
```

#### Returns

Account id of owner.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": "1.2.15"
}
```

## Contracts

### get\_contract\(contract\_id\)

Get a contract info from VM by ID.

#### Parameters

| Option | Description |
| :--- | :--- |
| `contract_id_type contract_id` | ID of the contract to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_contract",
        [
            "1.9.0"
        ]
    ]
}
```

#### Returns

The contracts data from VM corresponding to the provided ID.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        0,
        {
            "code": "6080604052600436106100d557...",
            "storage": [
                [
                    "036b6384b5eca791c62761152d0c79bb0604c104a5fb6f4eb0703f3154bb3db0",
                    [
                        "05",
                        "d3c21bcecceda1000000"
                    ]
                ], ...
            ]
        }
    ]
}
```

### get\_contracts\(contract\_ids\)

Get a list of contracts by ID.

**Parameters**

| Option | Description |
| :--- | :--- |
| `vector<contract_id_type> contract_ids` | IDs of the contracts to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_contracts",
        [
            "1.9.0",
            "1.9.1", ...
        ]
    ]
}
```

#### Returns

The contracts corresponding to the provided IDs.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.9.0",
            "type": "evm",
            "destroyed": false,
            "statistics": "2.17.0",
            "owner": "1.2.27",
            "extensions": []
        },
        {
            "id": "1.9.1",
            "type": "evm",
            "destroyed": false,
            "statistics": "2.17.1",
            "supported_asset_id": "1.3.0",
            "owner": "1.2.38",
            "extensions": []
        }
    ]
}
```

### get\_contract\_logs\(contract\_id, from, to\)

Get logs of specified contract.

#### Parameters

| Option | Description |
| :--- | :--- |
| `contract_id_type contract_id` | ID of the contract |
| `uint32_t from` | number of block to start retrieve from |
| `uint32_t to` | number of block to end to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_contract_logs",
        [
            "1.9.3",
            "500",
            "100"
        ]
    ]
}
```

#### Returns

The contracts logs from specified blocks interval.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "address": "0100000000000000000000000000000000000003",
            "log": [
                "a1f905024bf9f0430b6d981173eb6df240bdf128fbadea8a869257b4015673e5"
            ],
            "data": "0000000000000000000000000000000000000000000000000000000000000097"
        }
    ]
}
```

### subscribe\_contracts\(contracts\_ids\)

Subscription to change the contract uses database-api.md\#set\_subscribe\_callback-callback-clear\_filter.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<contract_id_type> contracts_ids` | IDs of the contracts to subscribe |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "subscribe_contracts",
        [
            [
                "1.9.3"
            ]
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": null
}
```

#### Notice example

```javascript
{
    "method": "notice",
    "params": [
        CALLBACK_ID,
        [
            [
                {
                    "address": "0100000000000000000000000000000000000003",
                    "log": [
                        "a1f905024bf9f0430b6d981173eb6df240bdf128fbadea8a869257b4015673e5"
                    ],
                    "data": "0000000000000000000000000000000000000000000000000000000000000097"
                }
            ]
        ]
    ]
}
```

### subscribe\_contract\_logs\(callback, contract\_id, from, to\)

Subscribe to contract's logs.

If you want to always receive alerts, then you can specify a very large number as the end of the range of the blocks you listen to, for example, `999999999`.

When calling this method, it will return all already existing events in the specified range as well as the `get_contract_logs` method.

#### Parameters

| Option | Description |
| :--- | :--- |
| `function<void(variant)> cb` | callback method which is called when contracts has new logs |
| `contract_id_type contract_id` | ID of the contract |
| `uint32_t from` | number of block to start retrieve from |
| `uint32_t to` | number of block to end to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "subscribe_contract_logs",
        [
            "7",
            "1.9.3",
            "680",
            "100"
        ]
    ]
}
```

#### Returns

The contracts logs from specified blocks interval.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": null
}
```

#### Notice example

```javascript
{
    "method": "notice",
    "params": [
        CALLBACK_ID,
        [
            [
                {
                    "address": "0100000000000000000000000000000000000003",
                    "log": [
                        "a1f905024bf9f0430b6d981173eb6df240bdf128fbadea8a869257b4015673e5"
                    ],
                    "data": "0000000000000000000000000000000000000000000000000000000000000097"
                }
            ]
        ]
    ]
}
```

### get\_contract\_result\(id\)

Get contract result from VM for specified result\_id

#### Parameters

| Option | Description |
| :--- | :--- |
| `contract_result_id_type id` | ID of result to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_contract_result",
        [
            "1.10.0"
        ]
    ]
}
```

#### Returns

Result of execution.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        0,
        {
            "exec_res": {
                "excepted": "None",
                "new_address": "0100000000000000000000000000000000000000",
                "output": "608060405260...",
                "code_deposit": "Success",
                "gas_refunded": 0,
                "gas_for_deposit": 720877,
                "deposit_size": 2601
            },
            "tr_receipt": {
                "status_code": 1,
                "gas_used": 885323,
                "bloom": "00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
                "log": []
            }
        }
    ]
}
```

### call\_contract\_no\_changing\_state\(contract\_id, registrar\_account, asset\_type, code\)

Call the provided contract, but don't change the state.

#### Parameters

| Option | Description |
| :--- | :--- |
| `contract_id_type contract_id` | ID of the contract |
| `account_id_type registrar_account` | name of the account calling the contract |
| `asset_id_type asset_type` | the type of the asset transfered to the contract |
| `string code` | the hash of the method to call\(or name for x86-x64 contracts\) |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "call_contract_no_changing_state",
        [
            "1.9.3",
            "1.2.26",
            "1.3.0",
            "6d4ce63c"
        ]
    ]
}
```

#### Returns

Result of execution.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": "0000000000000000000000000000000000000000000000000000000000000093"
}
```

## Balances

### get\_account\_balances\(id, assets\)

Get an account’s balances in various assets.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type id` | ID of the account to get balances for |
| `flat_set<asset_id_type> assets` | an array of IDs of the assets to get balances of; if empty, get all assets account has a balance in |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_account_balances",
        [
            "1.2.15",
            [
                "1.3.0", ...
            ]
        ]
    ]
}
```

#### Returns

An array of balances of the account.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "amount": "799959899999120",
            "asset_id": "1.3.0"
        }
    ]
}
```

### get\_contract\_balances\(contract\_id\)

Get an contract's balances in various assets.

#### Parameters

| Option | Description |
| :--- | :--- |
| `contract_id_type contract_id` | ID of the contract to get balances for |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_contract_balances",
        [
            "1.9.0"
        ]
    ]
}
```

#### Returns

An array of balances of the contract.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "amount": 100,
            "asset_id": "1.3.0"
        }
    ]
}
```

### get\_named\_account\_balances\(name, assets\)

Semantically equivalent to _get\_account\_balances_, but takes a name instead of an ID.

#### Parameters

| Option | Description |
| :--- | :--- |
| `string name` | name of the account to get balances for |
| `flat_set<asset_id_type> assets` | an array of IDs of the assets to get balances of; if empty, get all assets account has a balance in |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_named_account_balances",
        [
            "nathan",
            [
                "1.3.0", ...
            ]
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "amount": "991999999999840",
            "asset_id": "1.3.0"
        }
    ]
}
```

### get\_balance\_objects\(keys\)

Returns all unclaimed balance objects for a set of addresses.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<public_key_t> keys` | an array of public keys |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_balance_objects",
        [
            [
                "ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu",
                ...
            ]
        ]
    ]
}
```

#### Returns

An array of balances objects.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.8.0",
            "owner": "ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu",
            "balance": {
                "amount": "1000000000000000",
                "asset_id": "1.3.0"
            },
            "last_claim_date": "1970-01-01T00:00:00",
            "extensions": []
        }
    ]
}
```

### get\_vested\_balances\(objs\)

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<balance_id_type> objs` | an array of balance ID |

#### Example

```javascript
{
    "id": 3,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_vested_balances",
        [
            [
                "1.8.0",
                ...
            ]
        ]
    ]
}
```

#### Returns

An array of assets vested.

```javascript
{
    "id": 3,
    "jsonrpc": "2.0",
    "result": [
        {
            "amount": "1000000000000000",
            "asset_id": "1.3.0"
        }
    ]
}
```

### get\_vesting\_balances\(account\_id\)

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type account_ids` | the id of account to use |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_vesting_balances",
        [
            "1.2.26"
        ]
    ]
}
```

#### Returns

An array of vesting balances.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.7.0",
            "owner": "1.2.26",
            "balance": {
                "amount": 100,
                "asset_id": "1.3.0"
            },
            "policy": [
                0,
                {
                    "begin_timestamp": "1970-01-01T00:00:00",
                    "vesting_cliff_seconds": 0,
                    "vesting_duration_seconds": 0,
                    "begin_balance": 100
                }
            ],
            "extensions": []
        }
    ]
}
```

## Assets

### get\_assets\(asset\_ids\)

Get a list of assets by ID. This function has semantics identical to get\_objects.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<asset_id_type> asset_ids` | IDs of the assets to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_assets",
        [
            [
                "1.3.0",
                "1.3.1", ...
            ]
        ]
    ]
}
```

#### Returns

The assets corresponding to the provided IDs.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.3.0",
            "symbol": "ECHO",
            "precision": 8,
            "issuer": "1.2.3",
            "options": {
                "max_supply": "1000000000000000",
                "issuer_permissions": 0,
                "flags": 0,
                "core_exchange_rate": {
                    "base": {
                        "amount": 1,
                        "asset_id": "1.3.0"
                    },
                    "quote": {
                        "amount": 1,
                        "asset_id": "1.3.0"
                    }
                },
                "whitelist_authorities": [],
                "blacklist_authorities": [],
                "description": "",
                "extensions": []
            },
            "dynamic_asset_data_id": "2.2.0",
            "extensions": []
        },
        {
            "id": "1.3.1",
            "symbol": "EETH",
            "precision": 6,
            "issuer": "1.2.1",
            "options": {
                "max_supply": "1000000000000000",
                "issuer_permissions": 15,
                "flags": 0,
                "core_exchange_rate": {
                    "base": {
                        "amount": 1,
                        "asset_id": "1.3.0"
                    },
                    "quote": {
                        "amount": 1,
                        "asset_id": "1.3.1"
                    }
                },
                "whitelist_authorities": [],
                "blacklist_authorities": [],
                "description": "ethereum asset",
                "extensions": []
            },
            "dynamic_asset_data_id": "2.2.1",
            "extensions": []
        }
    ]
}
```

### list\_assets\(lower\_bound\_symbol, limit\)

Get assets alphabetically by symbol name.

#### Parameters

| Option | Description |
| :--- | :--- |
| `string lower_bound_symbol` | lower bound of symbol names to retrieve |
| `uint32_t limit` | maximum number of assets to fetch \(must not exceed 100\) |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "list_assets",
        [
            "",
            "2"
        ]
    ]
}
```

#### Returns

The assets found.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.3.0",
            "symbol": "ECHO",
            "precision": 8,
            "issuer": "1.2.3",
            "options": {
                "max_supply": "1000000000000000",
                "issuer_permissions": 0,
                "flags": 0,
                "core_exchange_rate": {
                    "base": {
                        "amount": 1,
                        "asset_id": "1.3.0"
                    },
                    "quote": {
                        "amount": 1,
                        "asset_id": "1.3.0"
                    }
                },
                "whitelist_authorities": [],
                "blacklist_authorities": [],
                "description": "",
                "extensions": []
            },
            "dynamic_asset_data_id": "2.2.0",
            "extensions": []
        },
        {
            "id": "1.3.1",
            "symbol": "EETH",
            "precision": 6,
            "issuer": "1.2.1",
            "options": {
                "max_supply": "1000000000000000",
                "issuer_permissions": 15,
                "flags": 0,
                "core_exchange_rate": {
                    "base": {
                        "amount": 1,
                        "asset_id": "1.3.0"
                    },
                    "quote": {
                        "amount": 1,
                        "asset_id": "1.3.1"
                    }
                },
                "whitelist_authorities": [],
                "blacklist_authorities": [],
                "description": "ethereum asset",
                "extensions": []
            },
            "dynamic_asset_data_id": "2.2.1",
            "extensions": []
        }
    ]
}
```

### lookup\_asset\_symbols\(symbols\_or\_ids\)

Get a list of assets by symbol. This function has semantics identical to get\_objects.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<string> symbols_or_ids` | symbols or stringified IDs of the assets to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "lookup_asset_symbols",
        [
            [
                "EETH",
                "1.3.0"
            ]
        ]
    ]
}
```

#### Returns

The assets corresponding to the provided symbols or IDs.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.3.1",
            "symbol": "EETH",
            "precision": 6,
            "issuer": "1.2.1",
            "options": {
                "max_supply": "1000000000000000",
                "issuer_permissions": 15,
                "flags": 0,
                "core_exchange_rate": {
                    "base": {
                        "amount": 1,
                        "asset_id": "1.3.0"
                    },
                    "quote": {
                        "amount": 1,
                        "asset_id": "1.3.1"
                    }
                },
                "whitelist_authorities": [],
                "blacklist_authorities": [],
                "description": "ethereum asset",
                "extensions": []
            },
            "dynamic_asset_data_id": "2.2.1",
            "extensions": []
        },
        {
            "id": "1.3.0",
            "symbol": "ECHO",
            "precision": 8,
            "issuer": "1.2.3",
            "options": {
                "max_supply": "1000000000000000",
                "issuer_permissions": 0,
                "flags": 0,
                "core_exchange_rate": {
                    "base": {
                        "amount": 1,
                        "asset_id": "1.3.0"
                    },
                    "quote": {
                        "amount": 1,
                        "asset_id": "1.3.0"
                    }
                },
                "whitelist_authorities": [],
                "blacklist_authorities": [],
                "description": "",
                "extensions": []
            },
            "dynamic_asset_data_id": "2.2.0",
            "extensions": []
        }
    ]
}
```

## Committee members

### get\_committee\_members\(committee\_member\_ids\)

Get a list of committee\_members by ID. This function has semantics identical to get\_objects.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<committee_member_id_type> committee_member_ids` | IDs of the committee\_members to retrieve |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_committee_members",
        [
            [
                "1.4.0",
                "1.4.1"
            ]
        ]
    ]
}
```

#### Returns

The committee\_members corresponding to the provided IDs.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.4.0",
            "committee_member_account": "1.2.6",
            "pay_vb": "1.7.0",
            "vote_id": "0:0",
            "total_votes": 0,
            "url": "",
            "eth_address": "f372c3b578534Ac5C1Cf0Cca7049A279d1ca3e79",
            "extensions": []
        },
        {
            "id": "1.4.1",
            "committee_member_account": "1.2.7",
            "pay_vb": "1.7.1",
            "vote_id": "0:1",
            "total_votes": 0,
            "url": "",
            "eth_address": "Fba802D86f8d9b080eD247e712751DDBF86086A9",
            "extensions": []
        }
    ]
}
```

### get\_committee\_member\_by\_account\(account\)

Get the committee\_member owned by a given account.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type account` | the ID of the account whose committee\_member should be retrieved |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_committee_member_by_account",
        [
            "1.2.6"
        ]
    ]
}
```

#### Returns

The committee\_member object, or null if the account does not have a committee\_member.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "id": "1.4.0",
        "committee_member_account": "1.2.6",
        "pay_vb": "1.7.0",
        "vote_id": "0:0",
        "total_votes": 0,
        "url": "",
        "eth_address": "f372c3b578534Ac5C1Cf0Cca7049A279d1ca3e79",
        "extensions": []
    }
}
```

### lookup\_committee\_member\_accounts\(lower\_bound\_name, limit\)

Get names and IDs for registered committee\_members.

#### Parameters

| Option | Description |
| :--- | :--- |
| `string lower_bound_name` | lower bound of the first name to return |
| `uint32_t limit` | maximum number of results to return -- must not exceed 1000 |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "lookup_committee_member_accounts",
        [
            "",
            "1000"
        ]
    ]
}
```

#### Returns

Map of committee\_member names to corresponding IDs.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        [
            "init0",
            "1.4.0"
        ],
        [
            "init1",
            "1.4.1"
        ],
        [
            "init2",
            "1.4.2"
        ],
        [
            "init3",
            "1.4.3"
        ],
        [
            "init4",
            "1.4.4"
        ],
        [
            "init5",
            "1.4.5"
        ]
    ]
}
```

### get\_committee\_count\(\)

Get the total number of committee registered with the blockchain

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_committee_count",
        []
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": 9
}
```

## Votes

### lookup\_vote\_ids\(votes\)

Given a set of votes, return the objects they are voting for.

This will be a mixture of committee\_member\_object.

The results will be in the same order as the votes. null will be returned for any vote ids that are not found.

#### Parameters

| Option | Description |
| :--- | :--- |
| `vector<vote_id_type> votes` | an array votes |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "lookup_vote_ids",
        [
            [
                "0:0",
                "0:1"
            ]
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.4.0",
            "committee_member_account": "1.2.6",
            "pay_vb": "1.7.0",
            "vote_id": "0:0",
            "total_votes": 0,
            "url": "",
            "eth_address": "f372c3b578534Ac5C1Cf0Cca7049A279d1ca3e79",
            "extensions": []
        },
        {
            "id": "1.4.1",
            "committee_member_account": "1.2.7",
            "pay_vb": "1.7.1",
            "vote_id": "0:1",
            "total_votes": 0,
            "url": "",
            "eth_address": "Fba802D86f8d9b080eD247e712751DDBF86086A9",
            "extensions": []
        }
    ]
}
```

## Authority / validation

### get\_transaction\_hex\(trx\)

Get a hexdump of the serialized binary form of a signed transaction.

#### Parameters

| Option | Description |
| :--- | :--- |
| `signed_transaction trx` | object signed transaction |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_transaction_hex",
        [
            {
                "ref_block_num": "221",
                "ref_block_prefix": "4141892275",
                "expiration": "1970-01-01T00:00:00",
                "operations": []
            }
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": "dd00b342e0f60000000000000000"
}
```

### get\_required\_signatures\(ctrx, available\_keys\)

Takes a partially signed transaction and a set of public keys that the owner has the ability to sign for and return the minimal subset of public keys that should add signatures to the transaction.

#### Parameters

| Option | Description |
| :--- | :--- |
| `signed_transaction trx` | object signed transaction |
| `flat_set<public_key_t> available_keys` | an array of public keys |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_required_signatures",
        [
            {
                "ref_block_num": 1719,
                "ref_block_prefix": 3664479505,
                "expiration": "2019-08-21T14:16:03",
                "operations": [
                    [
                        28,
                        {
                            "fee": {
                                "amount": 5001,
                                "asset_id": "1.3.0"
                            },
                            "owner": "1.2.26",
                            "label": "label1",
                            "extensions": []
                        }
                    ]
                ],
                "extensions": [],
                "signatures": [],
                "signed_with_echorand_key": false
            },
            [
                "ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu"
            ]
        ]
    ]
}
```

#### Returns

An set of public keys.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        "ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu"
    ]
}
```

### get\_potential\_signatures\(ctrx\)

This method will return the set of all public keys that could possibly sign for a given transaction. This call can be used by wallets to filter their set of public keys to just the relevant subset prior to calling get\_required\_signatures to get the minimum subset.

#### Parameters

| Option | Description |
| :--- | :--- |
| `signed_transaction trx` | object signed transaction |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_potential_signatures",
        [
            {
                "ref_block_num": 1719,
                "ref_block_prefix": 3664479505,
                "expiration": "2019-08-21T14:16:03",
                "operations": [
                    [
                        28,
                        {
                            "fee": {
                                "amount": 5001,
                                "asset_id": "1.3.0"
                            },
                            "owner": "1.2.26",
                            "label": "label1",
                            "extensions": []
                        }
                    ]
                ],
                "extensions": [],
                "signatures": [
                    "aa936713a49db3b2881ece72879dc2cb22c4b81368f9bbb4e57666b7277b96e153a5519a8fed82ca54ee71cc3dd0a33c614aa44613580009e2de242de5ce8902"
                ],
                "signed_with_echorand_key": false
            }
        ]
    ]
}
```

#### Returns

An set of public keys.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        "ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu"
    ]
}
```

### verify\_authority\(trx\)

Returns true of the trx has all of the required signatures, otherwise throws an exception.

#### Parameters

| Option | Description |
| :--- | :--- |
| `signed_transaction trx` | object signed transaction |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "verify_authority",
        [
            {
                "ref_block_num": 1719,
                "ref_block_prefix": 3664479505,
                "expiration": "2019-08-21T14:16:03",
                "operations": [
                    [
                        28,
                        {
                            "fee": {
                                "amount": 5001,
                                "asset_id": "1.3.0"
                            },
                            "owner": "1.2.26",
                            "label": "label1",
                            "extensions": []
                        }
                    ]
                ],
                "extensions": [],
                "signatures": [
                    "aa936713a49db3b2881ece72879dc2cb22c4b81368f9bbb4e57666b7277b96e153a5519a8fed82ca54ee71cc3dd0a33c614aa44613580009e2de242de5ce8902"
                ],
                "signed_with_echorand_key": false
            }
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": true
}
```

### verify\_account\_authority\(name\_or\_id, signers\)

Returns true if the signers have enough authority to authorize an account.

#### Parameters

| Option | Description |
| :--- | :--- |
| `string name_or_id` | the name or ID of the account |
| `flat_set<public_key_t> signers` | an array of public keys |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "verify_account_authority",
        [
            "nathan",
            [
                "ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu"
            ]
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": true
}
```

### validate\_transaction\(trx\)

Validates a transaction against the current state without broadcasting it on the network.

#### Parameters

| Option | Description |
| :--- | :--- |
| `signed_transaction trx` | object signed transaction |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "validate_transaction",
        [
            {
                "ref_block_num": 3530,
                "ref_block_prefix": 636194404,
                "expiration": "2019-08-21T15:36:27",
                "operations": [
                    [
                        28,
                        {
                            "fee": {
                                "amount": 5002,
                                "asset_id": "1.3.0"
                            },
                            "owner": "1.2.26",
                            "label": "god_please",
                            "extensions": []
                        }
                    ]
                ],
                "extensions": [],
                "signatures": [
                    "22e67b0b5072fd1e6901d983663b093b81898b318f34ee931e244f076c387cda7f32027cc31b7d50c77299072ddc516ffaf538e6b5c6d385830f1b4d050db20f"
                ],
                "signed_with_echorand_key": false
            }
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "ref_block_num": 3530,
        "ref_block_prefix": 636194404,
        "expiration": "2019-08-21T15:36:27",
        "operations": [
            [
                28,
                {
                    "fee": {
                        "amount": 5002,
                        "asset_id": "1.3.0"
                    },
                    "owner": "1.2.26",
                    "label": "god_please",
                    "extensions": []
                }
            ]
        ],
        "extensions": [],
        "signatures": [
            "22e67b0b5072fd1e6901d983663b093b81898b318f34ee931e244f076c387cda7f32027cc31b7d50c77299072ddc516ffaf538e6b5c6d385830f1b4d050db20f"
        ],
        "signed_with_echorand_key": false,
        "operation_results": [
            [
                1,
                "2.15.4"
            ]
        ]
    }
}
```

### get\_required\_fees\(ops, id\)

For each operation calculate the required fee in the specified asset type. If the asset type does not have a valid core\_exchange\_rate.

#### Parameters

| Option | Description |
| :--- | :--- |
| `string name_or_id` | the name or ID of the account |
| `flat_set<public_key_t> signers` | an array of public keys |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_required_fees",
        [
            [
                [
                    28,
                    {
                        "fee": {
                            "amount": 5002,
                            "asset_id": "1.3.0"
                        },
                        "owner": "1.2.26",
                        "label": "god_please",
                        "extensions": []
                    }
                ]
            ],
            "1.3.0"
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "amount": 5002,
            "asset_id": "1.3.0"
        }
    ]
}
```

## Proposed transactions

### get\_proposed\_transactions\(id\)

Returns the set of proposed transactions relevant to the specified account id.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type id` | the ID of the account |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_proposed_transactions",
        [
            "1.2.26"
        ]
    ]
}
```

#### Returns

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.5.0",
            "expiration_time": "1970-01-01T00:00:00",
            "proposed_transaction": {
                "ref_block_num": 221,
                "ref_block_prefix": 4141892275,
                "expiration": "1970-01-01T00:00:00",
                "operations": [],
                "extensions": []
            },
            "required_active_approvals": [],
            "available_active_approvals": [],
            "available_key_approvals": [],
            "extensions": []
        }
    ]
}
```

## Sidechain

### get\_eth\_address\(account\)

Returns information about generated ethereum address, if then exist and approved, for the given account id.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type account` | the id of the account to provide information about |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_eth_address",
        [
            "1.2.21"
        ]
    ]
}
```

#### Returns

The public ethereum address data stored in the blockchain

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "id": "1.12.0",
        "account": "1.2.21",
        "eth_addr": "1134464B537884EE89cb298eEd674C9B14BCce47",
        "is_approved": true,
        "approves": [],
        "extensions": []
    }
}
```

### get\_account\_deposits\(account\)

Returns all approved deposits, for the given account id.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type account` | the id of the account to provide information about |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_account_deposits",
        [
            "1.2.21"
        ]
    ]
}
```

#### Returns

The all public deposits data stored in the blockchain.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.13.0",
            "deposit_id": 0,
            "account": "1.2.21",
            "value": 1000,
            "is_approved": true,
            "approves": [],
            "extensions": []
        }
    ]
}
```

### get\_account\_withdrawals\(account\)

Returns all approved withdrawals, for the given account id.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type account` | the id of the account to provide information about |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_account_withdrawals",
        [
            "1.2.21"
        ]
    ]
}
```

#### Returns

The all public withdrawals data stored in the blockchain.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.14.0",
            "withdraw_id": 0,
            "account": "1.2.21",
            "eth_addr": "1AFeEcE88325110488570146f2635C8615Ad0613",
            "value": 1000,
            "is_approved": true,
            "approves": [],
            "extensions": []
        }
    ]
}
```

## Sidechain ERC20

### get\_erc20\_token\(eth\_addr\)

Returns information about erc20 token, if then exist.

#### Parameters

| Option | Description |
| :--- | :--- |
| `eth_address_type eth_addr` | the ethereum address of token in Ethereum network |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_erc20_token",
        [
            "8B5D021C528Cb0ADb9dA277D109c039dEdFd6871"
        ]
    ]
}
```

#### Returns

The public erc20 token data stored in the blockchain.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "id": "1.15.0",
        "owner": "1.2.0",
        "eth_addr": "8B5D021C528Cb0ADb9dA277D109c039dEdFd6871",
        "contract": "1.9.0",
        "name": "erc20",
        "symbol": "ERC",
        "decimals": 0
    }
}
```

### get\_erc20\_account\_deposits\(account\)

Returns all approved deposits, for the given account id.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type account` | the id of the account to provide information about |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_erc20_account_deposits",
        [
            "1.2.0"
        ]
    ]
}
```

#### Returns

The all public erc20 deposits data stored in the blockchain.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.16.0",
            "account": "1.2.0",
            "erc20_addr": "8B5D021C528Cb0ADb9dA277D109c039dEdFd6871",
            "value": "1",
            "transaction_hash": "9742f2d928365be7591107b0d8afa701f24104acd8d5ecc32516dfab410f9c4e",
            "is_approved": true,
            "approves": []
        }
    ]
}
```

### get\_erc20\_account\_withdrawals\(account\)

Returns all approved withdrawals, for the given account id.

#### Parameters

| Option | Description |
| :--- | :--- |
| `account_id_type account` | the id of the account to provide information about |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_erc20_account_withdrawals",
        [
            "1.2.0"
        ]
    ]
}
```

#### Returns

The all public erc20 withdrawals data stored in the blockchain.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": [
        {
            "id": "1.17.0",
            "withdraw_id": 0,
            "account": "1.2.0",
            "to": "1AFeEcE88325110488570146f2635C8615Ad0613",
            "erc20_token": "1.15.0",
            "value": "1",
            "is_approved": true,
            "approves": []
        }
    ]
}
```

## Contract Feepool

### get\_contract\_pool\_balance\(id\)

Get an contract's pool balance in default asset.

#### Parameters

| Option | Description |
| :--- | :--- |
| `contract_id_type id` | ID of the contract to get balances for |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_contract_pool_balance",
        [
            "1.9.0"
        ]
    ]
}
```

#### Returns

Balances of the contract.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "amount": 1,
        "asset_id": "1.3.0"
    }
}
```

### get\_contract\_pool\_whitelist\(id\)

Get an contract's whitelist and blacklist.

#### Parameters

| Option | Description |
| :--- | :--- |
| `contract_id_type id` | ID of the contract to get balances for |

#### Example

```javascript
{
    "id": 4,
    "method": "call",
    "params": [
        DATABASE_API_ID,
        "get_contract_pool_whitelist",
        [
            "1.9.0"
        ]
    ]
}
```

#### Returns

Struct contract\_pool\_whitelist which consist of whitelist blacklist.

```javascript
{
    "id": 4,
    "jsonrpc": "2.0",
    "result": {
        "whitelist": [
            "1.2.1"
        ],
        "blacklist": [
            "1.2.2"
        ]
    }
}
```

