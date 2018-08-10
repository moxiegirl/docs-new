---
layout: naming
title: Lookup the name state history
subtitle: Cras at dolor eget urna varius faucibus tempus in elit. Cras a dui imperdiet, tempus metus quis, pharetra turpis.
author:
tags: othertag
---
```bash
$ curl https://core.blockstack.org/v1/names/patrickstanley.id/history
{
  "445838": [
    {
      "address": "1occgbip7tFDXX9MvzQhcnTUUjcVX2dYK",
      "block_number": 445838,
      "burn_address": "1111111111111111111114oLvT2",
      "consensus_hash": "7b696b6f4060b792d41912068944d73b",
      "op": "?",
      "op_fee": 25000,
      "opcode": "NAME_PREORDER",
      "preorder_hash": "26bf7874706ac761afdd403ed6b3b9578fb01a34",
      "sender": "76a91408d0dd44c1f0a3a4f0957ae95901929d7d66d55788ac",
      "sender_pubkey": "039a8948d339ecbff44cf426cb85d90fce876f1658d385cdc47f007f279be626ea",
      "txid": "6730ae09574d5935ffabe3dd63a9341ea54fafae62fde36c27738e9ee9c4e889",
      "vtxindex": 40
    }
  ],
  "445851": [
    {
      "address": "17CbHgTgBG3kLedXNneEKBkCTgW2fyrnUD",
      "block_number": 445838,
      "consensus_hash": null,
      "first_registered": 445851,
      "importer": null,
      "importer_address": null,
      "last_creation_op": "?",
      "last_renewed": 445851,
      "name": "patrickstanley.id",
      "name_hash128": "683a3e1ee5f0296833c56e481cf41b77",
      "namespace_block_number": 373601,
      "namespace_id": "id",
      "op": ":",
      "op_fee": 25000,
      "opcode": "NAME_REGISTRATION",
      "preorder_block_number": 445838,
      "preorder_hash": "26bf7874706ac761afdd403ed6b3b9578fb01a34",
      "revoked": false,
      "sender": "76a9144401f3be5311585ea519c1cb471a8dc7b02fd6ee88ac",
      "sender_pubkey": "039a8948d339ecbff44cf426cb85d90fce876f1658d385cdc47f007f279be626ea",
      "transfer_send_block_id": null,
      "txid": "55b8b42fc3e3d23cbc0f07d38edae6a451dfc512b770fd7903725f9e465b2925",
      "value_hash": null,
      "vtxindex": 54
    }
  ],
  "445873": [
    {
      "address": "17CbHgTgBG3kLedXNneEKBkCTgW2fyrnUD",
      "block_number": 445838,
      "consensus_hash": "18b8d69f0182b89ccb1aa536f83be18a",
      "first_registered": 445851,
      "importer": null,
      "importer_address": null,
      "last_creation_op": "?",
      "last_renewed": 445851,
      "name": "patrickstanley.id",
      "name_hash128": "683a3e1ee5f0296833c56e481cf41b77",
      "namespace_block_number": 373601,
      "namespace_id": "id",
      "op": "+",
      "op_fee": 25000,
      "opcode": "NAME_UPDATE",
      "preorder_block_number": 445838,
      "preorder_hash": "26bf7874706ac761afdd403ed6b3b9578fb01a34",
      "revoked": false,
      "sender": "76a9144401f3be5311585ea519c1cb471a8dc7b02fd6ee88ac",
      "sender_pubkey": "039a8948d339ecbff44cf426cb85d90fce876f1658d385cdc47f007f279be626ea",
      "transfer_send_block_id": null,
      "txid": "dc478659fc684a1a6e1e09901971e82de11f4dfe2b32a656700bf9a3b6030719",
      "value_hash": "02af0ef21161ad06b0923106f40b994b9e4c1614",
      "vtxindex": 95
    }
  ],
  "445884": [
    {
      "address": "1GZqrVbamkaE6YNveJFWK6cDrCy6bXyS6b",
      "block_number": 445838,
      "consensus_hash": "18b8d69f0182b89ccb1aa536f83be18a",
      "first_registered": 445851,
      "importer": null,
      "importer_address": null,
      "last_creation_op": "?",
      "last_renewed": 445851,
      "name": "patrickstanley.id",
      "name_hash128": "683a3e1ee5f0296833c56e481cf41b77",
      "namespace_block_number": 373601,
      "namespace_id": "id",
      "op": ">>",
      "op_fee": 25000,
      "opcode": "NAME_TRANSFER",
      "preorder_block_number": 445838,
      "preorder_hash": "26bf7874706ac761afdd403ed6b3b9578fb01a34",
      "revoked": false,
      "sender": "76a914aabffa6dd90d731d3a349f009323bb312483c15088ac",
      "sender_pubkey": null,
      "transfer_send_block_id": 445875,
      "txid": "7a0a3bb7d39b89c3638abc369c85b5c028d0a55d7804ba1953ff19b0125f3c24",
      "value_hash": "02af0ef21161ad06b0923106f40b994b9e4c1614",
      "vtxindex": 16
    }
  ]
}
```

All of the above information is extracted from the blockchain.  Each top-level
field encodes the states the name transitioned to at the given block height (e.g.
445838, 445851, 445873, adn 445884).  At each block height, the name's zone file
hashes are returned in the order they were discovered in the blockchain.

Each name state contains a lot of ancillary data that is used internally by
other API calls and client libraries.  The relevant fields for this document's
scope are:

* `address`: This is the base58check-encoded public key hash.
* `name`:  This is the name queried.
* `value_hash`:  This is the zone file hash.
* `opcode`:  This is the type of transaction that was processed.
* `txid`:  This is the transaction ID in the underlying blockchain.

The name's *entire* history is returned.  This includes the history of the name
under its previous owner, if the name expired and was reregistered.
