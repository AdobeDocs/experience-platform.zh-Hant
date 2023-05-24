---
title: 餘額轉移方案欄位組
description: 此文檔提供「餘額轉移」方案欄位組的概覽。
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 1%

---

# [!UICONTROL 餘額轉移] 架構欄位組

[!UICONTROL 餘額轉移] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)。 欄位組提供單個 `personalFinances.balanceTransfers` 對象到架構，該架構捕獲有關帳戶之間財務餘額轉移的詳細資訊。

![](../../images/field-groups/balance-transfers.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL 財務帳戶]](../../data-types/financial-account.md) | 描述從中轉移餘額的財務帳戶。 |
| `accountTo` | [[!UICONTROL 財務帳戶]](../../data-types/financial-account.md) | 描述要轉移餘額的財務帳戶。 |
| `transaction` | [[!UICONTROL 交易記錄]](../../data-types/transaction.md) | 描述與餘額轉移關聯的財務交易記錄。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json)。
