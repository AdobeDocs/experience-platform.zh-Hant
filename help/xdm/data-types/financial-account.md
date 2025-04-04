---
title: 財務帳戶資料型別
description: 瞭解財務帳戶XDM資料型別。
exl-id: badf9b20-d397-4b46-b045-19c69806fe8e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 8%

---

# [!UICONTROL 財務帳戶]資料型別

[!UICONTROL 財務帳戶]是標準的XDM資料型別，說明財務帳戶的詳細資料，包括其型別、擁有者和目前餘額。

![](../images/data-types/financial-account.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `currentAccountBalance` | [[!UICONTROL 貨幣]](./currency.md) | 帳戶的目前餘額。 |
| `financialAccountId` | [!UICONTROL 字串] | 帳戶的唯一ID。 |
| `financialAccountName` | [!UICONTROL 字串] | 指派給帳戶的名稱。 |
| `financialAccountType` | [!UICONTROL 字串] | 財務帳戶的型別，例如，支票、存款或退休。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/financial-account.schema.json)。
