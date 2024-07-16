---
title: 存款詳細資料結構欄位群組
description: 瞭解存款詳細資料結構欄位群組。
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 4%

---

# [!UICONTROL 存款詳細資料]結構描述欄位群組

[!UICONTROL 存款詳細資料]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組。 欄位群組提供單一`personalFinances.deposits`欄位給結構描述，擷取有關財務存款的詳細資料。

![](../../images/field-groups/deposit-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `account` | [[!UICONTROL 財務帳戶]](../../data-types/financial-account.md) | 描述與存款關聯的財務帳戶。 |
| `transaction` | [[!UICONTROL 交易]](../../data-types/transaction.md) | 描述與存款相關的財務交易。 |
| `mobileDeposit` | [!UICONTROL 布林值] | 指出存款是否透過行動平台完成。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json)。
