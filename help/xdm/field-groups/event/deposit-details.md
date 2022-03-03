---
title: 存款詳細資訊方案欄位組
description: 本文檔提供存款詳細資訊架構欄位組的概覽。
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 4%

---

# [!UICONTROL Deposit Details] schema field group

[!UICONTROL 存款詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)。 The field group provides a single `personalFinances.deposits` field to a schema, which captures details about a financial deposit.

![](../../images/field-groups/deposit-details.png)

| 屬性 | Data type | 說明 |
| --- | --- | --- |
| `account` | [[!UICONTROL 財務帳戶]](../../data-types/financial-account.md) | Describes the financial account associated with the deposit. |
| `transaction` | [[!UICONTROL Transaction]](../../data-types/transaction.md) | 描述與存款關聯的財務交易記錄。 |
| `mobileDeposit` | [!UICONTROL 布爾型] | 指示押金是否通過移動平台完成。 |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the [public XDM repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
