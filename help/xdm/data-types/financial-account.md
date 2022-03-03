---
title: 財務帳戶資料類型
description: 此文檔概述了財務帳戶XDM資料類型。
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 8%

---

# [!UICONTROL 財務帳戶] 資料類型

[!UICONTROL 財務帳戶] 是一個標準XDM資料類型，它描述財務帳戶的詳細資訊，包括其類型、所有者和當前餘額。

![](../images/data-types/financial-account.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL 貨幣]](./currency.md) | 帳戶的當前餘額。 |
| `financialAccountId` | [!UICONTROL 字串] | 帳戶的唯一ID。 |
| `financialAccountName` | [!UICONTROL 字串] | 分配給帳戶的名稱。 |
| `financialAccountType` | [!UICONTROL 字串] | 財務帳戶的類型，如支票、儲蓄或退休。 |

{style=&quot;table-layout:auto&quot;}

有關資料類型的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json)。
