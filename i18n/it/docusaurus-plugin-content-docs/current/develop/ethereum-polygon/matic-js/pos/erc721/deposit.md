---
id: deposit
title: deposit
keywords:
- 'pos client, erc721, deposit, polygon, sdk'
description: 'Deposita un token da ethereum alla catena di polygon.'
---

Il metodo `deposit` può essere utilizzato per depositare un token da ethereum alla catena di polygon.

```
const erc721RootToken = posClient.erc721(<root token address>, true);

const result = await erc721RootToken.deposit(<token id>, <user address>);

const txHash = await result.getTransactionHash();

const txReceipt = await result.getReceipt();

```
