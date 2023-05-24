---
title: 存款詳細資訊方案欄位組
description: 本文檔提供存款詳細資訊架構欄位組的概覽。
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 2%

---

# [!UICONTROL 存款詳細資訊] 架構欄位組

[!UICONTROL 存款詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)。 欄位組提供單個 `personalFinances.deposits` 欄位，用於捕獲有關財務存款的詳細資訊。

![](../../images/field-groups/deposit-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `account` | [[!UICONTROL 財務帳戶]](../../data-types/financial-account.md) | 描述與存款關聯的財務帳戶。 |
| `transaction` | [[!UICONTROL 交易記錄]](../../data-types/transaction.md) | 描述與存款關聯的財務交易記錄。 |
| `mobileDeposit` | [!UICONTROL 布林值] | 指示押金是否通過移動平台完成。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json)。
