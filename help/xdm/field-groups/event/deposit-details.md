---
title: 存款詳細資訊結構欄位組
description: 本文檔提供「存款詳細資訊」架構欄位組的概述。
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 2%

---

# [!UICONTROL 存款詳細資訊] 方案欄位組

[!UICONTROL 存款詳細資訊] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md). 欄位群組提供單一 `personalFinances.deposits` 欄位至結構，可擷取有關金融存款的詳細資訊。

![](../../images/field-groups/deposit-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `account` | [[!UICONTROL 財務帳戶]](../../data-types/financial-account.md) | 說明與存款關聯的財務帳戶。 |
| `transaction` | [[!UICONTROL 交易]](../../data-types/transaction.md) | 說明與存款關聯的金融交易。 |
| `mobileDeposit` | [!UICONTROL 布林值] | 指出押金是否透過行動平台完成。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
