---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；個人配置檔案；欄位；模式；模式；忠誠詳細資訊；模式設計；欄位組；欄位組；
solution: Experience Platform
title: 會員詳細資訊方案欄位組
description: 此文檔概述了「會員詳細資訊」方案欄位組。
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 2%

---

# [!UICONTROL 會員詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 會員詳細資訊] 是標準架構欄位組 [[!DNL XDM Individual Profile] 類](../../classes/individual-profile.md)。 欄位組提供單個對象類型欄位， `loyalty`，它捕獲與客戶忠誠計畫中的人員成員資格相關的資訊。

![](../../images/field-groups/loyalty-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `pointsExpiration` | 對象陣列 | 列出將到期的任何會員點（或會員點組），以及將到期的日期。 每個陣列項必須是包含以下兩個屬性的對象： <ul><li>`pointsExpirationDate`:ISO 8601日期時間，指點將過期的時間。</li><li>`pointsExpiring`:截至關聯到期日的到期點餘額。</li></ul> |
| `joinDate` | 日期時間 | ISO 8601日期時間，該人員加入忠誠計畫的時間。 |
| `loyaltyID` | 字串陣列 | 表示與會員計畫成員關聯的會員計畫ID。 |
| `points` | 雙倍 | 忠誠成員的當前忠誠積分或獎勵餘額。 |
| `pointsRedeemed` | 雙倍 | 會員已應用於採購或已換領的積分金額。 |
| `program` | 字串 | 登記人員的會員計畫的名稱。 |
| `status` | 字串 | 人員的會員資格的當前狀態，如 `active`。 `disabled`或 `suspended`。 |
| `tier` | 字串 | 捕獲登記人員的會員計畫層。 |
| `upgradeDate` | 字串 | 會員成員升級到其最新層級的日期。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
