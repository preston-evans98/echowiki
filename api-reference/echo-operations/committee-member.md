# Committee Member Operations

## committee_member_create_operation

Create a committee_member object, as a bid to hold a committee_member seat on the network.

Accounts which wish to become committee_members may use this operation to create a committee_member object which stakeholders may vote on to approve its position as a committee_member.

```cpp
struct committee_member_create_operation : public base_operation
{
   struct fee_parameters_type { uint64_t fee = 5000 * ECHO_BLOCKCHAIN_PRECISION; };

   asset                                 fee;
   /// The account which owns the committee_member. This account pays the fee for this operation.
   account_id_type                       committee_member_account;
   string                                url;
   
   eth_address_type                      eth_address;

   extensions_type extensions;

   account_id_type fee_payer()const { return committee_member_account; }
   void            validate()const;
};
```

### JSON Example

```json
[
  16,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "committee_member_account": "1.2.0",
    "url": "",
    "eth_address": "0000000000000000000000000000000000000000",
    "extensions": []
  }
]
```

## committee_member_update_operation

Update a committee_member object.

Currently the only field which can be updated is the `url` field.

```cpp
struct committee_member_update_operation : public base_operation
{
   struct fee_parameters_type { uint64_t fee = 20 * ECHO_BLOCKCHAIN_PRECISION; };

   asset                                 fee;
   /// The committee member to update.
   committee_member_id_type              committee_member;
   /// The account which owns the committee_member. This account pays the fee for this operation.
   account_id_type                       committee_member_account;
   optional< string >                    new_url;
   optional< eth_address_type >          new_eth_address;

   extensions_type extensions;

   account_id_type fee_payer()const { return committee_member_account; }
   void            validate()const;
};
```

### JSON Example

```json
[
  17,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "committee_member": "1.4.0",
    "committee_member_account": "1.2.0",
    "extensions": []
  }
]
```

## committee_member_update_global_parameters_operation

Used by committee_members to update the global parameters of the blockchain.

This operation allows the committee_members to update the global parameters on the blockchain. These control various tunable aspects of the chain, including block and maintenance intervals, maximum data sizes, the fees charged by the network, etc.

This operation may only be used in a proposed transaction, and a proposed transaction which contains this operation must have a review period specified in the current global parameters before it may be accepted.

```cpp
struct committee_member_update_global_parameters_operation : public base_operation
{
   struct fee_parameters_type { uint64_t fee = ECHO_BLOCKCHAIN_PRECISION; };

   asset             fee;
   chain_parameters  new_parameters;

   extensions_type extensions;

   account_id_type fee_payer()const { return account_id_type(); }
   void            validate()const;
};
```

### JSON Example

```json
[
  18,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "new_parameters": {
      "current_fees": {
        "parameters": [],
        "scale": 10000
      },
      "block_interval": 5,
      "maintenance_interval": 86400,
      "maintenance_duration_seconds": 10,
      "committee_proposal_review_period": 1209600,
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
        "_time_net_1mb": 0,
        "_time_net_256b": 0,
        "_creator_count": 0,
        "_verifier_count": 0,
        "_ok_threshold": 0,
        "_max_bba_steps": 0,
        "_gc1_delay": 0
      },
      "sidechain_config": {
        "eth_contract_address": "0000000000000000000000000000000000000000",
        "eth_committee_update_method": {
          "method": "",
          "gas": 0
        },
        "eth_gen_address_method": {
          "method": "",
          "gas": 0
        },
        "eth_withdraw_method": {
          "method": "",
          "gas": 0
        },
        "eth_update_addr_method": {
          "method": "",
          "gas": 0
        },
        "eth_withdraw_token_method": {
          "method": "",
          "gas": 0
        },
        "eth_collect_tokens_method": {
          "method": "",
          "gas": 0
        },
        "eth_committee_updated_topic": "0000000000000000000000000000000000000000000000000000000000000000",
        "eth_gen_address_topic": "0000000000000000000000000000000000000000000000000000000000000000",
        "eth_deposit_topic": "0000000000000000000000000000000000000000000000000000000000000000",
        "eth_withdraw_topic": "0000000000000000000000000000000000000000000000000000000000000000",
        "erc20_deposit_topic": "0000000000000000000000000000000000000000000000000000000000000000",
        "ETH_asset_id": "1.3.0",
        "fines": {
          "generate_eth_address": 0
        },
        "waiting_blocks": 0
      },
      "erc20_config": {
        "contract_code": "",
        "create_token_fee": 0,
        "transfer_topic": "0000000000000000000000000000000000000000000000000000000000000000",
        "check_balance_method": {
          "method": "",
          "gas": 0
        },
        "burn_method": {
          "method": "",
          "gas": 0
        },
        "issue_method": {
          "method": "",
          "gas": 0
        }
      },
      "gas_price": {
        "price": 1,
        "gas_amount": 1000
      },
      "extensions": []
    },
    "extensions": []
  }
]
```